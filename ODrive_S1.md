# ODrive S1 技術資料

---

## 目次

1. [電気的仕様](#電気的仕様)
2. [物理的仕様](#物理的仕様)
3. [通信インターフェース](#通信インターフェース)
4. [ブレーキ抵抗器](#ブレーキ抵抗器)
5. [端子・ピンアウト](#端子ピンアウト)
   - [ピンアウト図](#ピンアウト図)
   - [コネクタ一覧](#コネクタ一覧)
   - [電源パッド配置](#電源パッド配置)
   - [J11 統合I/Oヘッダー (30ピン)](#j11-統合ioヘッダー-30ピン)
   - [J16/J17 CANヘッダー](#j16j17-canヘッダー)
   - [GPIO特性](#gpio特性)
6. [電圧保護設定](#電圧保護設定)

---

## 電気的仕様

> **引用元**: [ODrive S1 Datasheet](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html), [ODrive S1 製品ページ](https://shop.odriverobotics.com/products/odrive-s1)

| 項目 | 仕様 |
|------|------|
| 動作電圧 | 12-48V (最大50.5V) |
| 連続電流 | 40A (自由空気) / 80A (ヒートスプレッダー装着時) |
| 連続出力 | 2kW |
| PWM周波数 | 24kHz |
| 制御ループ周波数 | 8kHz (電流制御ループ24kHz予定) |
| 最大電気周波数 | 700Hz (2000Hz対応予定) |
| ロジック電源入力 (オプション) | 10-14V |

## 物理的仕様

> **引用元**: [ODrive S1 製品ページ](https://shop.odriverobotics.com/products/odrive-s1)

| 項目 | 仕様 |
|------|------|
| 基板サイズ | 66mm x 50mm |
| 質量 (端子なし) | 35g |
| 質量 (端子あり) | 55g |



## 通信インターフェース

> **引用元**: [ODrive S1 Datasheet - ODrive Documentation](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html)

| インターフェース | 仕様 |
|------------------|------|
| CAN | 2.0B @ 1Mbps (CAN-FD 5Mbps実験的サポート) |
| USB | USB 2.0 |
| UART | 絶縁、3.3V/5V対応 |
| STEP/DIR | 絶縁、ステッピングモーター互換 |
| PWM入力 | RC受信機対応 |
| アナログ入力 | 電圧入力による制御 |

## ブレーキ抵抗器

> **引用元**: [ODrive S1 Datasheet - ODrive Documentation](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html)

| 項目 | 仕様 |
|------|------|
| 付属抵抗器 | 2Ω 50W |
| ピーク回生電力 | 2000W |
| オンボードチョッパ | 搭載 |

---

# 端子・ピンアウト

> **引用元**: [ODrive S1 Datasheet - ODrive Documentation](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html)
>
> 以下の端子情報は公式データシートからの引用です。最新情報は公式ドキュメントを参照してください。

## ピンアウト図

> **画像引用**: ODrive S1 Pinout Diagram
>
> ![ODrive S1 Pinout](https://docs.odriverobotics.com/v/latest/_images/s1_pinout.png)
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

> **詳細**: [CAN Bus Guide](https://docs.odriverobotics.com/v/latest/guides/can-guide.html)

| ピン | 名称 | 機能 |
|------|------|------|
| 1 | CAN_H | CAN High |
| 2 | CAN_L | CAN Low |
| 3 | GND NC | GND (デイジーチェーン用、内部未接続) |
| 4 | GND NC | GND (デイジーチェーン用、内部未接続) |

> **公式情報**: J16/J17のGNDピンは内部でODriveに接続されておらず、デイジーチェーン用途のみ。グラウンドループを作らずにCANバスのGNDを接続可能。

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

# 電圧保護設定

> **引用元**: [Hardware Configuration - ODrive Documentation](https://docs.odriverobotics.com/v/latest/manual/hardware-config.html)

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

