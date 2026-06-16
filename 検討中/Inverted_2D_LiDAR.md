# 逆さ・下向き傾斜 2D LiDAR による低位置障害物検出 (調査メモ)

> [!NOTE]
> 近場・低位置の障害物検出用に2D LiDARを「逆さ（上下反転）」で追加する案の検討資料。
> 世の中の取り付け手法・製品/ロボット事例・関連記事を調査してまとめたもの。**採用未確定の検討段階**。

## 目次

- [結論サマリ](#結論サマリ)
- [重要な用語の区別: 「逆さ」と「下向き傾斜」は別物](#重要な用語の区別-逆さと下向き傾斜は別物)
- [1. なぜ逆さ／下向きにするのか（技術的理由）](#1-なぜ逆さ下向きにするのか技術的理由)
- [2. 取り付け手法とソフト側の対応](#2-取り付け手法とソフト側の対応)
- [3. 検出アルゴリズム（崖・ネガティブ障害物）](#3-検出アルゴリズム崖ネガティブ障害物)
- [4. 俯角の実例](#4-俯角の実例)
- [5. ROS / ROS2 での扱い](#5-ros--ros2-での扱い)
- [6. 実ロボット・製品・プロジェクト事例](#6-実ロボット製品プロジェクト事例)
- [7. 言及している記事・フォーラム・論文](#7-言及している記事フォーラム論文)
- [8. 注意点・トレードオフ・残課題](#8-注意点トレードオフ残課題)
- [本構成 (BotWheel Explorer) への適用メモ](#本構成-botwheel-explorer-への適用メモ)

---

## 結論サマリ

2D LiDARを「逆さ（上下反転）」または「下向きに傾けて」取り付ける手法は、ロボット近傍・地面付近の低い障害物や段差・落下（崖／ネガティブ障害物）の検出を目的とした、**実務でも学術でも確立された構成**。大きく2系統に分かれる。

| 系統 | 何のため | ソフト側の論点 | 代表ソース |
|------|----------|----------------|------------|
| **(A) フラットな上下反転マウント** | 取付高さを下げる／設置上の都合 | スキャン方向の反転、tfで約π(3.14 rad)回転補正 | invert_laser, ArduPilot PRX1_ORIENT=1 |
| **(B) 下向き傾斜 (downward-tilted / push-broom)** | 地面の穴・段差・縁石・落下を直接検出、近傍死角の縮小 | 取付ジオメトリからの崖判定、costmapレイヤー統合 | MDPI Sensors 論文群, negative-obstacle-detection |

> [!IMPORTANT]
> 「近場で低位置の障害検出」が目的なら、本当に欲しいのは多くの場合 **(B) 下向き傾斜** の方。単純な上下反転(A)はセンサ高さを下げるだけで、レーザ面が水平のままなら床より上の薄い障害物しか拾えない。

---

## 重要な用語の区別: 「逆さ」と「下向き傾斜」は別物

- **逆さ (upside-down / flipped)**: センサを天地反転して取り付ける。レーザ面は（理想的には）水平のまま。主目的は**取付高さを下げる・配置の都合**。スキャン方向(時計回り↔反時計回り)が反転するためソフト補正が要る。
- **下向き傾斜 (tilted-down / push-broom)**: レーザ面を地面に向けて俯角をつける。主目的は**地面ハザード（穴・段差・崖・低い物体）の直接検出**と近傍死角の縮小。

> **引用元**: 本調査の総合所見（用語混同に注意）

---

## 1. なぜ逆さ／下向きにするのか（技術的理由）

下向き傾斜2D LiDARで地面付近の低障害物・崖（ネガティブ障害物）を検出する手法は、複数のピアレビュー論文で確立されている。技術的根拠は次の通り。

- **水平マウントでは検出できない地面上の穴や低い物体を直接検出できる**
- **近傍の死角を大幅に縮小できる**（後述の事例では俯角40°で死角 3 m → 0.21 m）
- 路面情報を多く取得でき、前方障害物をよりよく検出できる

> **引用元**:
> - [MDPI Sensors 2018, 18(6):1749](https://www.mdpi.com/1424-8220/18/6/1749) ／ ミラー [PMC6022102](https://pmc.ncbi.nlm.nih.gov/articles/PMC6022102/) — 俯角8°、SICK LMS111。「下向き2D LiDARは水平LiDARより路面情報を多く得られ前方障害物をよりよく検出できる」
> - [MDPI Sensors 2020, 20(9):2500](https://www.mdpi.com/1424-8220/20/9/2500) ／ ミラー [PMC7248764](https://pmc.ncbi.nlm.nih.gov/articles/PMC7248764/) — push-broom, UTM-30LX。「2D LiDARを下向きにする動機は、水平固定2D LiDARでは検出できない地面の穴や小物体の直接検出」
> - [PMC11679008](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11679008/) — 果樹園UGV, Livox MID-70, 俯角40°。死角 3 m → 0.21 m、地面点群密度が一桁増、検出成功率92.7%、最遠検出約9 m
> - [PMC3574724](https://pmc.ncbi.nlm.nih.gov/articles/PMC3574724/) — SICK LMS-291, 高さ2 m, わずかに俯角。前方約17 mの路面を走査し縁石を検出

---

## 2. 取り付け手法とソフト側の対応

### (A) 上下反転（フラット）マウント

2D LiDARをフラットに上下反転してマウントするのは、主に**取付高さを下げる／設置上の都合**のための実在の構成。ソフト側でスキャン方向の反転、またはtfでの回転補正が必要。

- **timkambic/invert_laser** (ROSノード): 「LiDARが物理的に上下逆さにマウントされたとき、使用前にスキャンデータを反転する必要があるためのノード」。`/scan` を購読し、反転した `/scan_inv` を配信。
- **ArduPilot** (`PRX1_ORIENT`): `0` = 車体上部マウント／`1` = 車体下部に上下逆さマウント。
- **tf補正**: `static_transform_publisher` で pitch ≈ 3.14 (π) 回転を適用して反転。例（ROS Answers 404357 の解）: `0 0 0 -0.785 3.14 0 base_link laser 100`
- **slam_karto** は `angle_increment` の符号で上下反転を自動検出。

> [!WARNING]
> 物理マウントに俯角／ロールのオフセットがあると、180°のクリーンな反転だけではレーザ面が地面と平行にならず、結果的に「傾斜配置」になる。意図的な傾斜配置(B)と区別して扱うこと。

> **引用元**:
> - [timkambic/invert_laser (GitHub)](https://github.com/timkambic/invert_laser)
> - [ArduPilot RPLidar A2 docs](https://ardupilot.org/rover/docs/common-rplidar-a2.html)
> - [ROS Answers 404357](https://answers.ros.org/question/404357/costmap-doesnt-consider-laser-beams-behind-the-robot-only-when-the-laser-frame-is-flipped-upside-down/)
> - [slam_karto issue #4](https://github.com/ros-perception/slam_karto/issues/4)

### (B) 下向き傾斜マウント

レーザ面に俯角をつけて地面に向ける。後述のアルゴリズムで崖／障害物を判定する。

---

## 3. 検出アルゴリズム（崖・ネガティブ障害物）

下向き傾斜LiDARによる崖／ネガティブ障害物検出の標準的アルゴリズム:

1. **ルックアップテーブルの事前生成**: 取付ジオメトリ（高さ・俯角・角度分解能）から、無障害の光線が地面(z=0)まで進む距離を各光線について計算しておく。
2. **しきい値判定**: 実測スキャンが基準値を一定以上超過した光線を「崖」と分類する。

点群ベースでは、隣接点間隔のジャンプ・壁面での「落下」現象・壁面での点密度増加を幾何特徴として使う。

> **引用元**:
> - [JohnTGZ/negative-obstacle-detection (GitHub)](https://github.com/JohnTGZ/negative-obstacle-detection) — C++ ROSパッケージ。物理パラメータ `lidar_height` (base_linkからの高さ)、`lidar_pitch` (y軸まわり俯角)、`lidar_resolution` (角度分解能)
> - [MDPI Sensors 2018, 18(6):1749](https://www.mdpi.com/1424-8220/18/6/1749) — 線分抽出→路面高さ・ベクトル推定→偏差で路面／障害物を分類
> - [PMC11679008](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11679008/) — 隣接点間隔のジャンプ・壁面での落下／点密度増加を特徴量に使用

---

## 4. 俯角の実例

| 俯角 | 用途 | センサ／ロボット | ソース |
|------|------|------------------|--------|
| わずか（高さ2m, 前方17m走査） | 縁石検出 | SICK LMS-291 | [PMC3574724](https://pmc.ncbi.nlm.nih.gov/articles/PMC3574724/) |
| 8° | 都市路面障害検出 | SICK LMS111 | [MDPI 18(6):1749](https://www.mdpi.com/1424-8220/18/6/1749) |
| 25° | push-broom 自己位置推定＋穴検出 | UTM-30LX (APR-03ロボット) | [MDPI 20(9):2500](https://www.mdpi.com/1424-8220/20/9/2500) |
| 40° | ネガティブ障害物検出（果樹園UGV） | Livox MID-70 | [PMC11679008](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11679008/) |

> [!NOTE]
> **トレードオフ**: 俯角を大きくすると死角は縮むが前方検出距離は短くなり、遠方点群が疎になる。25°は「1 m/s 走行で700 mm前方の障害物を停止できる」要件から逆算した値（MDPI 20(9):2500）。

---

## 5. ROS / ROS2 での扱い

傾斜LiDAR／深度センサの出力を costmap レイヤーへ統合する実装が存在する。

- **JohnTGZ/negative-obstacle-detection**:
  - 崖点を `sensor_msgs/LaserScan` (`scan_cliff`) として配信し、`cliff_layer` costmap を構築。
  - `failsafe_threshold_percentage` を超える割合の光線が `failsafe_threshold_dist` 未満ならフェイルセーフ作動。
  - `cmd_vel_safety` (`geometry_msgs/Twist`) でロボットを停止するフェイルセーフを持つ。
- **depth_nav_tools** (mdrwiega / navrobot fork):
  - `cliff_detector`: 既知のセンサ姿勢から地面より下の障害物（崖・下り階段）を検出。センサ高さと俯角の定義が必要。
  - `laserscan_kinect`: `sensor_tilt_angle` パラメータ（地面側に傾けると正値）で下向き傾斜マウントに対応。
  - ※ ただし **depth_nav_tools は深度カメラ／Kinect向けで、2D LiDAR向けではない**点に注意。

> **引用元**:
> - [JohnTGZ/negative-obstacle-detection](https://github.com/JohnTGZ/negative-obstacle-detection)
> - [mdrwiega/depth_nav_tools](https://github.com/mdrwiega/depth_nav_tools) ／ [navrobot/depth_nav_tools](https://github.com/navrobot/depth_nav_tools)
> - 関連論文: Drwiega 2017 "A Set of Depth Sensor Processing ROS Tools"

> [!NOTE]
> Nav2（ROS2）でのネイティブな崖／ネガティブ障害物レイヤー対応の現行ベストプラクティス（STVL / Spatio-Temporal Voxel Layer、keepout等）は本調査では未確認。確認できた実装は主にROS1ベース。

---

## 6. 実ロボット・製品・プロジェクト事例

| 事例 | 構成 | 備考 | URL |
|------|------|------|-----|
| **APR-03 ロボット** (研究) | push-broom 2D LiDAR (UTM-30LX, 俯角25°) | 穴・上り下り階段を衝突なく検出。自己位置推定にも使用 | [MDPI 20(9):2500](https://www.mdpi.com/1424-8220/20/9/2500) |
| **果樹園UGV** (研究) | 下向き傾斜 Livox MID-70 (俯角40°) | ネガティブ障害物検出、死角3m→0.21m | [PMC11679008](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11679008/) |
| **Phoebe TurtleBot** (オープンソース/ホビー) | Neato XV-11 レーザー | コメンターが「レーザーを逆さに付ければもっと低くできる」と提案 | [Hackaday.io](https://hackaday.io/project/161085-phoebe-turtlebot/log/153478-phoebe-chassis-2-electronics-tray) |

> [!WARNING]
> **量産ロボット製品**（掃除ロボ・配送ロボ・AMR・サービスロボの具体的な型番）で「逆さ／傾斜2D LiDAR」を採用していると**断定できる一次ソースは今回確証できなかった**。確認できたのは研究プロジェクトとオープンソース／ホビー事例のみ。

---

## 7. 言及している記事・フォーラム・論文

### フォーラム・ブログ（実務・コミュニティ）

- **ROS Discourse**: [Detect Low Obstacles using Tilted 2D Lidar [experimental]](https://discourse.openrobotics.org/t/detect-low-obstacles-using-tilted-2d-lidar-experimental/18175) — ユーザー marshalshi, 2020-12-22。「実験的。製品で使うならもっとテストを」。リンク先はMediumのブログ記事（ピアレビューなし）。
- **ROS Answers**: [costmap doesn't consider laser beams behind the robot (laser frame flipped upside down)](https://answers.ros.org/question/404357/) — tf補正(pitch≈π)の具体例。
- **ROS Answers**: [gmapping and inverted (upside down) laser](https://answers.ros.org/question/11952/gmapping-and-inverted-upside-down-laser/)
- **SICK USA Blog**: [Don't let your robot fall down stairs — negative obstacle detection using LiDAR](https://sickusablog.com/dont-let-robot-fall-stairs-negative-obstacle-detection-using-lidar-must-mobile-robots/) — 落下防止のためのネガティブ障害物検出。
- **Qiita (日本語)**: [LiDAR関連記事](https://qiita.com/srs/items/fba2c83b96d17b2680e6)

### 論文（ピアレビュー）

- [MDPI Sensors 2018, 18(6):1749](https://www.mdpi.com/1424-8220/18/6/1749) — 下向き2D LiDARによる路面・障害物検出（俯角8°）
- [MDPI Sensors 2020, 20(9):2500](https://www.mdpi.com/1424-8220/20/9/2500) — "Mobile Robot Self-Localization with 2D Push-Broom LIDAR in a 2D Map"（俯角25°）
- [PMC11679008](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11679008/) — 果樹園UGVのネガティブ障害物検出（俯角40°, Livox MID-70）
- [PMC3574724](https://pmc.ncbi.nlm.nih.gov/articles/PMC3574724/) — SICK LMS-291による縁石検出

> [!NOTE]
> MDPI本体URLは自動取得でHTTP 403を返す場合がある。確実なのはPMCミラー（[PMC6022102](https://pmc.ncbi.nlm.nih.gov/articles/PMC6022102/) = MDPI 18(6):1749, [PMC7248764](https://pmc.ncbi.nlm.nih.gov/articles/PMC7248764/) = MDPI 20(9):2500）。

---

## 8. 注意点・トレードオフ・残課題

### 注意点

1. **用語混同**: 「逆さ(反転)」と「下向き傾斜」は別物（[冒頭参照](#重要な用語の区別-逆さと下向き傾斜は別物)）。
2. **センサ種別の不一致**: 最も具体的な数値（死角3m→0.21m, 検出9m, 92.7%）を出すPMC11679008は**3D ソリッドステートLiDAR (Livox MID-70)** であり、2Dスキャナ(RPLIDAR/SICK TIM/Hokuyo URG)ではない。死角縮小の原理は2Dにも転用できるが、数値はそのまま当てはまらない。depth_nav_tools も深度カメラ向け。
3. **ソース品質のばらつき**: 学術根拠(MDPI/PMC)は強い。実装側(negative-obstacle-detection, invert_laser)は個人GitHubプロジェクトで採用実績は不明。Phoebe/ROS Discourse はブログ／フォーラム品質で実験的。

### トレードオフ

下向き傾斜は近傍・地面ハザードに強い一方、**遠方・背の高い前方障害物の検出距離と上方FOVを犠牲にする**。実運用では**水平＋傾斜の2台構成**や**3D LiDARとの併用**が一般的（US Patent 11607804, MDPI 20(9):2500 が言及）。

### 残課題（要追加調査）

- 量産ロボット製品で逆さ／傾斜2D LiDAR採用を一次資料で確認できる具体的型番はあるか（今回確証できず）。
- Nav2(ROS2)でのネイティブな崖／ネガティブ障害物レイヤーの現行ベストプラクティス。
- RPLIDAR/SICK TIM/Hokuyo URG など実2Dスキャナを傾斜配置した場合の最適俯角・最小検出距離・歩行速度別の段差検出可否を定量化した2D専用ベンチマーク。
- 傾斜マウントによる床面の鏡面反射・低反射率床での欠測やゴースト点の影響と、laser_filters 等での実務的フィルタ設定。

---

## 本構成 (BotWheel Explorer) への適用メモ

- 既に主センサとして [Livox MID-360](../Livox_MID360.md)（3D LiDAR, 垂直FOV -7°〜+52°）を搭載予定。MID-360は垂直方向に下も見えるが、近傍・直下の死角は残るため、**低位置・近接専用の補助2D LiDARを下向き傾斜で追加**する案は理にかなう。
- 2D LiDAR追加時の検討項目:
  - **俯角**: ロボット速度と停止距離から逆算（参考: 1 m/s で 25° 程度）。本機の最高速度・制動性能に合わせて再計算が必要。
  - **取付高さ・前方オフセット**: 近傍死角を最小化しつつ、必要な前方検出距離を確保する妥協点。
  - **ソフト**: ROS2なら傾斜スキャンを costmap の obstacle/cliff レイヤーへ統合。崖判定はルックアップテーブル方式（negative-obstacle-detection 相当）を移植 or 自作。
  - **電源**: MID-360同様に電源系（[DCDC](../DCDC_Converter.md)）への追加負荷を確認。
- 「逆さ(フラット反転)」だけだと低位置の薄い障害物しか拾えないため、**目的が近接・低位置・段差検出なら下向き傾斜を推奨**。
