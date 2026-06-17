# 全天球カメラ検討メモ

調査日: 2026-06-17 (JST)

目的: ROS2ロボットで周囲映像を取得し、将来的にLiDAR点群へ色を付ける用途を想定して、全天球/360度カメラの候補、価格、ROS2適性、スペック、評判を整理する。

## 結論

ロボット実装のしやすさを最優先するなら、第一候補は **Insta360 X3/X4**、次点が **RICOH THETA V/Z1/X**。  
Insta360はROS2 Humbleで動作実績のある `ai4ce/insta360_ros_driver` があり、X2/X3で検証済み、X4も別リポジトリでwebcam mode + `camera_ros` の事例がある。RICOH THETAはROS/ROS2事例が多く、APIやLinuxライブ配信情報も多いが、機種やファームウェアによって `libuvc` / `gstreamer` / PTP 周りの癖が出やすい。

LiDAR色付き点群が目的なら、写真品質だけでなく「連続給電」「熱停止しにくさ」「equirectangular画像をROS2 topicとして安定取得できること」「タイムスタンプ同期」「外部キャリブレーション」が重要。動きながら色付けする場合、ローリングシャッターの歪みが問題になりやすいので、最初は停止撮影または低速移動で検証するのが現実的。

## 推奨候補

| 優先 | 機種 | 理由 | 注意 |
| --- | --- | --- | --- |
| 1 | Insta360 X3 | 中古/新品が安い。ROS2 HumbleドライバでX2/X3検証済み。5.7K 360動画、72MP静止画。 | 旧機種。暗所・細部はX5/X4/Osmo 360に劣る。 |
| 2 | Insta360 X4 | 8K 360動画、国内新品がX5より安い。webcam modeからROS2へ入れる事例あり。 | `ai4ce` ドライバではX4 issueがあり、X3ほど枯れていない。 |
| 3 | RICOH THETA V | ROS/ROS2事例が多く、THETA API/ライブ配信情報が豊富。中古で安い。 | 販売終了。4K世代で画質は最新8K機に劣る。Linux設定に癖あり。 |
| 4 | RICOH THETA Z1 | 1型センサーx2、RAW対応で静止画/暗所が強い。LiDAR色付け用の静止パノラマに向く。 | 新品/中古とも高め。動画は4Kで最新機より弱い。 |
| 5 | DJI Osmo 360 | 8K50、120MP、内蔵ストレージ、DJIマイク連携。画質/価格のバランスが良い。 | ROS2事例は少ない。SDK/USBライブ取得経路の確認が必要。 |

## 価格メモ

価格は調査時点の表示価格・出品例。中古は状態/付属品/保証で大きく変動する。

為替目安: 1 USD ~= 160 JPY。国内価格が取れるものは国内円価格を優先。

