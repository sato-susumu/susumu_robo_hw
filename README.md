# susumu_robo_hw

> [!WARNING]
> **注意：このリポジトリは生成AIで適当に作ってます。**

ロボットハードウェアに関する技術資料

## ドキュメント

### メインコンポーネント

- [ODrive S1 技術資料](ODrive_S1.md) - ODrive S1モータコントローラのスペック、ピンアウト、設定
- [BotWheel Explorer 技術資料](BotWheel_Explorer.md) - BotWheel Explorerキットの仕様、組立情報
- [Livox MID-360 技術資料](Livox_MID360.md) - 3D LiDARセンサ仕様、点群・測距・インターフェース
- [Intel RealSense D435i 技術資料](RealSense_D435i.md) - ステレオ深度カメラ + IMU (6DoF)、近距離障害物検出・RGB-D認識
- [MINISFORUM Venus UM790 Pro 技術資料](MINISFORUM_UM790Pro.md) - ロボット母艦PC (Ryzen 9 7940HS)、USB4/2.5GbE/19V給電
- [AmiVoice Front WT01 技術資料](AmiVoice_WT01.md) - 音声認識特化Bluetoothウェアラブルマイク (2マイクアレイ・ノイズキャンセリング)

### 電源・電気系

- [バッテリー技術資料](Battery.md) - LiTime 24V LiFePO4仕様、電圧設定、ヒューズ
- [低電圧カットオフモジュール (LVD) 技術資料](LowVoltageDisconnect.md) - 過放電保護モジュール (18V/24V)
- [DC-DCコンバータ技術資料](DCDC_Converter.md) - Raspberry Pi用電源変換、USB-PD
- [Anker Prime Power Bank (27650mAh, 250W) 技術資料](Anker_Prime_PowerBank.md) - 大容量・高出力モバイルバッテリー (USB-C PD 最大140W×2)、補助電源

### 配線・端子・接続

- [ケーブル・配線規格](Cable_Wiring.md) - AWG規格、コネクタ型番
- [フェルール (棒端子) 技術資料](Ferrule.md) - DIN 46228色コード、寸法規格
- [Waveshare USB-HUB-7U 技術資料](USB-HUB-7U.md) - 工業用7ポートUSB 2.0ハブ (MTT技術・ESD/過電圧保護・金属筐体)

### 機械部品

- [ネジ規格技術資料](Screw_Specs.md) - メトリックネジ寸法

### 検討中

採用が確定していない検討段階の資料は専用フォルダにまとめています。

- [検討中ドキュメント一覧](検討中/README.md) - Raspberry Pi 4、Anker PowerConf S3、ROS2/オープンHW差動二輪リファレンス等
