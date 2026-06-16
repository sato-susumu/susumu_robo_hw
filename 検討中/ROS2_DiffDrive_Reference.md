# ROS2 差動二輪 リファレンスモデル

ROS2 (Humble / Jazzy 世代) における差動二輪 (differential drive) ロボットの標準的なソフトウェア構成と、本リポジトリのハードウェア (ODrive BotWheel Explorer + Raspberry Pi 4 + Livox MID-360) への適用指針をまとめる。

---

## 目次

1. [標準ソフトウェアスタックの全体像](#標準ソフトウェアスタックの全体像)
2. [各ノード・プラグインの責務](#各ノードプラグインの責務)
3. [データフロー (トピック・TF)](#データフロー-トピックtf)
4. [diff_drive_controller の主要パラメータ](#diff_drive_controller-の主要パラメータ)
5. [Nav2 との連携要件](#nav2-との連携要件)
6. [既存リファレンス実装の比較](#既存リファレンス実装の比較)
7. [本構成 (BotWheel Explorer) への適用](#本構成-botwheel-explorer-への適用)
8. [Livox MID-360 と SLAM/Nav2](#livox-mid-360-と-slamnav2)
9. [差動二輪の運動学モデル](#差動二輪の運動学モデル)
10. [本構成のパラメータ早見表](#本構成のパラメータ早見表)
11. [残課題 (要追加調査)](#残課題-要追加調査)

---

## 標準ソフトウェアスタックの全体像

> **引用元**: [diff_drive_controller - control.ros.org (Jazzy)](https://control.ros.org/jazzy/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html) / [ros2_control_demos example_2 (DiffBot)](https://control.ros.org/jazzy/doc/ros2_control_demos/example_2/doc/userdoc.html)

ROS2 世代の差動二輪では、`ros2_control` の `controller_manager` が以下の2つのコントローラを同時に active で動かし、`robot_state_publisher` が残りの TF を出す構成が定石である。これは ros2_control 公式デモ `example_2` (DiffBot) でそのまま実証されている。

| 構成要素 | 種別 | プラグイン/パッケージ |
|----------|------|----------------------|
| controller_manager | ros2_control 本体 | `controller_manager` |
| 差動二輪コントローラ | controller | `diff_drive_controller/DiffDriveController` |
| ジョイント状態ブロードキャスタ | broadcaster | `joint_state_broadcaster/JointStateBroadcaster` |
| ハードウェアインターフェース | hardware (system) | カスタム `SystemInterface` 派生プラグイン |
| ロボット状態パブリッシャ | 独立ノード | `robot_state_publisher` |

---

## 各ノード・プラグインの責務

> **引用元**: [diff_drive_controller (Jazzy)](https://control.ros.org/jazzy/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html) / [joint_state_broadcaster (Humble)](https://control.ros.org/humble/doc/ros2_controllers/joint_state_broadcaster/doc/userdoc.html) / [Nav2 Odometry setup](https://docs.nav2.org/setup_guides/odom/setup_odom_gz.html)

| 要素 | 責務 |
|------|------|
| **diff_drive_controller** | ロボット本体の速度指令 (cmd_vel の `linear.x`, `angular.z`) を左右ホイール速度へ変換 (逆運動学)。ホイールのフィードバックからオドメトリを計算し公開。`odom→base_link` の TF をブロードキャスト |
| **joint_state_broadcaster** | ハードウェアの全 state interface を読み、`/joint_states`・`/dynamic_joint_states` へ公開。**指令は受けない** (broadcaster は real controller ではないため) |
| **robot_state_publisher** | URDF と `/joint_states` から、`base_link→各リンク (ホイール等)` の TF を公開 |
| **hardware_interface (system)** | `read()` で実HWの位置/速度を state interface へ、`write()` で command interface の値を実HWへ反映 |

公式表現:
- diff_drive_controller: 「velocity commands for the robot body, which are translated to wheel commands for the differential drive base」「Odometry is computed from hardware feedback and published」
- joint_state_broadcaster: 「reads all state interfaces and reports them on `/joint_states` and `/dynamic_joint_states`」「broadcasters are not real controllers, and therefore take no commands」

> **注意**: `odom→base_link` の TF は **diff_drive_controller** が、`base_link→ホイール` の TF は **robot_state_publisher** が出す。役割が分かれている点に注意。

---

## データフロー (トピック・TF)

```
[Nav2 / teleop / joystick]
        │  geometry_msgs/Twist(Stamped)
        ▼
   (twist_mux)              ← 複数 cmd_vel の優先度付き多重化 (任意)
        │  ~/cmd_vel
        ▼
┌─────────────────────────────────────────────┐
│ controller_manager                          │
│  ┌───────────────────────┐                  │
│  │ diff_drive_controller │                  │
│  │  cmd_vel → 左右ホイール速度 (逆運動学)     │──── command interface ──┐
│  │  フィードバック → odometry                 │                          │
│  └───────────────────────┘                  │                          ▼
│  ┌───────────────────────┐                  │              ┌──────────────────────┐
│  │ joint_state_broadcaster│                 │◀── state ────│ hardware_interface    │
│  └───────────────────────┘                  │   interface  │ (実HW: ODrive CAN等)  │
└─────────────────────────────────────────────┘              └──────────────────────┘
        │  ~/odom (nav_msgs/Odometry)          │  /joint_states
        │  /tf: odom→base_link                 ▼
        │                            [robot_state_publisher]
        ▼                                      │  /tf: base_link→各リンク
   [Nav2 / EKF]  ◀────────────────────────────┘ (+ URDF)
```

- **cmd_vel の入口**: Nav2 や teleop が `geometry_msgs/Twist(Stamped)` を発行。複数ソースがある場合は `twist_mux` で優先度付きに多重化してから `~/cmd_vel` へ。
- **オドメトリの出口**: `~/odom` (`nav_msgs/Odometry`) と `odom→base_link` TF。これがそのまま Nav2 のオドメトリ要件を満たす。

---

## diff_drive_controller の主要パラメータ

> **引用元**: [diff_drive_controller (Jazzy)](https://control.ros.org/jazzy/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html) / [(Humble)](https://control.ros.org/humble/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html)

| パラメータ | 内容 |
|------------|------|
| `left_wheel_names` / `right_wheel_names` | 左右ホイールのジョイント名 (リスト) |
| `wheel_separation` | **左右ホイール間の最短距離** (= トラック幅)。誤るとカーブ挙動が不正に |
| `wheel_radius` | ホイール半径。線速度→ホイール回転の変換に使用。誤ると速度が想定と変わる |
| `enable_odom_tf` | `true` (既定) で `odom→base_link` TF を `/tf` へ公開 |
| `odom_frame_id` / `base_frame_id` | 既定 `odom` / `base_link` |
| `open_loop` | `true` で指令値からオドメトリ算出、`false` (既定) でHWフィードバックから算出 |

公式表現:
- `wheel_separation`: 「Shortest distance between the left and right wheels. If this parameter is wrong, the robot will not behave correctly in curves.」
- `wheel_radius`: 「used for transformation of linear velocity into wheel rotations. If this parameter is wrong the robot will move faster or slower than expected.」

### cmd_vel のメッセージ型 (ディストリ差に注意)

| ディストリ | 購読トピック / 型 |
|------------|-------------------|
| **Jazzy** | `~/cmd_vel` = `geometry_msgs/TwistStamped` **必須** (旧 `use_stamped_vel` / `~/cmd_vel_unstamped` は廃止) |
| **Humble** | `use_stamped_vel=true` → `~/cmd_vel` (TwistStamped) / `false` → `~/cmd_vel_unstamped` (Twist) |

> コントローラが使うのは `linear.x` と `angular.z` のみ。**実装時は対象ディストリで必ずメッセージ型を確認すること** (本スタックで世代差が出る数少ない箇所)。

---

## Nav2 との連携要件

> **引用元**: [Nav2 Setting Up Odometry](https://docs.nav2.org/setup_guides/odom/setup_odom_gz.html)

Nav2 はオドメトリ源に対し、以下の **両方** の公開を要求する。

| 要件 | 内容 |
|------|------|
| `nav_msgs/Odometry` メッセージ | pose と **velocity** を含む (TF だけでは速度情報を運べないため) |
| `odom→base_link` TF | 連続的 (locally accurate) な姿勢推定 |

公式表現: 「the navigation stack requires that any odometry source publish both a transform and a `nav_msgs/Odometry` message ... that contains velocity information」「Nav2 requires the `nav_msgs/Odometry` message and `odom => base_link` transforms」

diff_drive_controller の `~/odom` + `enable_odom_tf` 出力がこの要件をそのまま満たす。オドメトリは「局所的に正確だが時間/距離で漂流する」連続成分であり、グローバルセンサ (SLAM/LiDAR) で `map→odom` を補正する。

---

## 既存リファレンス実装の比較

> **引用元**: 各プロジェクト公式リポジトリ ([articubot_one](https://github.com/joshnewans/articubot_one) / [Andino](https://github.com/Ekumen-OS/andino) / [linorobot2](https://github.com/linorobot/linorobot2) / [DiffBot example_2](https://control.ros.org/jazzy/doc/ros2_control_demos/example_2/doc/userdoc.html))

| プロジェクト | 対象HW / 接続 | ros2_control | オドメトリ算出場所 | 特徴 |
|--------------|---------------|--------------|--------------------|------|
| **DiffBot (example_2)** | 公式デモ (仮想HW) | ✅ カスタム `SystemInterface` | ホスト (HW I/F) | **最小テンプレート**。HW自作の雛形 |
| **articubot_one** (J. Newans) | Arduino / シリアル 57600 | ✅ `diffdrive_arduino` | ホスト (HW I/F) | Nav2+slam_toolbox+twist_mux+joystick 一式同梱。教材として定番 |
| **Andino** (Ekumen-OS) | マイコン / シリアル | ✅ `andino_base` (HW I/F) | マイコンファーム | Humble/Jazzy 両対応のフルOSS。`andino_control`/`andino_base`/`andino_firmware` の3層構成 |
| **linorobot2** | Teensy等 / micro-ROS | ❌ (micro-ROS でオフロード) | **マイコンファーム** (エッジ計算) | 2WD/4WD/Mecanum対応。Nav2+SLAM Toolbox+robot_localization EKF 統合済み |
| **TurtleBot4** | iRobot Create3 | (Create3側で処理) | ベース内蔵 | 完成品。リファレンスというより製品 |

### 設計上の分岐点: オドメトリをどこで計算するか

- **ホスト側 (ros2_control HW I/F)**: DiffBot / articubot_one / Andino。`read()` でエンコーダ生値を取得し、diff_drive_controller がオドメトリを算出。**本構成の推奨パターン** (後述)。
- **マイコン/エッジ側 (micro-ROS)**: linorobot2。ファームが PID 制御・オドメトリ・IMU 融合まで担い、`/odom` を直接公開。ros2_control を使わない別アーキテクチャ。

> articubot_one の値 (`wheel_separation 0.297m`, `wheel_radius 0.033m`, `enc_counts_per_rev 3436`) は **同プロジェクト固有の小型ロボット値** であり、本件 BotWheel とは無関係。流用しないこと。

---

## 本構成 (BotWheel Explorer) への適用

> **引用元**: [ODrive 公式 ros_odrive リポジトリ](https://github.com/odriverobotics/ros_odrive) / [odrive_botwheel_explorer README](https://github.com/odriverobotics/ros_odrive/blob/main/odrive_botwheel_explorer/README.md)

**ODrive 公式が、まさに本構成 (BotWheel Explorer) 向けの ROS2 参照実装を提供している。** これが最も確実な出発点となる。

### ros_odrive パッケージ構成

| サブパッケージ | 役割 |
|----------------|------|
| `odrive_node` | CAN バス経由で ODrive と通信するスタンドアロン ROS2 ノード |
| `odrive_ros2_control` | ODrive を CAN 経由で扱う **ros2_control 統合** (公式表記: work in progress) |
| `odrive_botwheel_explorer` | `odrive_ros2_control` を使った **BotWheel Explorer の実例** |

- 対応ディストリ: **ROS2 >= Humble**
- 通信: **Linux SocketCAN** 経由 (トップレベルパラメータ `can` でインターフェース名を指定)
- command/state interface: `position` / `velocity` / `effort` (torque) を双方サポート
- ジョイントレベルパラメータ: `node_id` (ODrive の Node ID)

### odrive_botwheel_explorer の中身

公式 README より:
- 提供物: 「Hardware descriptor (URDF) files for the BotWheel Explorer」と「A launch file that allows to drive the robot around by sending `geometry_msgs/msg/TwistStamped` messages」
- 前提: 「your ODrives are already configured (with node_id 0 and 1)」 ← **本リポジトリの Node ID 左0/右1 と一致**
- `DiffDriveController` が速度コマンドインターフェースを要求 = 上記の標準スタックそのもの
- 起動: `ros2 launch odrive_botwheel_explorer botwheel_explorer.launch.py`
- トラブルシュート例: 「Failed to initialize SocketCAN on can0」 ← `can0` インターフェースが前提

> **本リポジトリの [`RaspberryPi4.md`](RaspberryPi4.md) / [`BotWheel_Explorer.md`](BotWheel_Explorer.md) の CAN 設定** (`sudo ip link set can0 up type can bitrate 250000`, Node ID 左0/右1) は、この公式 ROS2 パッケージの前提とそのまま合致する。

### 適用の要点

1. **まず `odrive_botwheel_explorer` をそのまま動かす** のが最短。URDF・launch・ros2_control 設定が一式揃っており、`can0` (250kbps)・Node ID 0/1 という本構成の前提に一致。
2. ros2_control HW I/F は **`odrive_ros2_control` (公式) を使う**。自作する場合は DiffBot の `DiffBotSystemHardware` を雛形に、`read()`/`write()` を SocketCAN 経由の ODrive コマンド (velocity 指令送信 / エンコーダから position・velocity 読出) へ置換する。
3. `wheel_radius` = 0.0855m (径171mm)、`wheel_separation` = 0.419m (トラック幅) を設定 (公式パッケージは既定値を持つ可能性が高いので確認)。

---

## Livox MID-360 と SLAM/Nav2

> **引用元**: [livox_ros_driver2 (Livox-SDK)](https://github.com/Livox-SDK/livox_ros_driver2) / [Nav2 with SLAM](https://docs.nav2.org/tutorials/docs/navigation2_with_slam.html)

### livox_ros_driver2

| 項目 | 内容 |
|------|------|
| 対応ディストリ | Foxy (20.04) / **Humble (22.04)** / **Jazzy (24.04)** |
| MID-360 対応 | ✅ 明記あり (HAP と Mid-360) |
| 出力形式 (`xfer_format`) | `0`=Livox PointCloud2 (PointXYZRTLT) / `1`=Livox CustomMsg / `2`=標準 PointCloud2 (PCL, ROS only) |
| frame_id | 既定 `livox_frame` (`msg_frame_id` で変更) |
| 依存 | **Livox-SDK2** のビルド・インストールが必須 |
| 設定 | `MID360_config.json` で `lidar_ipaddr` / `host_ip` / ポート (`cmd_data_port 56100`, `point_data_port 56300`) を指定 |

### 3D LiDAR で 2D ナビをする際の構成判断

MID-360 は 3D 点群 (PointCloud2) を出力するが、`slam_toolbox` や Nav2 のコストマップは本来 2D `LaserScan` を前提とする。主な選択肢:

| 方式 | 概要 | 向き |
|------|------|------|
| **pointcloud_to_laserscan** | 3D点群を一定高さ帯で水平スライスし 2D `LaserScan` に投影 → `slam_toolbox` (2D SLAM) | 2D平面ナビ、軽量、既存資産流用 |
| **3D SLAM (RTAB-Map / FAST-LIO 等)** | 3D点群のまま地図化・自己位置推定 | 3D地図が必要、段差/起伏のある環境 |

> 平面屋内 (本キットは IP10・屋内乾燥環境想定) であれば、`pointcloud_to_laserscan` + `slam_toolbox` が最も標準的で導入しやすい。`map→odom` を SLAM が補正し、`odom→base_link` を diff_drive_controller が出す役割分担になる。

---

## 差動二輪の運動学モデル

> **引用元**: [Mobile Robot Kinematics - control.ros.org](https://control.ros.org/rolling/doc/ros2_controllers/doc/mobile_robot_kinematics.html)

記号:
- `v` : 本体並進速度 [m/s] (cmd_vel の `linear.x`)
- `ω` : 本体角速度 [rad/s] (cmd_vel の `angular.z`)
- `r` : ホイール半径 [m] (`wheel_radius`)
- `b` : トラック幅 = 左右ホイール間距離 [m] (`wheel_separation`)
- `ω_L`, `ω_R` : 左右ホイール角速度 [rad/s]

### 逆運動学 (cmd_vel → 左右ホイール)

diff_drive_controller が内部で行う変換。各ホイールの周速度は本体速度に旋回成分を加減したもの:

```
v_L = v − ω·(b/2)        v_R = v + ω·(b/2)
ω_L = v_L / r = (v − ω·b/2) / r
ω_R = v_R / r = (v + ω·b/2) / r
```

### 順運動学 / オドメトリ (左右ホイール → 本体)

```
v = (v_R + v_L) / 2 = r·(ω_R + ω_L) / 2
ω = (v_R − v_L) / b = r·(ω_R − ω_L) / b
```

時間積分で姿勢を更新 (θ は本体方位):

```
x_{k+1} = x_k + v·cos(θ_k)·Δt
y_{k+1} = y_k + v·sin(θ_k)·Δt
θ_{k+1} = θ_k + ω·Δt
```

### エンコーダ CPR からの距離換算

エンコーダのカウントから走行距離 (= ホイール回転) を求める基本式:

```
1回転あたりの距離 = 2π·r  (ホイール円周)
カウントあたりの距離 = (2π·r) / CPR
ホイール移動距離 = Δcount × (2π·r) / CPR
```

> BotWheel は **3200 CPR**、半径 `r` = 0.0855m。`open_loop=false` では HW I/F が `read()` で取得したエンコーダ位置/速度を基に diff_drive_controller がこの計算を行う。公式 `odrive_ros2_control` では ODrive 側がエンコーダを回転量に正規化して返すため、CPR 換算はドライバ層で吸収される (実装依存のため要確認)。

---

## 本構成のパラメータ早見表

> ハードウェア値の出典: [`BotWheel_Explorer.md`](BotWheel_Explorer.md) / [`RaspberryPi4.md`](RaspberryPi4.md)

| 項目 | 値 | ROS2 上の対応 |
|------|----|--------------|
| ホイール直径 | 171mm | `wheel_radius` = **0.0855** [m] |
| トラック幅 | 419mm | `wheel_separation` = **0.419** [m] |
| エンコーダ | 3200 CPR | オドメトリ換算 (ドライバ層) |
| CAN ビットレート | 250 kbps | SocketCAN `can0` @ 250000 |
| ODrive Node ID | 左 0 / 右 1 | `node_id` (ジョイント単位) |
| CAN 接続 | Pi4 + CAN HAT (SPI) | SocketCAN `can0` |
| LiDAR | Livox MID-360 (3D) | `livox_ros_driver2`, frame `livox_frame` |
| ROS2 ディストリ | — | Humble 以上 (ros_odrive 要件) |

---

## 残課題 (要追加調査)

観点(1)標準スタック・(2)リファレンス実装・(4)運動学は公式一次情報で高信頼に裏付け済み。以下は実装着手時に対象環境で確認が必要:

1. **odrive_ros2_control の成熟度**: 公式表記が "work in progress"。velocity 制御と position/velocity フィードバックが ros2_control HW I/F として安定動作するか、対象ディストリ (Humble/Jazzy) で検証する。
2. **CPR→オドメトリ係数**: ODrive がエンコーダを回転量へ正規化する設定 (turns/counts) と、diff_drive_controller 側の `wheel_radius` の整合。
3. **Livox MID-360 のSLAM構成**: `pointcloud_to_laserscan` + `slam_toolbox` (2D) と RTAB-Map等 (3D) のトレードオフを実環境で評価。
4. **Pi4 CAN HAT の SocketCAN 安定化**: 250kbps・ODrive 2台同時通信時のバス負荷とカーネル/オーバーレイ設定 ([`RaspberryPi4.md`](RaspberryPi4.md) 参照)。
5. **cmd_vel メッセージ型**: 対象ディストリでの `Twist` / `TwistStamped` 確認 (Jazzy は TwistStamped 必須)。

---

## 主要参照リンク

| カテゴリ | リンク |
|----------|--------|
| 標準スタック | [diff_drive_controller (Jazzy)](https://control.ros.org/jazzy/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html) / [(Humble)](https://control.ros.org/humble/doc/ros2_controllers/diff_drive_controller/doc/userdoc.html) |
| デモ | [ros2_control_demos example_2 (DiffBot)](https://control.ros.org/jazzy/doc/ros2_control_demos/example_2/doc/userdoc.html) |
| 運動学 | [Mobile Robot Kinematics](https://control.ros.org/rolling/doc/ros2_controllers/doc/mobile_robot_kinematics.html) |
| Nav2 | [Setting Up Odometry](https://docs.nav2.org/setup_guides/odom/setup_odom_gz.html) / [Nav2 with SLAM](https://docs.nav2.org/tutorials/docs/navigation2_with_slam.html) |
| ODrive (本構成) | [ros_odrive](https://github.com/odriverobotics/ros_odrive) / [odrive_botwheel_explorer](https://github.com/odriverobotics/ros_odrive/blob/main/odrive_botwheel_explorer/README.md) |
| Livox | [livox_ros_driver2](https://github.com/Livox-SDK/livox_ros_driver2) |
| リファレンス実装 | [articubot_one](https://github.com/joshnewans/articubot_one) / [Andino](https://github.com/Ekumen-OS/andino) / [linorobot2](https://github.com/linorobot/linorobot2) |