| 機種 | 新品価格の目安 | 中古価格/相場メモ | 価格ソース |
| --- | ---: | ---: | --- |
| RICOH THETA X | 86,900-109,800円 | 買取上限 40,100円、実売中古は概ね5-8万円台想定 | 価格.com 86,900円、RICOH360 Store 109,800円、リファン買取 40,100円 |
| RICOH THETA Z1 51GB | 132,800円、EU 999.99EUR | Yahoo!オークション例 69,800-82,800円、買取 35,100円 | RICOH360 Store、Yahoo!オークション、リファン |
| RICOH THETA V | 販売終了 | キタムラ中古 35,900円から、Yahoo!例 29,800-33,048円 | キタムラ、Yahoo!オークション |
| RICOH THETA SC2 | 販売終了/在庫限り。米国 $339.99例 | 買取上限 14,000円程度 | Amazon US、ネット中古買取 |
| RICOH360 THETA A1 | EU/海外中心。価格は地域差あり、概ね800-900EUR級 | まだ中古少ない | RICOH発表、RICOH EU |
| Insta360 X5 | 国内最安 74,800円、米国 $549.99から | Yahoo!フリマ例 67,999-78,000円 | 価格.com、Insta360、Yahoo!フリマ |
| Insta360 X4 | 国内最安 45,866-46,111円付近 | Price Rank中古 39,800円、Yahoo!フリマ例 42,800円 | 価格.com、Price Rank、Yahoo!フリマ |
| Insta360 X3 | 公式 $299.99、国内セール30,210円例 | Yahoo!オークション例 25,000-28,000円、買取 17,500円 | Insta360、価格.com口コミ、Yahoo!オークション、リファン |
| Insta360 X4 Air | $399.99 | 新しめで中古少ない | TechRadar、Insta360 |
| Insta360 ONE RS 1-Inch 360 | 118,800円 / $799.99 | 中古は少なめ。Amazon US $1,199表示例もあり価格差大 | Insta360 Store、Amazon |
| DJI Osmo 360 Standard Combo | 国内最安 45,000円、海外 479.99EUR級 | Yahoo!オークション未使用例 71,030-72,800円 | 価格.com、Amazon JP、Yahoo!オークション、CineD |
| GoPro MAX2 | 国内 79,800円、米国 $499.99級 | 新しめで中古少ない | キタムラ、GoPro、TechRadar |
| GoPro MAX | Amazon US $439例 | 旧機種。セール/中古で安い | Amazon US、TechRadar |
| Kandao QooCam 3 Ultra | B&H $479、国内楽天 106,527円例 | B&H used $392.50 | B&H、楽天 |
| Labpano PilotPano | $479 | eBay新品例 $299.99 | Panox store、eBay |
| Labpano Pilot One EE | $1,529.15-1,784.15 | 中古少ない | Panox store |
| Trisio Lite 2 | 新品は3-5万円台相当の海外出品が多い | eBay中古 KRW 313,588程度 | eBay、Pergear |
| XPhase Pro S2/X2 | $979級 | 中古少ない | Panoraven、Stabilizer-pro |

## 主な候補一覧とスペック比較

| 機種 | センサー | 静止画 | 360動画 | ライブ/USB取得 | 防水/耐候 | 重量 | ロボット用途評価 |
| --- | --- | ---: | ---: | --- | --- | ---: | --- |
| RICOH THETA X | 1/2型 x2 | 11K 60MP | 5.7K/30, 4K/60 | USB live、Web API、プラグイン | 明確な防水なし | 約170g | 交換バッテリ/microSD/GPS/画面あり。ROSはTHETA系資産を流用しやすい。 |
| RICOH THETA Z1 | 1型 x2 | 23MP RAW/DNG | 4K/29.97 | USB live、Web API、プラグイン | 明確な防水なし | 約182g | 静止画色付け・暗所に強い。動画解像度は古い。 |
| RICOH THETA V | 1/2.3型級 x2 | 14MP級 | 4K/29.97 | USB live実績豊富 | 明確な防水なし | 約121g | ROS/ROS2実例が多い。安く試すには良い。 |
| RICOH360 THETA A1 | 1/2型 x2 | 60MP | 8K、4K/2K live | Web/API系想定 | 防水/防塵/耐温度 | 未確認 | 建設/点検向け。堅牢だがROS2実例はまだ少ない。 |
| Insta360 X5 | 1/1.28型 x2 | 72MP級 | 8K/30, 5.7K/60 | Insta360 SDK、webcam/USB経路要確認 | 15m防水、交換レンズ | 約200g級 | 画質/暗所/耐久は強い。ROS2はX3/X4ほど事例確認が必要。 |
| Insta360 X4 | 1/2型級 x2 | 72MP | 8K/30, 5.7K/60 | ROS2事例あり、webcam mode | 10m防水 | 約203g | 価格と性能のバランス良。X4固有のROS設定確認が必要。 |
| Insta360 X3 | 1/2型 x2 | 72MP | 5.7K/30 | ROS2 Humbleドライバ検証済み | 10m防水 | 約180g | ROS2導入の第一候補。新品/中古とも安い。 |
| Insta360 ONE RS 1-Inch 360 | 1型 x2 | 21MP | 6K | SDKあり | 防滴程度 | 約239g | 暗所・画質は良いが高価でロボット実装例は少なめ。 |
| DJI Osmo 360 | 1/1.1型級 x2 | 120MP | 8K/50, 8K/30 100分 | USB/SDK要確認 | IP68/10m | 183g | ハードは強い。ROS2資産は薄い。 |
| GoPro MAX2 | 未確認 | 29MP | True 8K/30, 5.6K/60 | webcam/SDK要確認 | 5m防水、交換レンズ | 未確認 | rugged、GPS/Log/timecode系が魅力。ROS2事例は薄い。 |
| GoPro MAX | 小型 x2 | 16.6MP | 5.6K/30 | webcam/HDMI経路要確認 | 5m防水 | 約154g | 旧機種。安ければ実験用。 |
| Kandao QooCam 3 Ultra | 1/1.7型 x2 | 96MP | 8K/30, 5.7K/60, 4K/120 | USB/SDK要確認 | IPX8 | 約336g | 画質/低照度は強いが重い。ROS2事例は薄い。 |
| Labpano PilotPano | 未確認 | 未確認 | 5.7K/30、4K live | Android/Pilot API | 未確認 | 295g | Android/Open APIで業務用途向け。ROS2直接実例は薄い。 |
| Labpano Pilot One EE | Sonyセンサー x4 | 8K | 8K/24 | Android/Pilot API | IP65 | 未確認 | 4眼で画質・ライブ配信寄り。高価。 |
| Trisio Lite 2 | 1/2.3型単眼回転 | 8K 32MP | 動画向きではない | Wi-Fi/USB | なし | 150g | 静止バーチャルツアー用。移動ロボット動画には不向き。 |
| XPhase Pro S2/X2 | 多眼 | 134MP/200MP級 | なし | 独自 | なし | 248g級 | 最高級静止画向け。ロボット常時映像には不向き。 |

