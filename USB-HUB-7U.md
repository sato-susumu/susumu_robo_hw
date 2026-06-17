# Waveshare USB-HUB-7U 技術資料

> **引用元**: [Waveshare USB-HUB-7U 製品ページ](https://www.waveshare.com/usb-hub-7u.htm) / [Waveshare Wiki](https://www.waveshare.com/wiki/USB-HUB-7U)

## 目次

- [製品概要](#製品概要)
- [基本仕様](#基本仕様)
- [電源仕様](#電源仕様)
- [保護機能](#保護機能)
- [外形・物理仕様](#外形物理仕様)
- [本構成での想定用途](#本構成での想定用途)

---

## 製品概要

Waveshare USB-HUB-7Uは、工業グレードの7ポートUSBハブ。MTT (Multiple Transaction Translator) 技術を採用し、7台のUSB機器を同時に安定動作させられる。金属筐体・各ポートのESD保護・過電圧保護を備え、ロボットや産業機器など多数のUSBデバイスを束ねる用途に適する。

> **引用元**: [Waveshare USB-HUB-7U 製品ページ](https://www.waveshare.com/usb-hub-7u.htm)

---

## 基本仕様

| 項目 | 仕様 |
|------|------|
| ポート数 | 7ポート (USB Type-A) |
| USB規格 | USB 2.0 / 1.1 互換 |
| ハブチップ | 工業グレードHUBチップ + MTT技術 |
| 付属ケーブル | USBケーブル 約 1.2 m |

> **引用元**: [Waveshare USB-HUB-7U 製品ページ](https://www.waveshare.com/usb-hub-7u.htm)

> [!NOTE]
> USB 2.0仕様 (最大480 Mbps) のため、高帯域を要する [Intel RealSense D435i](RealSense_D435i.md) (USB 3.0) のフルスペック動作には非対応。マウス・キーボード・低速シリアル・小型周辺機器の集約に向く。

---

## 電源仕様

| 項目 | 仕様 |
|------|------|
| 各ポート最大出力電流 | 1.2 A (十分な電源入力がある場合) |
| 付属電源 | 5V 2A |
| 推奨電源 | 5V 4A 以上 (高負荷時) |

> **引用元**: [Waveshare USB-HUB-7U 製品ページ](https://www.waveshare.com/usb-hub-7u.htm)

---

## 保護機能

- 各USBポートのESD保護
- 過電圧保護
- 工業グレード金属筐体

> **引用元**: [Waveshare USB-HUB-7U 製品ページ](https://www.waveshare.com/usb-hub-7u.htm)

---

## 外形・物理仕様

| 項目 | 仕様 |
|------|------|
| 外形寸法 | 138 × 51 × 21 mm (L × W × H) |
| 重量 | 336 g |
| 筐体 | 工業グレード金属ケース (取付穴あり) |

> **引用元**: [Waveshare USB-HUB-7U 製品ページ](https://www.waveshare.com/usb-hub-7u.htm) / [RobotShop 製品ページ](https://www.robotshop.com/products/industrial-grade-usb-hub-7x-usb-20-ports-us-plug)

---

## 本構成での想定用途

- ロボット母艦 [MINISFORUM UM790 Pro](MINISFORUM_UM790Pro.md) / [Raspberry Pi](検討中/RaspberryPi4.md) に対し、多数のUSBデバイス (マイク・センサ・シリアル変換器等) を集約
- 取付穴・金属筐体により車体への固定が容易
- ESD/過電圧保護で移動体環境での安定動作を期待

> [!NOTE]
> 各ポート1.2A・推奨5V 4A以上のため、多数のバスパワー機器を接続する場合は外部電源 (セルフパワー) で運用する。USB 2.0帯域である点に留意し、高帯域カメラは母艦のUSB 3.0/USB4ポートに直結する。
