# ODrive S1 / BotWheel Explorer 技術資料

---

## 目次

1. [ODrive S1 スペック表](#odrive-s1-スペック表)
   - [電気的仕様](#電気的仕様)
   - [物理的仕様](#物理的仕様)
   - [制御モード](#制御モード)
   - [エンコーダサポート](#エンコーダサポート)
   - [通信インターフェース](#通信インターフェース)
   - [ブレーキ抵抗器](#ブレーキ抵抗器)
2. [ODrive S1 端子・ピンアウト](#odrive-s1-端子ピンアウト)
   - [コネクタ一覧](#コネクタ一覧)
   - [電源パッド配置](#電源パッド配置)
   - [J11 統合I/Oヘッダー (30ピン)](#j11-統合ioヘッダー-30ピン)
   - [J16/J17 CANヘッダー](#j16j17-canヘッダー)
   - [GPIO特性](#gpio特性)
3. [ODrive BotWheel Explorer スペック表](#odrive-botwheel-explorer-スペック表)
   - [キット内容物](#キット内容物-フルキット)
   - [完成時寸法](#完成時寸法)
   - [BotWheel モーター仕様](#botwheel-モーター仕様)
   - [BotWheel 物理仕様](#botwheel-物理仕様)
   - [BotWheel センサー](#botwheel-センサー)
   - [キャスター (補助輪) 仕様](#キャスター-補助輪-仕様)
4. [ケーブル・配線規格](#ケーブル配線規格)
   - [AWG規格表](#awg規格表)
   - [用途別推奨ケーブル](#用途別推奨ケーブル)
   - [コネクタ型番一覧](#コネクタ型番一覧)
5. [電源・バッテリー](#電源バッテリー)
   - [推奨電源仕様](#推奨電源仕様)
   - [DeWalt 20Vバッテリー仕様](#dewalt-20vバッテリー仕様)
   - [利用ヒューズ](#利用ヒューズ)
   - [ブレードヒューズ色別規格](#ブレードヒューズ-atoatc-色別規格)
6. [DC-DCコンバータ](#dc-dcコンバータ)
7. [電圧関連まとめ](#電圧関連まとめ)
8. [電圧保護設定](#電圧保護設定-odrive-s1)
9. [外部電圧アラーム](#外部電圧アラーム-リポチェッカー)
10. [リンク集](#リンク集)
   - [ハードウェア関連](#ハードウェアに関するリンク)
   - [ソフトウェア関連](#ソフトウェアに関するリンク)
   - [3D CAD・設計データ](#3d-cad設計データ)

---

# ODrive S1 スペック表

## 電気的仕様

| 項目 | 仕様 |
|------|------|
| 動作電圧 | 12-48V (最大50.5V) |
| 連続電流 | 40A (ヒートスプレッダー使用推奨) |
| 連続出力 | 2kW |
| PWM周波数 | 24kHz |
| 制御ループ周波数 | 8kHz (電流制御ループ24kHz予定) |
| 最大電気周波数 | 700Hz (2000Hz対応予定) |
| ロジック電源入力 (オプション) | 10-14V |

## 物理的仕様

| 項目 | 仕様 |
|------|------|
| 基板サイズ | 66mm x 50mm |
| 質量 (端子なし) | 35g |
| 質量 (端子あり) | 55g |

## 制御モード

| モード | 説明 |
|--------|------|
| トルク制御 | 電流(トルク)を直接制御 |
| 速度制御 | 目標速度に追従 |
| 位置制御 | 目標位置に移動 |
| トラジェクトリ制御 | 軌道計画に沿った動作 |
| センサレス速度制御 | エンコーダなしで速度制御 |

## エンコーダサポート

| タイプ | インターフェース |
|--------|------------------|
| オンボード磁気エンコーダ | MA702 IC内蔵 |
| インクリメンタル | クアドラチャ / ホール |
| アブソリュート (SPI) | AMS, CUI, Broadcom等 |
| アブソリュート (RS485) | MPS, RLS等 |

> **注意**: RS485とSPIエンコーダは同時使用不可

## 通信インターフェース

| インターフェース | 仕様 |
|------------------|------|
| CAN | 2.0B @ 1Mbps (CAN-FD 5Mbps実験的サポート) |
| USB | USB 2.0 |
| UART | 絶縁、3.3V/5V対応 |
| STEP/DIR | 絶縁、ステッピングモーター互換 |
| PWM入力 | RC受信機対応 |
| アナログ入力 | 電圧入力による制御 |

## ブレーキ抵抗器

| 項目 | 仕様 |
|------|------|
| 付属抵抗器 | 2Ω 50W |
| ピーク回生電力 | 2000W |
| オンボードチョッパ | 搭載 |

---

# ODrive S1 端子・ピンアウト

> **引用元**: [ODrive S1 Datasheet - ODrive Documentation](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html)
>
> 以下の端子情報は公式データシートからの引用です。最新情報は公式ドキュメントを参照してください。

## ピンアウト図

> **画像引用**: ODrive S1 Pinout Diagram
>
> ![ODrive S1 Pinout](https://docs.odriverobotics.com/v/latest/_images/s1-pinout.png)
>
> *出典: [ODrive S1 Datasheet](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html)*

## コネクタ一覧

| コネクタ | 説明 | 基板側型番 | ハーネス側型番 |
|----------|------|-----------|---------------|
| Power | 電源スクリュー端子 (オプション) | TB005-762-07BE | N/A |
| J11 | 統合I/Oヘッダー (30ピン) | S30B-PUDSS-1 | PUDP-30V-S |
| J16 | CANヘッダー1 | SM04B-GHS-TB | GHR-04V-S |
| J17 | CANヘッダー2 | SM04B-GHS-TB | GHR-04V-S |
| J1 | デバッグヘッダー | BM05B-GHS-TB | GHR-05V-S |

## 電源パッド配置

| パッド | 機能 | 説明 |
|--------|------|------|
| DC+ | 電源入力 (+) | DC-基準、12-48V |
| DC- | パワーグラウンド | システムGND |
| A | モーター相A | 任意の順序で接続可 |
| B | モーター相B | 任意の順序で接続可 |
| C | モーター相C | 任意の順序で接続可 |
| R+ | ブレーキ抵抗 (+) | 外部抵抗接続用 |
| R- | ブレーキ抵抗 (-) | 外部抵抗接続用 |

## J11 統合I/Oヘッダー (30ピン)

> **画像引用**: J11 Unified I/O Header Pinout
>
> ![J11 Pinout](https://docs.odriverobotics.com/v/latest/_images/s1-pinout.png)
>
> *出典: [ODrive S1 Datasheet - Pinout](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html#pinout)*

### ピン配置表

| ピン | 名称 | 機能 | GPIO番号 | 備考 |
|------|------|------|----------|------|
| 1 | GND | グラウンド | - | - |
| 2 | 12V IN | ロジック電源入力 | - | 10-14V、オプション |
| 3 | GND ISO | 絶縁GND | - | 絶縁IO用 |
| 4 | V+ ISO | 絶縁電源入力 | - | 3.3V or 5V |
| 5 | STEP | ステップ入力 (絶縁) | G05 | 入力のみ |
| 6 | DIR | 方向入力 (絶縁) | G07 | 入力のみ |
| 7 | ENABLE | イネーブル入力 (絶縁) | G08 | 入力のみ |
| 8 | OUT | 汎用出力 (絶縁) | G06 | 出力のみ |
| 9 | TX+ | UART TX+ (RS422) | G00 | 差動出力 |
| 10 | TX- | UART TX- (RS422) | G00 | 差動出力 |
| 11 | RX | UART RX | G03 | シングルエンド入力 |
| 12 | GND | グラウンド | - | - |
| 13 | THERM+ | サーミスタ+ | G04 | 1kΩプルアップ内蔵 |
| 14 | THERM- | サーミスタ- | - | GND接続 |
| 15 | HALL A | ホールセンサーA | G01 | 2.7kΩプルアップ |
| 16 | HALL B | ホールセンサーB | G02 | 2.7kΩプルアップ |
| 17 | HALL Z | ホールセンサーZ/Index | G11 | 2.7kΩプルアップ |
| 18 | +5V | 5V出力 | - | センサー電源用 |
| 19 | GND | グラウンド | - | - |
| 20 | ENC A | エンコーダA | G09 | クアドラチャ |
| 21 | ENC B | エンコーダB | G10 | クアドラチャ |
| 22 | SPI SCK | SPI クロック | - | 外部エンコーダ用 |
| 23 | SPI MISO | SPI データ入力 | - | 外部エンコーダ用 |
| 24 | SPI MOSI | SPI データ出力 | - | 外部エンコーダ用 |
| 25 | SPI nCS | SPI チップセレクト | G12 | nCS専用 |
| 26 | RS485 A | RS485 A (+) | - | 差動通信 |
| 27 | RS485 B | RS485 B (-) | - | 差動通信 |
| 28 | RS485 Y | RS485 Y | - | エコー用 |
| 29 | RS485 Z | RS485 Z | - | エコー用 |
| 30 | GND | グラウンド | - | - |

### GPIO特性詳細

| GPIOグループ | ピン | 特性 |
|--------------|------|------|
| ホールピン | G01, G02, G11 | 2.7kΩプルアップ (5V)、ローパスフィルタ (τ=4.25μs) |
| サーミスタ | G04 | 1kΩプルアップ (3.3V)、分圧回路内蔵 |
| 絶縁入力 | G05, G07, G08 | 入力専用、1.5MΩプルダウン内蔵 |
| 絶縁出力 | G06 | 出力専用 |
| RS422 TX | G00 | 差動出力、ロジック入力不可 |
| SPI nCS | G12 | nCS専用、汎用GPIO不可 |

## J16/J17 CANヘッダー

> **画像引用**: CAN Header Pinout (J16/J17)
>
> ![CAN Pinout](https://docs.odriverobotics.com/v/latest/_images/s1-pinout.png)
>
> *出典: [ODrive S1 Datasheet - Pinout](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html#pinout)*
>
> 詳細: [CAN Bus Guide](https://docs.odriverobotics.com/v/latest/guides/can-guide.html)

| ピン | 名称 | 機能 |
|------|------|------|
| 1 | CAN_H | CAN High |
| 2 | CAN_L | CAN Low |
| 3 | GND NC | GND (デイジーチェーン用、内部未接続) |
| 4 | GND NC | GND (デイジーチェーン用、内部未接続) |

> **公式情報**: J16/J17のGNDピンは内部でODriveに接続されておらず、デイジーチェーン用途のみ。グラウンドループを作らずにCANバスのGNDを接続可能。
>
> *出典: [ODrive S1 Datasheet](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html)*

### CAN終端抵抗

| 項目 | 仕様 |
|------|------|
| オンボード終端抵抗 | 120Ω |
| 有効化方法 | DIPスイッチ "CAN 120R" をON |
| 使用条件 | バスの両端デバイスのみ有効化 |

> **注意**: CAN_GNDはDC-に単一点 (スターポイント) で接続必須

## GPIO特性

| ピン特性 | 仕様 |
|----------|------|
| 電圧許容 | 5Vトレラント (V+ ISO=5V時) |
| 絶縁IO電源 (V+ ISO) | 3.3V または 5V 入力 |
| 出力レベル | V+ ISO と同電圧 |
| プルアップ/プルダウン | 絶縁IOには内蔵なし |

### サーミスタ接続

| S1ピン | 接続先 |
|--------|--------|
| Pin 13 (thermistor+) | BotWheelサーミスタ信号 |
| Pin 14 (thermistor-) | GND |

> **注意**: THERMISTOR+ には1kΩの内蔵分圧抵抗あり

---

# ODrive BotWheel Explorer スペック表

> **公式情報**: [BotWheel Explorer Kit - ODrive Shop](https://shop.odriverobotics.com/products/botwheel-explorer)
>
> **公式ドキュメント**: [BotWheel Explorer Guide](https://docs.odriverobotics.com/v/latest/guides/botwheel-explorer.html)
>
> **公式ビルドガイド**: [BotWheel Explorer REV-B Hardware Build (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-REV-B-Hardware-Build-0eb19815a7b847a2a037a4246647d13c)

## キット内容物 (フルキット)

| 品目 | 数量 |
|------|------|
| ODrive S1 (スクリュー端子付) | 2 |
| ODrive BotWheel | 2 |
| ODrive S1エンクロージャ (ヒートスプレッダ・透明) | 2 |
| USBアイソレータ | 1 |
| シャーシプレート | 1 |
| メカニカルパーツバンドル (キャスター・CANハーネス含む) | 1 |

## 完成時寸法

> *出典: [BotWheel Explorer Kit](https://shop.odriverobotics.com/products/botwheel-explorer)*

| 項目 | 仕様 |
|------|------|
| サイズ | 450mm x 500mm x 175mm |
| 最低地上高 | 100mm |
| トラック幅 | 419mm |
| 重量 | 約20kg |
| 最大積載量 | 100kg (中央に均等分布) |

## 環境定格

> *出典: [BotWheel Explorer Kit](https://shop.odriverobotics.com/products/botwheel-explorer)*

| 項目 | 仕様 |
|------|------|
| IP等級 | IP10 |
| 使用環境 | 屋内・乾燥環境のみ |

---

## BotWheel モーター仕様

| 項目 | 仕様 |
|------|------|
| モータータイプ | ブラシレスハブモーター |
| ポール対数 | 15 |
| Kv値 | 8.7 RPM/V |
| トルク定数 (Kt) | 0.951 N-m/A |
| 定格トルク | 5 Nm |
| 定格速度 (24V時) | 110 rpm |
| 定格連続電流 | 5A |
| 定格連続出力 | 70W |

## BotWheel 物理仕様

| 項目 | 仕様 |
|------|------|
| ホイール直径 | 171mm |
| ホイール幅 | 約45mm |
| 質量 (1個) | 2.2kg |
| 質量 (2個セット) | 4.4kg |
| 定格負荷 | 80kg/ホイール |
| 取付パターン | 4×M6ネジ穴 (36mm円形パターン) |
| 防水等級 | IP54 (雨天走行可、水没不可) |

## BotWheel センサー

| センサー | 仕様 |
|----------|------|
| インクリメンタルエンコーダ | 3200 CPR |
| ホールセンサー | 搭載 |
| サーミスタ | R25=20kΩ, β=3950K |

## BotWheel コネクタ

| コネクタ | 型番 | 用途 |
|----------|------|------|
| 電源/エンコーダ | JST JWPF | 防水、モーター相・エンコーダ |
| サーミスタ | JST WPJ | 防水、温度センサー |

---

## キャスター (補助輪) 仕様

> **公式情報**: [BotWheel Explorer Kit - ODrive Shop](https://shop.odriverobotics.com/products/botwheel-explorer)

BotWheel Explorerには前方にキャスター (補助輪) が1個付属しています。

| 項目 | 仕様 | 公式出典 |
|------|------|----------|
| タイプ | スイベルキャスター (360°回転) | [製品ページ](https://shop.odriverobotics.com/products/botwheel-explorer) |
| 用途 | 2輪駆動の第3支点 | - |
| 地上高確保 | 100mm | [製品ページ: Ground clearance](https://shop.odriverobotics.com/products/botwheel-explorer) |
| バージョン | RevB (改良版キャスター搭載) | [製品ページ](https://shop.odriverobotics.com/products/botwheel-explorer) |

> **公式記載**: "ODrive has updated the Botwheel Explorer to RevB, which is larger and includes an improved caster."
>
> *出典: [BotWheel Explorer Kit](https://shop.odriverobotics.com/products/botwheel-explorer)*

> **注意**: RevA (旧バージョン) が必要な場合は info@odriverobotics.com に問い合わせ

---

# ケーブル・配線規格

## AWG規格表

> **引用元**: [American Wire Gauge Chart - PowerStream](https://www.powerstream.com/Wire_Size.htm), [Engineering Toolbox](https://www.engineeringtoolbox.com/wire-gauges-d_419.html)

### AWG線径・許容電流表

| AWG | 直径 (mm) | 断面積 (mm²) | 許容電流 (A) | 抵抗 (Ω/m) | 主な用途 |
|-----|-----------|--------------|--------------|------------|----------|
| 10 | 2.59 | 5.26 | 30 | 0.00328 | 大電力、モーター電源 |
| 12 | 2.05 | 3.31 | 20 | 0.00521 | 電源ライン、モーター |
| 14 | 1.63 | 2.08 | 15 | 0.00828 | 電源、汎用 |
| 16 | 1.29 | 1.31 | 10 | 0.0132 | 中電力配線 |
| 18 | 1.02 | 0.82 | 7 | 0.0209 | 低電力、センサー |
| 20 | 0.81 | 0.52 | 5 | 0.0333 | 信号線、センサー |
| 22 | 0.64 | 0.33 | 3 | 0.0530 | 信号線、通信 |
| 24 | 0.51 | 0.20 | 2.1 | 0.0842 | 信号線、I/O |
| 26 | 0.40 | 0.13 | 1.3 | 0.134 | 細線、通信 |

> **注意**: 許容電流は単線・開放空気中の参考値。束線や高温環境では減定格が必要

### 電圧降下の目安

| AWG | 10A時の電圧降下 (1m往復) | 5A時の電圧降下 (1m往復) |
|-----|--------------------------|-------------------------|
| 12 | 0.10V | 0.05V |
| 14 | 0.17V | 0.08V |
| 18 | 0.42V | 0.21V |
| 24 | 1.68V | 0.84V |

## 用途別推奨ケーブル

| 用途 | 推奨AWG | 絶縁体 | 備考 |
|------|---------|--------|------|
| モーター電源 (DC+/DC-) | 10-12 AWG | シリコン | 高温耐性推奨 |
| モーター相 (A/B/C) | 12-14 AWG | シリコン | 短距離OK |
| ブレーキ抵抗器 | 14-16 AWG | シリコン/PVC | 発熱に注意 |
| バッテリーメイン | 10-12 AWG | シリコン | 30A対応 |
| CAN通信 | 24-26 AWG | ツイストペア | シールド推奨 |
| UART通信 | 24-26 AWG | PVC | - |
| エンコーダ | 24-26 AWG | PVC | シールド推奨 |
| ホールセンサー | 24-26 AWG | PVC | - |
| サーミスタ | 24-26 AWG | PVC | - |
| I/O汎用 | 22-24 AWG | PVC/UL007 | ODrive推奨 |
| Raspberry Pi電源 | 18-20 AWG | シリコン | 5V 3-5A対応 |

## コネクタ型番一覧

### ODrive S1 メインコネクタ

| コネクタ | 型番 | メーカー | 用途 |
|----------|------|----------|------|
| I/O ヘッダー (30ピン) | S30B-PUDSS-1 | JST | 基板側 |
| I/O ハウジング | PUDP-30V-S | JST (PUD系) | ワイヤーハーネス側 |
| I/O クリンプ端子 | SPUD-001T-P0.5 | JST | 圧着端子 |
| 電源端子 (オプション) | TB005-762-07BE | Dinkle | スクリューターミナル |
| CANヘッダー | SM04B-GHS-TB | JST (GH系) | 基板側 |
| CANハウジング | GHR-04V-S | JST (GH系) | ハーネス側 |
| デバッグヘッダー | BM05B-GHS-TB | JST (GH系) | 基板側 |

### BotWheel コネクタ

| コネクタ | 型番 | 用途 |
|----------|------|------|
| モーター/エンコーダ | JST JWPF | 防水コネクタ |
| サーミスタ | JST WPJ | 防水コネクタ |
| ハーネス接続 | JST PUD | S1との接続 |

### CANバス コネクタ

| コネクタ | 型番 | 用途 |
|----------|------|------|
| USB-CAN アダプタ側 | JST-GH | プラグアンドプレイ |
| 汎用接続 | スクリューターミナル | 柔軟な配線 |

### ハーネスビルドキット内容

| 部品 | 型番 | 数量 |
|------|------|------|
| ハウジング | PUDP-30V-S | 2個 |
| クリンプ端子 | SPUD-001T-P0.5 | 30個 |
| ワイヤー | 24AWG, 150mm, UL007 | 30本 |

---

# 電源・バッテリー

## 推奨電源仕様

| 項目 | 仕様 |
|------|------|
| 電圧範囲 | 12-48V (最大50.5V) |
| 推奨バッテリー | DeWalt 20V (5S Li-ion, 16.5-21V) |
| 付属バッテリー容量 | 110Wh |
| バッテリータイプ | DeWalt DCB205等互換 |

## DeWalt 20Vバッテリー仕様

| 項目 | 仕様 |
|------|------|
| セル構成 | 5S (5直列) |
| 満充電電圧 | 21.0V (4.2V/セル) |
| 低電圧カットオフ | 16.5V (3.3V/セル) |
| 公称電圧 | 18-20V |

## 利用ヒューズ

> **公式ビルドガイド**: [BotWheel Explorer REV-B Hardware Build (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-REV-B-Hardware-Build-0eb19815a7b847a2a037a4246647d13c)
>
> 詳細な部品リストは公式ビルドガイドを参照してください。

| 項目 | 推奨仕様 |
|------|----------|
| メインヒューズ | 30A 自動車用ブレードヒューズ |
| ワイヤーゲージ | 12AWG (高電力用) |
| ヒューズホルダー | 防水ゴムキャップ付き推奨 |

### ブレードヒューズ (ATO/ATC) 色別規格

> **引用元**: [Automotive Fuse - Wikipedia](https://en.wikipedia.org/wiki/Automotive_fuse), [Blade-Type Fuse Color Codes](https://www.electricaltechnology.org/2025/01/blade-type-fuse-color-codes.html)
>
> ![Blade Fuse Color Chart](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8e/Electrical_fuses%2C_blade_type.svg/400px-Electrical_fuses%2C_blade_type.svg.png)
>
> *出典: Wikimedia Commons*

| 定格電流 | 色 | 用途例 |
|----------|------|--------|
| 1A | 黒 | - |
| 2A | グレー | - |
| 3A | 紫/バイオレット | 小型センサー |
| 5A | 黄褐色/タン | LED、小型電装品 |
| 7.5A | 茶 | アクセサリー |
| 10A | 赤 | 照明、小型モーター |
| 15A | 青 | 電装品、中型負荷 |
| 20A | 黄 | 電動ウィンドウ、モーター |
| 25A | 無色/クリア | パワーシート |
| 30A | 緑 | 大電流用途 (モーター駆動に適切) |
| 35A | 青紫 | 大型モーター |
| 40A | オレンジ | 電動ファン |

### ヒューズ種類

| タイプ | 説明 | サイズ |
|--------|------|--------|
| ATO | 開放型 (Open)、標準サイズ | 19.1mm x 18.5mm x 5.1mm |
| ATC | 密閉型 (Closed)、標準サイズ | 19.1mm x 18.5mm x 5.1mm |
| Mini | 小型版 | 10.9mm x 16.3mm x 3.8mm |
| Maxi | 大型版 (色コードが異なる) | 29.2mm x 34.3mm x 9.2mm |

> **注意**: ATO/ATCは互換性あり。Maxiヒューズは色と定格の対応が異なるので注意

---

# 電圧関連まとめ

システム全体の電圧に関する情報を一覧にまとめます。

## 電圧一覧表

| 項目 | 電圧 | 備考 |
|------|------|------|
| **ODrive S1 動作電圧** | 12-48V (最大50.5V) | メイン電源入力 |
| **ODrive S1 ロジック電源** | 10-14V | オプション、12V IN |
| **絶縁IO電源 (V+ ISO)** | 3.3V または 5V | 外部から供給 |
| **センサー電源 (+5V)** | 5V | J11 Pin18から出力 |
| **DeWalt バッテリー満充電** | 21.0V | 4.2V × 5セル |
| **DeWalt バッテリー公称** | 18-20V | 通常使用範囲 |
| **DeWalt バッテリー低電圧** | 16.5V | 3.3V × 5セル |
| **Raspberry Pi** | 5V | DC-DC変換必要 |

## バッテリー別電圧設定早見表

| バッテリー | セル | 公称電圧 | 低電圧トリップ | 過電圧トリップ |
|------------|------|----------|----------------|----------------|
| DeWalt 20V | 5S | 18.5V | 16.5V | 21.25V |
| 6S LiPo | 6S | 22.2V | 19.8V | 25.5V |
| 7S LiPo | 7S | 25.9V | 23.1V | 29.75V |
| 10S LiPo | 10S | 37.0V | 33.0V | 42.5V |
| 12S LiPo | 12S | 44.4V | 39.6V | 50.5V (上限) |
| 24V鉛蓄電池 | - | 24V | 22V | 28V |
| 48V鉛蓄電池 | - | 48V | 44V | 50.5V (上限) |

> **計算式**:
> - 低電圧トリップ = 3.3V × セル数
> - 過電圧トリップ = 4.25V × セル数 (最大50.5V)

## 電圧保護の流れ

```
バッテリー → ヒューズ (30A) → ODrive S1
                              ↓
              ┌───────────────┴───────────────┐
              ↓                               ↓
     過電圧検出 (回生時)              低電圧検出 (放電時)
              ↓                               ↓
     ブレーキ抵抗器で消費              モーター停止
```

## 電圧監視ポイント

| 監視項目 | 方法 | 備考 |
|----------|------|------|
| バス電圧 | ODrive内蔵ADC | `odrv0.vbus_voltage`で確認 |
| セル電圧 | 外部リポチェッカー | バランスコネクタ接続 |
| 低電圧警告 | リポチェッカーブザー | 3.3V/セル設定推奨 |
| 過電圧保護 | ODrive内蔵 | 回生時に発動 |

---

# DC-DCコンバータ

> **公式ビルドガイド**: [BotWheel Explorer REV-B Hardware Build (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-REV-B-Hardware-Build-0eb19815a7b847a2a037a4246647d13c)
>
> 公式で使用されているDC-DCコンバータの詳細は上記ビルドガイドを参照してください。

## Raspberry Pi用電源変換

BotWheel ExplorerではRaspberry Piへの給電にDC-DCコンバータが必要です。

> **公式キット情報**: BotWheel ExplorerはRaspberry Pi 4を使用
>
> *出典: [BotWheel Explorer Kit](https://shop.odriverobotics.com/products/botwheel-explorer)*

| 項目 | 仕様 |
|------|------|
| 入力電圧 | 12-24V (バッテリー電圧) |
| 出力電圧 | 5V |
| 出力電流 | 3A以上推奨 (Pi 4), 5A推奨 (Pi 5) |
| 公式使用ボード | Raspberry Pi 4 |

### 推奨DC-DCモジュール例

以下はPololu等から入手可能な一般的なDC-DCモジュールの例です:

| モジュール | 出力 | 電流 | 入力範囲 | 参考リンク |
|------------|------|------|----------|------------|
| Pololu D24V60F5 | 5V | 6A | ~38V | [Pololu](https://www.pololu.com/product/2865) |
| Pololu D24V50F5 | 5V | 5A | ~38V | [Pololu](https://www.pololu.com/product/2851) |
| LM2596モジュール | 可変 | 3A | 4.5-40V | 汎用品 |

> **注意**: 公式で使用されている具体的な機種は[公式ビルドガイド](https://odriverobotics.notion.site/Botwheel-Explorer-REV-B-Hardware-Build-0eb19815a7b847a2a037a4246647d13c)を確認してください。

## 推奨DC-DCコンバータ仕様

| 項目 | 推奨仕様 |
|------|----------|
| タイプ | 降圧型 (Buck) |
| 効率 | 90%以上 |
| スイッチング周波数 | 150kHz以上 |
| 保護機能 | 過電流・短絡保護付き |
| 出力コネクタ | USB Type-C (Pi 5) / micro USB (Pi 4) |

## LM2596モジュール仕様例

| 項目 | 仕様 |
|------|------|
| 入力電圧範囲 | 4.5-40V |
| 出力電圧範囲 | 1.25-37V (可変) |
| 最大出力電流 | 3A |
| スイッチング周波数 | 150kHz |
| 効率 | 最大92% |
| サイズ | 約43mm x 21mm x 14mm |

---

# 電圧保護設定 (ODrive S1)

## 電圧トリップレベル

| パラメータ | 説明 | デフォルト値 |
|------------|------|--------------|
| `dc_bus_overvoltage_trip_level` | 過電圧トリップ | 26V (24V版) / 52V (48V版) |
| `dc_bus_undervoltage_trip_level` | 低電圧トリップ | 設定必要 |

## 設定例 (odrivetool)

```python
# 5S LiPoバッテリー (DeWalt 20V) の場合
bat_n_cells = 5

# 低電圧トリップ (3.3V/セル)
odrv0.config.dc_bus_undervoltage_trip_level = 3.3 * bat_n_cells  # = 16.5V

# 過電圧トリップ (4.25V/セル)
odrv0.config.dc_bus_overvoltage_trip_level = 4.25 * bat_n_cells  # = 21.25V

odrv0.save_configuration()
```

## 推奨設定値

| バッテリー | セル数 | 低電圧トリップ | 過電圧トリップ |
|------------|--------|----------------|----------------|
| DeWalt 20V | 5S | 16.5V | 21.25V |
| 6S LiPo | 6S | 19.8V | 25.5V |
| 24V鉛蓄電池 | - | 22V | 28V |
| 12S LiPo | 12S | 39.6V | 51.0V (最大50.5V) |

> **注意**: 過電圧トリップはODrive S1の最大定格50.5Vを超えて設定不可

## ブレーキ抵抗器設定 (回生制動時)

```python
# ブレーキ抵抗器の設定 (S1付属: 2Ω 50W)
odrv0.config.brake_resistor0.resistance = 2.0
odrv0.config.brake_resistor0.enable = True

# 電圧フィードバック (電源ダイオード使用時)
odrv0.config.enable_dc_bus_voltage_feedback = True
odrv0.config.dc_bus_voltage_feedback_ramp_start = 23.0  # 公称電圧+2V
odrv0.config.dc_bus_voltage_feedback_ramp_end = 27.0    # 公称電圧+6V

odrv0.save_configuration()
```

---

# 外部電圧アラーム (リポチェッカー)

## 1S-8S リポバッテリーチェッカー

バッテリーの過放電を防ぐため、外部電圧アラームの併用を推奨します。

| 項目 | 仕様 |
|------|------|
| 対応セル数 | 1S-8S |
| 対応バッテリー | LiPo, Li-ion, LiMn, LiFe |
| 電圧検出精度 | ±0.01V |
| セル電圧表示範囲 | 0.5-4.5V |
| 総電圧表示範囲 | 0.6-36V |
| サイズ | 約40 x 28 x 13mm |
| 重量 | 約12g |

## アラーム設定

| 項目 | 設定範囲 | 推奨値 |
|------|----------|--------|
| アラーム電圧 | 2.7-3.8V/セル (0.1V刻み) | 3.3V/セル |
| プリセット値 | 3.3V/セル | - |

## 動作

| 状態 | 動作 |
|------|------|
| 正常 | 電圧表示 |
| 低電圧検出 | ブザー音 + 赤LED点灯 |

## 接続方法

| 接続先 | 説明 |
|--------|------|
| バランスコネクタ | バッテリーのバランス端子に直接接続 |

> **注意**: DeWaltバッテリーはバランスコネクタが外部露出していないため、アダプタ経由での接続が必要な場合があります

---

# リンク集

## ハードウェアに関するリンク

| リンク | 説明 |
|--------|------|
| [ODrive S1 データシート](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html) | S1の詳細仕様・ピンアウト |
| [BotWheel Explorer ガイド](https://docs.odriverobotics.com/v/latest/guides/botwheel-explorer.html) | 組立・セットアップガイド |
| [ODrive S1 製品ページ](https://shop.odriverobotics.com/products/odrive-s1) | 購入ページ |
| [BotWheel 製品ページ](https://shop.odriverobotics.com/products/botwheels) | 購入ページ |
| [BotWheel Explorer Kit](https://shop.odriverobotics.com/products/botwheel-explorer) | キット購入ページ |
| [ハーネスビルドキット](https://shop.odriverobotics.com/products/harness-build-kit-for-odrive-s1) | 配線部品キット |

### 配線図

| リンク | 説明 |
|--------|------|
| [ハードウェアビルドガイド](https://docs.odriverobotics.com/v/latest/guides/botwheel-explorer.html) | 配線詳細はNotionページ参照 |
| [S1ピンアウト](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html) | コネクタピン配置 |
| [ハードウェア設定](https://docs.odriverobotics.com/v/latest/manual/hardware-config.html) | 電圧・ブレーキ設定 |

---

## ソフトウェアに関するリンク

| リンク | 説明 |
|--------|------|
| [ODrive ドキュメント](https://docs.odriverobotics.com/) | 公式ドキュメントトップ |
| [odrivetool](https://docs.odriverobotics.com/v/latest/interfaces/odrivetool.html) | CLI設定ツール |
| [Web GUI](https://gui.odriverobotics.com/) | ブラウザベース設定ツール |
| [CAN Bus ガイド](https://docs.odriverobotics.com/v/latest/guides/can-guide.html) | CANプロトコル詳細 |
| [UART ガイド](https://docs.odriverobotics.com/v/latest/manual/uart.html) | シリアル通信詳細 |
| [GitHub: ros_odrive](https://github.com/odriverobotics/ros_odrive) | ROS2パッケージ |
| [Python CAN パッケージ](https://dylanballback.github.io/ODriveCan/setup/odrive/setup/) | pyodrivecan セットアップ |

### Raspberry Pi セットアップ

| 手順 | コマンド/説明 |
|------|---------------|
| SPI有効化 | `raspi-config`でSPIを有効化 |
| can-utilsインストール | `sudo apt-get install can-utils` |
| CANインターフェース起動 | `sudo ip link set can0 up type can bitrate 1000000` |
| python-canインストール | `pip3 install python-can` |

### ODriveノードID設定

| ODrive | Node ID |
|--------|---------|
| 左側 | 0 |
| 右側 | 1 |

---

## 3D CAD・設計データ

| リンク | 説明 |
|--------|------|
| [ODrive S1 OnShape CAD](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html) | 公式3Dモデル (データシート内リンク) |
| [ODrive S1 エンクロージャ CAD](https://shop.odriverobotics.com/products/enclosure-for-odrive-s1) | ケース3Dモデル |
| [GrabCAD ODrive モデル](https://grabcad.com/library/tag/odrive) | コミュニティ作成モデル |

> **OnShape CADの利用方法**:
> 1. [ODrive S1 データシート](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html) にアクセス
> 2. "CAD" セクションのOnShapeリンクをクリック
> 3. OnShapeでSTEP/IGES等の形式でエクスポート可能
