# 検討中ドキュメント

> [!NOTE]
> このフォルダは**採用が確定していない検討段階**の技術資料を置く場所です。
> 構成・部品の検討用メモであり、本採用された内容はリポジトリ直下に移動します。

## ドキュメント一覧

### コンポーネント検討

- [Raspberry Pi 4 技術資料](RaspberryPi4.md) - 電源仕様、GPIO、CAN設定
- [Anker PowerConf S3 技術資料](Anker_PowerConf_S3.md) - 会議用スピーカーフォン仕様

### センサ構成検討

- [逆さ・下向き傾斜 2D LiDAR による低位置障害物検出](Inverted_2D_LiDAR.md) - 取り付け手法・製品/ロボット事例・関連記事・論文の調査メモ (URL付き)
- [全天球カメラ検討メモ](Omnidirectional_360_Cameras.md) - 360度カメラ候補、価格、ROS2適性、LiDAR色付き点群用途、レビューリンク

### 電源検討 (24V系)

検討中の **24V LiFePO4 (LiTime)** を中核とした電源系統一式。Kit標準電源 (DeWalt 20V) とは別系統。

- [LiTime 24V LiFePO4バッテリー](LiTime_24V_LiFePO4.md) - 24V系・大容量の電源候補 (50Ah/25Ah)、電圧設定
- [Raspberry Pi 5 / USB-PD 電源変換](RaspberryPi5_USB_PD_Power.md) - Coolgear CG-PD200MAX (USB-PD 200W)、Pi 5/USB-PD給電、24Vバッテリーとの互換性
- [CZH-LABS 24V 30A LVD Module](CZH-LABS_24V_LVD.md) - 24V LiFePO4 用の過放電保護 (LVD)、推奨設定・電圧-SOCチャート

### ソフトウェア・ROS2

- [ROS2 差動二輪 リファレンスモデル](ROS2_DiffDrive_Reference.md) - ros2_control + diff_drive_controller の標準スタック、既存実装比較、本構成への適用、運動学モデル
- [オープンハードウェア 差動二輪 リファレンス集 (10〜50kgクラス)](OpenHW_DiffDrive_References.md) - 同クラスのオープンHW差動二輪プロジェクト比較 (ホバーボード系・Linorobot2・MORPH等)

### その他

- [ASUS ROG Flow X13 充電スペック](flow_x13.md) - USB-C PD充電仕様
