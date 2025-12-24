# プロジェクト概要

ロボットハードウェア (BotWheel Explorer) に関する技術資料リポジトリ。

## プロジェクト構成

- **ドキュメントのみ**: コードなし、Markdownファイルで構成
- **言語**: 日本語
- **対象ハードウェア**: ODrive BotWheel Explorer (2輪駆動ロボットプラットフォーム)

## ドキュメント構成

| カテゴリ | ファイル | 内容 |
|----------|----------|------|
| メインコンポーネント | `ODrive_S1.md` | モータコントローラ仕様 |
| | `BotWheel_Explorer.md` | キット仕様、組立情報 |
| | `RaspberryPi4.md` | 電源、GPIO、CAN設定 |
| 電源系 | `Battery.md` | LiTime 24V LiFePO4、電圧設定 |
| | `DCDC_Converter.md` | 5V変換、USB-PD |
| | `LowVoltageDisconnect.md` | 過放電保護モジュール |
| 配線・端子 | `Cable_Wiring.md` | AWG規格、コネクタ |
| | `Ferrule.md` | 棒端子、DIN 46228 |
| 機械部品 | `Screw_Specs.md` | メトリックネジ規格 |

## 編集ルール

1. **引用元の明記**: 各セクションに `> **引用元**: [リンク名](URL)` 形式で情報源を記載
2. **表形式を多用**: 仕様は表 (`| 項目 | 仕様 |`) で整理
3. **目次の維持**: 各ファイル先頭に目次セクションを配置
4. **リンクは文脈に配置**: 関連リンクは該当する内容の近くに記載 (末尾にまとめない)

## 主要コンポーネント仕様

- **ODrive S1**: 12-48V、40A連続、CAN 250kbps
- **BotWheel**: 171mm径ハブモーター、3200 CPRエンコーダ
- **Raspberry Pi 4**: 5V 3A、SPI経由CAN HAT
- **LiTime 24V 50Ah**: 8S LiFePO4、25.6V公称、BMS内蔵
