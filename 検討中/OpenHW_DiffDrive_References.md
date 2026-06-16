# オープンハードウェア 差動二輪 リファレンス集 (10〜50kgクラス)

ODrive BotWheel Explorer (車体約20kg・最大積載100kg・差動二輪) と同クラスの、オープンハードウェアな差動二輪移動ロボットの参照プロジェクトをまとめる。設計・モータ選定・ROS2スタックの参考対象として整理した。

ソフトウェアスタック (ros2_control / Nav2 / 運動学) の詳細は [`ROS2_DiffDrive_Reference.md`](ROS2_DiffDrive_Reference.md) を参照。

---

## 目次

1. [結論サマリ](#結論サマリ)
2. [候補一覧 (比較表)](#候補一覧-比較表)
3. [BotWheel Explorer 自体 (基準点)](#botwheel-explorer-自体-基準点)
4. [ホバーボードハブモータ系 (重量・積載クラス最一致)](#ホバーボードハブモータ系-重量積載クラス最一致)
5. [ROS2 ソフトスタック参照 (Linorobot2)](#ros2-ソフトスタック参照-linorobot2)
6. [参考: 規模感が外れるが設計の作法が参考になるもの](#参考-規模感が外れるが設計の作法が参考になるもの)
7. [重要な注意点・限界](#重要な注意点限界)
8. [残課題 (要追加調査)](#残課題-要追加調査)

---

## 結論サマリ

- **重量が明示的に10〜50kgクラスと確認できたのは BotWheel Explorer (20kg) のみ。** 他は重量の一次情報がなく、モータ出力・積載・部品構成からの推定。
- **重量・積載クラスが最も近い自作系は「ホバーボードの350W BLDCハブモータ流用」の作例** — Robaka / Robaka v2、MORPH。中型差動二輪を安く組む際の有力な参考。
- **ROS2 ソフトスタックの参照は Linorobot2** (Apache-2.0、2WD=差動、Nav2/SLAM/EKF統合済み)。ただしハードCADの公開は限定的。
- **BotWheel Explorer は ODrive 公式の `ros_odrive` がそのまま参照実装** になるが、ODrive S1 のファームは非公開 (NDA) で「完全オープンハードウェア」ではない点が本質的制約。

---

## 候補一覧 (比較表)

| プロジェクト | 駆動 / モータ / コントローラ | 規模感 (重量/積載/ホイール) | オープン度 | ソフトスタック | 本構成への参考度 |
|--------------|------------------------------|------------------------------|------------|----------------|------------------|
| **BotWheel Explorer** | 差動二輪 / ODrive Botwheel ハブ / ODrive S1×2 (CAN) | 20kg / 100kg / 171mm | URDF・ros2_control公開、**S1ファームは非公開(NDA)** | ROS2 `ros_odrive`, DiffDriveController | ★基準。直接の手本 |
| **Robaka / Robaka v2** | 差動二輪 / 350W ホバーボードハブ×2 | 重量不明 (推定中型) | ハードのオープン度は不確実 | ROS1 `ros_control` + hoverboard-driver (Bipropellantファーム), Jetson Nano+STM32 | ハブモータ流用の作法 |
| **MORPH** | 差動二輪 / 350W ホバーボードハブ×2 / **VESC×2** | 積載 約100kg (設計目標・未検証) | Hackaday/GitHub公開 | ROS1 (Indigo/Kinetic) `vesc_driver` | VESC採用の中型作例 |
| **Linorobot2** | 2WD(差動)/4WD/Mecanum / マイコン+micro-ROS | 規模感の数値は未確定 | Apache-2.0 (ソフト主体) | **ROS2** Nav2+SLAM Toolbox+robot_localization EKF | ★ROS2スタック参照 |
| **Andino** | 差動二輪 / DG01D-E ホビーギヤモータ+L298N | **<10kg (TurtleBotクラス)** | 完全オープン (BSD-3) hardware/firmware/CAD | ROS2 Humble/Jazzy, diff_drive_controller | 設計作法のみ(規模感外) |

---

## BotWheel Explorer 自体 (基準点)

> **引用元**: [BotWheel Explorer - ODrive Shop](https://shop.odriverobotics.com/products/botwheel-explorer) / [BotWheel - ODrive Shop](https://shop.odriverobotics.com/products/botwheels) / [ros_odrive (GitHub)](https://github.com/odriverobotics/ros_odrive)

本リポジトリの対象機そのものが、10〜50kgクラスの差動二輪リファレンスの基準点になる。

| 項目 | 値 |
|------|----|
| 駆動方式 | 差動二輪 (ODrive Botwheel ハブモータ×2 + キャスター) |
| 車体重量 | 20kg |
| 寸法 | 0.45 × 0.5 × 0.175 m |
| 最大積載 | 100kg (推奨) |
| ホイール径 | 171mm (単体2.2kg、80kg/wheel定格) |
| モータ | 24V公称、連続5A/70W、5Nm、24Vで110rpm、3200CPR、IP54 |
| コントローラ | ODrive S1 ×2 (CAN, node_id 0/1) |

- ROS2参照実装: `odrive_botwheel_explorer` (URDF + ros2_control + DiffDriveController、dual ODrive over SocketCAN `can0`)。
- **オープン度の限界**: ros_odrive (URDF/ros2_control統合) はオープンだが、**ODrive S1 のファームウェアソースは非公開** (オープンなのはレガシー ODrive v3.x のみ、S1はNDA下)。

> 詳細スペックは [`BotWheel_Explorer.md`](BotWheel_Explorer.md)、CAN設定は [`RaspberryPi4.md`](RaspberryPi4.md) を参照。

---

## ホバーボードハブモータ系 (重量・積載クラス最一致)

ホバーボードの 350W BLDC ハブモータを左右に流用する手法は、**重量・積載がこのクラス (中型) に最も合致しやすい** 定番アプローチ。BotWheel と同じ「ハブモータ直駆動の差動二輪」という機構思想を、より安価に再現できる。

### Robaka / Robaka v2

> **引用元**: [Converting a hoverboard into a ROS robot (Medium)](https://medium.com/@alxm/converting-a-hoverboard-into-a-self-driving-mobile-robot-with-ros-d886c867e8a9) / [robaka-ros (GitHub)](https://github.com/alex-makarov/robaka-ros) / [hoverboard-driver (GitHub)](https://github.com/alex-makarov/hoverboard-driver)

| 項目 | 内容 |
|------|------|
| 駆動 | 差動二輪、350W モータホイール×2 (独立駆動ハブ輪) |
| 制御 | `ros_control` + 専用 hoverboard-driver (Bipropellant カスタムファーム) |
| 計算機 | Jetson Nano + STM32F103 |
| 参考点 | ホバーボードモータを ROS の `diff_drive_controller` に載せる実例 |

> **注意**: 「100kg積載・15km/h」というクラス主張は本調査で **反証され除外**。また Robaka のハードウェア (CAD等) のオープン度は不確実 (公開範囲が限定的)。あくまでソフト/手法の参考。

### MORPH (Modular Open Robotics Platform)

> **引用元**: [MORPH - Hackaday.io](https://hackaday.io/project/25730-morph-modular-open-robotics-platform-for-hackers) / [morph (GitHub)](https://github.com/roaldlemmens/morph)

| 項目 | 内容 |
|------|------|
| 駆動 | 差動二輪、350W BLDC ハブモータ×2 (ホバーボード流用) |
| 制御 | **VESC ×2** (オープンソースESC) + AS5047 磁気エンコーダ |
| 積載 | 約100kg (設計目標、**未検証**) |
| ソフト | ROS1 (Indigo/Kinetic) `vesc_driver` (MIT-Racecar) |
| 参考点 | **ODrive 以外 (VESC) でこのクラスを組む** 代表例。エンコーダ追加の構成も参考に |

---

## ROS2 ソフトスタック参照 (Linorobot2)

> **引用元**: [linorobot2 (GitHub)](https://github.com/linorobot/linorobot2) / [linorobot/kinematics (GitHub)](https://github.com/linorobot/kinematics)

ハード規模よりも **ROS2 自律移動スタックの完成形** として参考になる。BotWheel Explorer が目指す ROS2/Nav2/SLAM 構成に直接合致。

| 項目 | 内容 |
|------|------|
| 駆動方式 | 2WD (=差動)、4WD、Mecanum に対応 |
| ライセンス | Apache-2.0 |
| ソフト | Nav2 + SLAM Toolbox + robot_localization EKF が事前統合済 (ekf.yaml 等あり) |
| アーキ | マイコンファーム + micro-ROS でオドメトリ/IMUをエッジ算出 (ros2_control を使わない別系統) |

> 規模感 (車体重量・寸法) の数値は未確定。ハードCADの完全公開は Apache-2.0 だけでは担保されない点に注意。**「ソフトの参考はLinorobot2、ハード機構の参考はホバーボード系/BotWheel」** と役割分担で見るのがよい。

---

## 参考: 規模感が外れるが設計の作法が参考になるもの

### Andino (Ekumen-OS)

> **引用元**: [andino (GitHub)](https://github.com/Ekumen-OS/andino)

完全オープンソース (BSD-3-Clause) の差動二輪ROS2機で、hardware/firmware/SLAM/Nav2 を一式GitHub公開。`diff_drive_controller` 使用、Humble/Jazzy対応。**ただし DG01D-E ホビーギヤモータ + L298N + Arduino Nano + Pi4B + 3Dプリント筐体で、明確に TurtleBot クラス (<10kg, <USD300)**。規模感は本要件 (10〜50kg) から外れる。

→ **「完全オープンな差動二輪ROS2機の設計作法・ディレクトリ構成」の手本** としては優秀 (本構成のソフト構造の参考)。重量クラスの参考にはならない。

### 汎用ホバーボード差動駆動ドライバ (再利用部品)

> **引用元**: [hoverboard-driver (GitHub)](https://github.com/hoverboard-robotics/hoverboard-driver) / [hoverboard_ros2_control (DataBot-Labs)](https://github.com/DataBot-Labs/hoverboard_ros2_control)

ホバーボードモータを採用する場合の制御基盤として再利用できる:

| ドライバ | 特徴 |
|----------|------|
| `hoverboard-driver` | MIT、UART/serial制御、ROS `diff_drive_controller` 統合、Feruファーム改、odometryをserial報告 |
| `hoverboard_ros2_control` | **ros2_control ハードウェアIF実装**、jazzy/humble/foxy対応、FOCファーム |

> BotWheel (ODrive CAN) とは別系統だが、ホバーボードモータを選ぶなら `hoverboard_ros2_control` が ros2_control 標準スタックに直接載る。

---

## 重要な注意点・限界

1. **重量数値の裏付けが弱い**: 10〜50kg を数値で確認できたのは BotWheel Explorer のみ。Robaka/MORPH/Linorobot2 は実測重量の一次情報がなく推定。MORPH の「約100kg」は積載の設計目標値であり車体重量ではない。
2. **ODrive S1 はファーム非公開 (NDA)**: BotWheel Explorer は ros2_control 層こそオープンだが、厳密には「完全オープンハードウェア」ではない。オープン度を最重視するなら VESC 系 (MORPH) が有利。
3. **ROS バージョン**: Robaka/MORPH 系は **ROS1ベース** が多く、ROS2移行が別途必要。ROS2ネイティブなのは Linorobot2、Andino、`hoverboard_ros2_control`、ODrive `ros_odrive`。
4. **ros_odrive の ros2_control 統合は "Work In Progress"** 段階で今後変わり得る。
5. **役割分担で見る**: ハード機構=BotWheel/ホバーボード系、ROS2ソフト=Linorobot2/Andino、と分けて参照するのが現実的。

---

## 残課題 (要追加調査)

1. Robaka v2 / MORPH / Linorobot2 対応機の **実車体重量・寸法・積載の一次情報 (数値)**。10〜50kg適合の確定には実測値が必要。
2. 350W級ハブモータ差動二輪で、**ROS2+ros2_control+Nav2 を完全統合し、かつ CAD/BOM/回路図まで公開** した中型機の他の作例 (VESC/ODrive採用の網羅)。
3. **電動車椅子ベース / Open-source AGV** (大学・企業公開の差動二輪台車) でこのクラスかつ設計入手可能なもの (今回の確証付きクレームでは具体例が拾えず。候補ソースとして openAMRobot, 自律車椅子系の論文・リポジトリは存在)。
4. **ODrive S1 以外で S1相当の中型ハブモータ駆動を完全オープン (CERN-OHL等) で実現**したモータコントローラ+ロボット統合事例。

---

## 主要参照リンク

| カテゴリ | リンク |
|----------|--------|
| 基準機 | [BotWheel Explorer](https://shop.odriverobotics.com/products/botwheel-explorer) / [Botwheel単体](https://shop.odriverobotics.com/products/botwheels) / [ros_odrive](https://github.com/odriverobotics/ros_odrive) / [ODrive firmware (v3.x のみオープン)](https://github.com/odriverobotics/ODrive) |
| ホバーボード系 | [Robaka (Medium)](https://medium.com/@alxm/converting-a-hoverboard-into-a-self-driving-mobile-robot-with-ros-d886c867e8a9) / [robaka-ros](https://github.com/alex-makarov/robaka-ros) / [MORPH (Hackaday)](https://hackaday.io/project/25730-morph-modular-open-robotics-platform-for-hackers) / [morph (GitHub)](https://github.com/roaldlemmens/morph) |
| ホバーボードドライバ | [hoverboard-driver](https://github.com/hoverboard-robotics/hoverboard-driver) / [hoverboard_ros2_control](https://github.com/DataBot-Labs/hoverboard_ros2_control) |
| ROS2スタック | [linorobot2](https://github.com/linorobot/linorobot2) / [andino](https://github.com/Ekumen-OS/andino) |
