# プロジェクト概要

ロボットハードウェア (BotWheel Explorer) に関する技術資料リポジトリ。

## プロジェクト構成

- **ドキュメントのみ**: コードなし、Markdownファイルで構成
- **言語**: 日本語
- **対象ハードウェア**: ODrive BotWheel Explorer (2輪駆動ロボットプラットフォーム)

## ドキュメント構成

リポジトリ直下が**採用確定構成**、`検討中/` フォルダが**未確定の検討段階**の資料。

### 確定構成 (リポジトリ直下)

| カテゴリ | ファイル | 内容 |
|----------|----------|------|
| メインコンポーネント | `ODrive_S1.md` | モータコントローラ仕様 |
| | `BotWheel_Explorer.md` | キット仕様、組立情報 |
| | `Livox_MID360.md` | 3D LiDARセンサ仕様 |
| | `RealSense_D435i.md` | ステレオ深度カメラ + IMU (6DoF)、近距離障害物検出・RGB-D認識 |
| | `MINISFORUM_UM790Pro.md` | ロボット母艦PC (Ryzen 9 7940HS)、USB4/2.5GbE/19V給電 |
| | `AmiVoice_WT01.md` | 音声認識特化Bluetoothウェアラブルマイク (2マイクアレイ・ノイズキャンセリング) |
| 電源系 | `Battery.md` | BotWheel Explorer Kit 標準電源 (DeWalt 20V)、マキタ18V、電圧設定 |
| | `DCDC_Converter.md` | 5V変換 (Buckコンバータ, Pi 4向け) |
| | `LowVoltageDisconnect.md` | 過放電保護モジュール (OONO 18V) |
| | `Anker_Prime_PowerBank.md` | Anker Prime 27650mAh/250W モバイルバッテリー (補助電源) |
| 配線・端子・接続 | `Cable_Wiring.md` | AWG規格、コネクタ |
| | `Ferrule.md` | 棒端子、DIN 46228 |
| | `USB-HUB-7U.md` | Waveshare 工業用7ポートUSB 2.0ハブ (MTT・ESD/過電圧保護) |
| 機械部品 | `Screw_Specs.md` | メトリックネジ規格 |
| インデックス | `README.md` | 全ドキュメントへのリンク |

### 検討中 (`検討中/` フォルダ)

| ファイル | 内容 |
|----------|------|
| `検討中/README.md` | 検討中ドキュメントのインデックス |
| `検討中/RaspberryPi4.md` | Raspberry Pi 4: 電源、GPIO、CAN設定 |
| `検討中/Anker_PowerConf_S3.md` | 会議用スピーカーフォン |
| `検討中/Inverted_2D_LiDAR.md` | 逆さ・下向き傾斜 2D LiDAR による低位置障害物検出の調査 |
| `検討中/LiTime_24V_LiFePO4.md` | 24V系電源候補 (LiTime 24V LiFePO4) |
| `検討中/RaspberryPi5_USB_PD_Power.md` | Pi 5 / USB-PD 電源変換 (Coolgear CG-PD200MAX) |
| `検討中/CZH-LABS_24V_LVD.md` | 24V系 過放電保護 (CZH-LABS 24V 30A LVD) |
| `検討中/ROS2_DiffDrive_Reference.md` | ROS2 差動二輪リファレンス |
| `検討中/OpenHW_DiffDrive_References.md` | オープンHW差動二輪リファレンス集 |
| `検討中/flow_x13.md` | ASUS ROG Flow X13 充電スペック |

> **24V系電源の関係**: `検討中/` の LiTime 24V バッテリー・CG-PD200MAX (USB-PD)・CZH-LABS 24V LVD は一体の「24V系電源案」。確定構成の DeWalt 20V 系統とは別系統。

## 編集ルール

1. **引用元の明記**: 各セクションに `> **引用元**: [リンク名](URL)` 形式で情報源を記載
2. **表形式を多用**: 仕様は表 (`| 項目 | 仕様 |`) で整理
3. **目次の維持**: 各ファイル先頭に目次セクションを配置
4. **リンクは文脈に配置**: 関連リンクは該当する内容の近くに記載 (末尾にまとめない)
5. **git操作は指示時のみ**: `git commit` / `git push` はユーザーから明示的に指示があった場合のみ実行
6. **確定と検討中の分離**: 採用確定はリポジトリ直下、未確定は `検討中/` に置く。移動時は元ファイルから該当記述を削除し、文脈位置に検討中ファイルへのリンクを残す。`検討中/` 直下からの相対リンクは `../` で親を参照

## 主要コンポーネント仕様

- **ODrive S1**: 12-48V、40A連続、CAN 250kbps
- **BotWheel**: 171mm径ハブモーター、3200 CPRエンコーダ
- **DeWalt 20V (Kit標準電源)**: 5S Li-ion、18-20V公称、110Wh
- **Raspberry Pi 4** (検討中): 5V 3A、SPI経由CAN HAT
- **LiTime 24V 50Ah** (検討中): 8S LiFePO4、25.6V公称、BMS内蔵
- **Livox MID-360**: 905nm LiDAR、360°×59°FOV、200,000点/秒、9-27V DC、IP67
- **Intel RealSense D435i**: ステレオ深度カメラ、深度FOV 87°×58°、IMU BMI055 (6DoF)、USB-C 3.1 Gen1
- **MINISFORUM UM790 Pro**: Ryzen 9 7940HS (8C/16T)、DDR5最大64GB、USB4/2.5GbE、19V/120W