## ROS2/ROS ドライバ一覧

GitHubのスター数・最終更新日 (`pushed_at`) は調査日 2026-06-17 時点でGitHub APIから取得した値。スター数・更新日は時間とともに変化する点に注意。「ROS対応」はリポジトリのブランチ構成・READMEの記載に基づく。

| リポジトリ | 対応カメラ | ROS対応 (distro) | ★ | 最終更新 | ライセンス | 備考 |
| --- | --- | --- | ---: | --- | --- | --- |
| [ai4ce/insta360_ros_driver](https://github.com/ai4ce/insta360_ros_driver) | Insta360 X2/X3 (X4は[issueあり](https://github.com/ai4ce/insta360_ros_driver/issues/13)) | ROS2 Humble (Ubuntu 22.04)、Noetic、ros2 各ブランチ | 246 | 2026-06-03 | Apache-2.0 | 360ドライバで最もスターが多く更新も活発。dual-lensモード+USB=Android設定が必須。Insta360 SDK (2025-04-23以降) を別途申請。dual fisheye → equirectangular/rectilinear変換とIMU処理を内蔵。 |
| [hzlbbfrog/insta360_ros2](https://github.com/hzlbbfrog/insta360_ros2) | Insta360 各種 | ROS2 (main) | 3 | 2024-12-24 | Apache-2.0 | 別系統のInsta360 ROS2ドライバ。小規模。 |
| [RobotiXX/insta360_camera_ros](https://github.com/RobotiXX/insta360_camera_ros) | Insta360 X4 | ROS2 (webcam mode + `camera_ros`) | 3 | 2025-06-18 | MIT | X4をwebcam modeで `camera_ros` 経由でROS2に入れる構成例。 |
| [stella-cv/theta_driver](https://github.com/stella-cv/theta_driver) | RICOH THETA V/Z1 | ROS / ROS2 Foxy (`ros`/`ros2` ブランチ) | 26 | 2023-09-03 | MIT | THETA系ROS2ドライバでスター最多。`libuvc-theta` 依存。Docker対応。Stella VSLAM系の資産。 |
| [madjxatw/ricoh_theta_ros](https://github.com/madjxatw/ricoh_theta_ros) | RICOH THETA V/Z1 | **ROS1** (catkin) | 17 | 2023-04-24 | - | ROS1 (catkin) パッケージ。`libuvc-theta`/`v4l2loopback`/`Equirec2Perspec`/`libptp` をsubmodule同梱。ROS2化には移植が必要。 |
| [hijimasa/ros2_theta_cam](https://github.com/hijimasa/ros2_theta_cam) | RICOH THETA V | ROS2 (READMEにdistro明記なし) | 5 | 2025-10-20 | Apache-2.0 | THETA系で比較的新しい更新。`gstthetauvc`/`libuvc` (nickel110 fork) 依存。2K/4K切替・シリアル指定対応。 |
| [itsuka-to/ros2_thetav](https://github.com/itsuka-to/ros2_thetav) | RICOH THETA V | ROS2 Dashing (Ubuntu 18.04)、Humbleブランチあり | 5 | 2022-11-14 | - | 非公式。GStreamer + `libuvc-theta` 依存。Live-Streaming-Mode必須。 |
| [leo-drive/color-point-cloud](https://github.com/leo-drive/color-point-cloud) | (全天球専用ではない) | ROS2 (main) | 82 | 2024-01-15 | - | 点群+複数カメラ画像から色付き点群を生成するツール。色付け処理の参考実装。 |

> **補足**: `madjxatw/ricoh_theta_ros` のみROS1 (catkin) で、他はROS2。THETA系はいずれも `libuvc-theta` 系の修正libuvc/GStreamer/v4l2loopbackが絡み、Insta360系よりLinuxセットアップの手間が増えやすい。

## ROS2でよく使われる/扱いやすい機種

### Insta360 X2/X3/X4系

- `ai4ce/insta360_ros_driver` はROS2 Humble / Ubuntu 22.04でテストされ、Insta360 X2/X3で検証済み。出力解像度は 3840x1920、2560x1280、2304x1152、1920x960 の30fpsが記載されている。
- GitHub topics上でもスター数が多く、2026-06更新の形跡があるため、360カメラのROS2実装としては比較的新しい。
- X4は互換性issueが出ている一方、`RobotiXX/insta360_camera_ros` はX4のwebcam modeを `camera_ros` でROS2に入れる構成を示している。
- 扱いやすい点: equirectangularに近い横2:縦1の画像をROS2 `sensor_msgs/Image` として流しやすい。一般的なOpenCV/cv_bridgeパイプラインに乗せやすい。
- 注意点: Insta360 SDKは申請/利用条件の確認が必要。最新X5/X4 AirはSDK対応機種に入るが、ROS2既存ドライバでそのまま動くかは別問題。

### RICOH THETA V/Z1/X系

- `hijimasa/ros2_theta_cam` はTHETAの画像をROS2 topicとしてpublishするパッケージ。`gstthetauvc`、`libuvc` などが必要。
- `itsuka-to/ros2_thetav` はUbuntu 22.04 / ROS2 HumbleでTHETA Vの画像topicをpublishする非公式パッケージ。
- RICOH THETA VをKR260 + ROS2 + RViz2でライブ配信/YOLO/3D marker化した事例があり、THETA VはAPIやライブラリが豊富で扱いやすいと述べられている。
- THETA V/Z1向けROS1ドライバやOpenVSLAM/Stella VSLAM事例が多い。ROS2へ移植または画像topicだけROS2化する選択肢がある。
- 扱いやすい点: THETA Web API、USB live streaming、プラグイン機構、コミュニティ情報が多い。Z1/Xは公式アプリ/転送/スティッチャーも整備されている。
- 注意点: LinuxでTHETA V/Z1を安定ライブ取得するには、patched `libuvc`、`v4l2loopback`、GStreamerなどが絡む場合がある。セットアップはInsta360のROS2ドライバより手間になる可能性がある。

### その他の機種

- DJI Osmo 360、GoPro MAX2、QooCam 3 Ultraはハード性能は高いが、ROS2の具体的な既存ドライバ/実例は少ない。USB webcam/UVCとして見えるか、SDKでライブフレームを取れるかを購入前に確認したい。
- Labpano系はAndroidベース/Open APIで業務用途には魅力があるが、重く高価で、ROS2ロボットでの既存例は少ない。
- Trisio/XPhaseは静止画バーチャルツアー向け。移動ロボットのリアルタイム視覚には不向き。

## LiDAR色付き点群への適性

色付き点群の基本処理は、LiDAR点群とカメラ画像を時刻同期し、外部パラメータ(カメラ-LiDAR間の姿勢)とカメラモデルを使って各点を画像上へ投影し、RGBを付与する流れ。

全天球カメラの場合は通常のピンホールカメラではなく、equirectangular画像または魚眼レンズモデルを扱う。`image_geometry` 前提の単純なピンホール投影だけでは足りないため、以下が必要。

- カメラ-LiDAR外部キャリブレーション: 固定マウントで剛体化し、TFを安定させる。
- 全天球投影モデル: 3D方向ベクトルから equirectangular の `(u, v)` へ変換する処理。
- 時刻同期: ROS2 header timestamp、可能なら同一PCでの取り込み、NTP/PTP、または低速/停止撮影。
- 露出固定: 自動露出がフレームごとに変わると点群色がちらつく。
- ローリングシャッター対策: 移動しながら撮ると歪みが出る。THETA VでLiDAR色付けをした事例では停止撮影が推奨されている。

関連実装として `leo-drive/color-point-cloud` はROS2で点群と複数カメラ画像から点群を色付けするツール。全天球専用ではないが、ROS2上の色付け処理の参考になる。研究面では OmniColor が独立した360度カメラとLiDAR点群を用いた色付け/姿勢最適化を扱っている。

## 評判・レビュー要約

### RICOH THETA Z1

- 良い点: 1型センサーx2、RAW/DNG対応、静止画・暗所・ダイナミックレンジが強い。バーチャルツアーや静止360写真では今でも評価が高い。
- 悪い点: 動画は4K止まりで、最新8K機より細部が弱い。価格が高い。防水/堅牢用途では追加保護が必要。
- ロボット視点: 低速/停止で高品質な色付き点群を作るなら有力。リアルタイム周囲認識用途ではコストに見合うか要検討。

### RICOH THETA X

- 良い点: 11K/60MP静止画、5.7K動画、タッチ画面、交換バッテリ、microSD、GPS。スマホなしで現場運用しやすい。
- 悪い点: バッテリ・熱・車載時の安定性についてユーザー報告がある。センサーはZ1より小さいため暗所画質はZ1に劣る。
- ロボット視点: 長時間運用の仕組みはZ1より作りやすい。ROS2実装はTHETA系資産を使える可能性が高いが、X専用の動作確認が必要。

### RICOH360 THETA A1

- 良い点: 建設/点検/保険など業務用途向け。防水・防塵・耐温度、長時間ミッション、H.265や低ビットレート記録、4K/2Kライブ配信が売り。
- 悪い点: 新しいため中古/レビュー/ROS2事例が少ない。8K動画はフレームレート制約がある情報あり。
- ロボット視点: 屋外・粉塵・雨・長時間の現場ロボットには魅力。開発リスクは高い。

### Insta360 X5

- 良い点: 8K/30、1/1.28型x2、暗所向けPureVideo、交換レンズ、15m防水。TechRadarなどで高評価。
- 悪い点: 8Kでは発熱/電池消費が増える。X4からの買い替え価値は用途次第。ROS2実績はX3/X4ほど確認できていない。
- ロボット視点: 画質・堅牢性の第一候補だが、まずX3/X4でROS2パイプラインを固めてから移行するのが堅い。

### Insta360 X4

- 良い点: 8K/30、5.7K/60、135分級バッテリ、アプリ/Studioが強い。明るい環境の動画が高評価。
- 悪い点: 低照度はX5/Osmo/1型機に劣る。8K時は熱を持つ。レンズガードや突出レンズの取り扱い注意。
- ロボット視点: 国内価格が落ちていて、性能/ROS2実験/入手性のバランスが良い。

### Insta360 X3

- 良い点: 安価、流通量が多い、5.7K 360動画、72MP静止画、防水。ROS2ドライバ検証済み。
- 悪い点: 8Kではない。暗所/細部は最新機に劣る。
- ロボット視点: 最初の実装検証機として最有力。壊しても損失が比較的小さい。

### DJI Osmo 360

- 良い点: 8K50、1型相当級センサー、120MP静止画、内蔵ストレージ、10-bit/D-Log M、DJIマイク連携。レビューでは価格/画質/操作性が評価される。
- 悪い点: レンズ交換不可。水中は本体防水でもスティッチ問題に注意。ROS2情報が少ない。
- ロボット視点: ハードは非常に魅力的だが、ROS2に入れるまでの開発工数が未知。

### GoPro MAX2 / MAX

- 良い点: MAX2はTrue 8K、交換レンズ、GPS、Log/timecode系が強み。GoProらしい堅牢性。
- 悪い点: TechRadarレビューでは低照度や発熱/バッテリに注意。ROS2実例は少ない。
- ロボット視点: GoPro ecosystemを使う理由があるなら候補。ROS2統合は追加調査が必要。

### Kandao QooCam 3 Ultra

- 良い点: 1/1.7型、F1.6、8K/30、5.7K/60、96MP、10-bit HDR、14-bit DNG。B&Hで新品$479/中古$392.50と海外価格は強い。
- 悪い点: 国内価格は高めに出ることがある。重い。ROS2実例が少ない。
- ロボット視点: 静止画・暗所・画質重視なら面白いが、ROS2導入リスクはInsta360/RICOHより高い。

### Labpano / Trisio / XPhase

- Labpano: Android OS/Open API/ライブ配信に強く、業務用途向け。価格・重量・ROS2事例の少なさが課題。
- Trisio Lite 2: 単眼回転で高品質静止パノラマを安く作るカメラ。動画/移動ロボットには不向き。
- XPhase: 静止画解像度は非常に高いが、動画なし・ワークフロー重め。点群色付けを停止撮影で最高画質にしたい場合のみ検討。

## 実装メモ

最初の検証手順:

1. Insta360 X3またはX4をUSB接続し、ROS2 Humbleで `ai4ce/insta360_ros_driver` または `camera_ros` 経由で `/image_raw` を出す。
2. equirectangular画像の解像度とfpsを固定する。最初は 3840x1920/30fps 程度。
3. カメラをロボット上部中央に固定し、LiDAR座標系とのTFを測る。
4. 3D点の方向ベクトルを equirectangular画像へ投影する小さなROS2ノードを作る。
5. まず停止状態で点群色付けを検証し、移動時のブレ/ローリング歪み/時刻ずれを見る。

equirectangular投影の基本式:

```text
dir = normalize(point_in_camera_frame)
longitude = atan2(dir.y, dir.x)
latitude = asin(dir.z)
u = (longitude + pi) / (2*pi) * image_width
v = (pi/2 - latitude) / pi * image_height
```

## 主要リンク

### ROS2/実装

- Insta360 ROS driver (ai4ce): https://github.com/ai4ce/insta360_ros_driver
- Insta360 ROS2 driver (hzlbbfrog): https://github.com/hzlbbfrog/insta360_ros2
- Insta360 X4 + camera_ros事例: https://github.com/RobotiXX/insta360_camera_ros
- RICOH THETA ROS2 camera: https://github.com/hijimasa/ros2_theta_cam
- RICOH THETA V ROS2 (Dashing/Humble): https://github.com/itsuka-to/ros2_thetav
- RICOH THETA ROS/ROS2 driver: https://github.com/stella-cv/theta_driver
- RICOH THETA ROS1 package notes: https://github.com/madjxatw/ricoh_theta_ros
- ROS2 + THETA V + RViz2事例: https://community.theta360.guide/t/ricoh-theta-live-streaming-360-object-detect-yolo-in-ros2-rviz2-and-kr260/10207
- ROS2 point cloud colorize: https://github.com/leo-drive/color-point-cloud
- OmniColor paper: https://arxiv.org/html/2404.04693v2

### ROS2ドライバの感想・レビュー・解説

- ai4ce/insta360_ros_driver 解説 (DeepWiki、構成/インストール/キャリブレーション解説): https://deepwiki.com/ai4ce/insta360_ros_driver
- ai4ce driver X4互換性の議論 (Issue #13): https://github.com/ai4ce/insta360_ros_driver/issues/13
- ai4ce driver 処理速度/出力周波数の議論 (Issue #20、RTX4090でも周波数変動の報告): https://github.com/ai4ce/insta360_ros_driver/issues/20
- THETA V を ROS2 + RViz2 + YOLO + KR260 でライブ配信した実践レポート (THETA Vは扱いやすいとの所感): https://community.theta360.guide/t/ricoh-theta-live-streaming-360-object-detect-yolo-in-ros2-rviz2-and-kr260/10207

### 公式/スペック

- RICOH THETA X: https://support.ricoh360.com/manual/x-add-info-01
- RICOH THETA Z1: https://support.ricoh360.com/manual/z1-add-info-01
- RICOH360 THETA A1: https://contents.ricoh360.com/theta/eu/en/a1
- RICOH THETA A1 release: https://www.ricoh.com/release/2025/0603_2
- Insta360 X5: https://www.insta360.com/product/insta360-x5
- Insta360 X4: https://www.insta360.com/product/insta360-x4
- Insta360 X3: https://www.insta360.com/product/insta360-x3
- Insta360 SDK: https://onlinemanual.insta360.com/developer/en-us/resource/sdk
- DJI Osmo 360: https://www.dji.com/360
- DJI Osmo 360 specs: https://www.dji.com/360/specs
- GoPro MAX2: https://gopro.com/en/us/shop/cameras/learn/max2/CHDHZ-311-master.html
- Kandao QooCam 3 Ultra specs: https://www.kandaovr.com/qoocam-3-ultra/tech-spec
- Labpano/Panox PilotPano: https://store.panox.com/products/pilotpano
- Labpano/Panox Pilot One EE: https://store.panox.com/products/pilot-one
- Trisio: https://www.trisio.com/
- XPhase Pro S2/X2: https://www.stabilizer-pro.com/products/xphase-pro-s2-x2-200mp-25lens-360-vr-camera

### 価格

- RICOH THETA X 価格.com: https://kakaku.com/item/K0001432210/
- RICOH THETA X RICOH360 Store: https://store-jp.ricoh360.com/products/theta-x
- RICOH THETA Z1 RICOH360 Store: https://store-jp.ricoh360.com/products/theta-z1
- RICOH THETA V キタムラ中古: https://shop2.kitamura.jp/%E3%83%AA%E3%82%B3%E3%83%BC%2BRICOH%2BTHETA%2BV/pd/4961311919947/
- Insta360 X5 価格.com: https://kakaku.com/item/K0001687256/
- Insta360 X4 価格推移: https://kakaku.com/item/K0001620327/pricehistory/
- Insta360 X4 中古: https://price-rank.com/p/146797?condition=used
- DJI Osmo 360 価格.com: https://kakaku.com/item/K0001702074/
- GoPro MAX2 キタムラ: https://shop.kitamura.jp/ec/pd/4595319442468
- QooCam 3 Ultra B&H: https://www.bhphotovideo.com/c/product/1858457-REG/kandao_289797_qoocam_3_ultra_360.html

### レビュー/評判

- RICOH THETA Z1 review: https://360rumors.com/ricoh-theta-z1/
- RICOH THETA X hands-on: https://hugh-hou.medium.com/ricoh-theta-x-hands-on-review-d722e19d35cc
- Mapillary THETA X user thread: https://forum.mapillary.com/t/ricoh-theta-x-coming/5773
- Insta360 X5 review: https://www.techradar.com/cameras/360-cameras/insta360-x5-review
- Insta360 X4 review: https://www.wired.com/review/insta360-x4-360-camera/
- DJI Osmo 360 review: https://www.techradar.com/cameras/360-cameras/dji-osmo-360-review
- GoPro MAX2 review: https://www.techradar.com/cameras/360-cameras/gopro-max-2-review
- QooCam 3 Ultra review: https://fstoppers.com/gear/reviews-qoocam-3-ultra-360-camera-worthy-name-680102
- Trisio Lite 2 review: https://blog.kuula.co/cameras-trisio-lite-2-review
