# 検討中ドキュメント

> [!NOTE]
> このフォルダは**採用が確定していない検討段階**の技術資料を置く場所です。
> 構成・部品の検討用メモであり、本採用された内容はリポジトリ直下に移動します。

## ドキュメント一覧

### コンポーネント検討

- [Raspberry Pi 4 技術資料](RaspberryPi4.md) - 電源仕様、GPIO、CAN設定
- [MINISFORUM Venus UM790 Pro 技術資料](MINISFORUM_UM790Pro.md) - ミニPC (Ryzen 9 7940HS)、ロボット母艦PC候補。USB4/2.5GbE/19V給電
- [Anker PowerConf S3 技術資料](Anker_PowerConf_S3.md) - 会議用スピーカーフォン仕様
- [AmiVoice Front WT01 技術資料](AmiVoice_WT01.md) - 音声認識特化Bluetoothウェアラブルマイク (2マイクアレイ・ノイズキャンセリング)

### センサ構成検討

- [Intel RealSense D435i 技術資料](RealSense_D435i.md) - ステレオ深度カメラ + IMU (6DoF)。深度FOV 87°×58°、USB 3.0、近距離障害物検出・RGB-D認識
- [逆さ・下向き傾斜 2D LiDAR による低位置障害物検出](Inverted_2D_LiDAR.md) - 取り付け手法・製品/ロボット事例・関連記事・論文の調査メモ (URL付き)

### 周辺機器・接続

- [Waveshare USB-HUB-7U 技術資料](USB-HUB-7U.md) - 工業用7ポートUSB 2.0ハブ (MTT技術・ESD/過電圧保護・金属筐体)

### 電源検討 (24V系)

検討中の **24V LiFePO4 (LiTime)** を中核とした電源系統一式。Kit標準電源 (DeWalt 20V) とは別系統。

- [LiTime 24V LiFePO4バッテリー](LiTime_24V_LiFePO4.md) - 24V系・大容量の電源候補 (50Ah/25Ah)、電圧設定
- [Raspberry Pi 5 / USB-PD 電源変換](RaspberryPi5_USB_PD_Power.md) - Coolgear CG-PD200MAX (USB-PD 200W)、Pi 5/USB-PD給電、24Vバッテリーとの互換性
- [CZH-LABS 24V 30A LVD Module](CZH-LABS_24V_LVD.md) - 24V LiFePO4 用の過放電保護 (LVD)、推奨設定・電圧-SOCチャート

### 電源検討 (その他)

- [Anker Prime Power Bank (27650mAh, 250W)](Anker_Prime_PowerBank.md) - 大容量・高出力モバイルバッテリー (USB-C PD 最大140W×2)、母艦PC/Pi の補助電源候補

### ソフトウェア・ROS2

- [ROS2 差動二輪 リファレンスモデル](ROS2_DiffDrive_Reference.md) - ros2_control + diff_drive_controller の標準スタック、既存実装比較、本構成への適用、運動学モデル
- [オープンハードウェア 差動二輪 リファレンス集 (10〜50kgクラス)](OpenHW_DiffDrive_References.md) - 同クラスのオープンHW差動二輪プロジェクト比較 (ホバーボード系・Linorobot2・MORPH等)

### その他

- [ASUS ROG Flow X13 充電スペック](flow_x13.md) - USB-C PD充電仕様
