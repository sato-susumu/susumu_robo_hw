# susumu_robo_hw

> [!WARNING]
> **注意：このリポジトリは生成AIで適当に作ってます。**

ロボットハードウェアに関する技術資料

## ドキュメント

### メインコンポーネント

- [ODrive S1 技術資料](ODrive_S1.md) - ODrive S1モータコントローラのスペック、ピンアウト、設定
- [BotWheel Explorer 技術資料](BotWheel_Explorer.md) - BotWheel Explorerキットの仕様、組立情報
- [Raspberry Pi 4 技術資料](RaspberryPi4.md) - 電源仕様、GPIO、CAN設定
- [Livox MID-360 技術資料](Livox_MID360.md) - 3D LiDARセンサ仕様、点群・測距・インターフェース

### 電源・電気系

- [バッテリー技術資料](Battery.md) - LiTime 24V LiFePO4仕様、電圧設定、ヒューズ
- [低電圧カットオフモジュール (LVD) 技術資料](LowVoltageDisconnect.md) - 過放電保護モジュール (18V/24V)
- [DC-DCコンバータ技術資料](DCDC_Converter.md) - Raspberry Pi用電源変換、USB-PD

### 配線・端子

- [ケーブル・配線規格](Cable_Wiring.md) - AWG規格、コネクタ型番
- [フェルール (棒端子) 技術資料](Ferrule.md) - DIN 46228色コード、寸法規格

### ソフトウェア・ROS2

- [ROS2 差動二輪 リファレンスモデル](ROS2_DiffDrive_Reference.md) - ros2_control + diff_drive_controller の標準スタック、既存実装比較、本構成への適用、運動学モデル
- [オープンハードウェア 差動二輪 リファレンス集 (10〜50kgクラス)](OpenHW_DiffDrive_References.md) - 同クラスのオープンHW差動二輪プロジェクト比較 (ホバーボード系・Linorobot2・MORPH等)

### 機械部品

- [ネジ規格技術資料](Screw_Specs.md) - メトリックネジ寸法

### その他

- [ASUS ROG Flow X13 充電スペック](flow_x13.md) - USB-C PD充電仕様
