# DC-DCコンバータ技術資料

---

## 目次

1. [概要](#概要)
2. [使用製品](#使用製品)
3. [Raspberry Pi用電源変換](#raspberry-pi用電源変換)
4. [配線例](#配線例)

---

## 概要

> **公式部品リスト**: [BotWheel Explorer Required Components (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-Required-Components-c154381af2354fc185e7c71082be498e)

BotWheel Explorerでは、バッテリー電圧 (12-24V) からRaspberry Pi用に5V電源を供給するためにDC-DCコンバータが必要です。

---

## 使用製品

### DC 12V/24V to 5V 6A 30W Dual USB-C Buck Converter

> **購入リンク**: [Amazon](https://www.amazon.com/Converter-Charging-Compatible-Raspberry-Cellphone/dp/B0BCP86XPY)

#### 入出力仕様

| 項目 | 仕様 |
|------|------|
| 入力電圧範囲 | DC 10-32V |
| 出力電圧 | DC 5V |
| 総出力電流 | 6A (最大) |
| ポート別出力電流 | 3A (最大/ポート) |
| 総出力電力 | 30W (最大) |
| ポート別出力電力 | 15W (最大/ポート) |
| 変換効率 | 最大96% |

#### 物理仕様

| 項目 | 仕様 |
|------|------|
| 出力ポート | USB Type-C × 2 |
| USB-Cケーブル長 | 31cm (12.2インチ) |
| 防水等級 | IP68 |

#### 保護機能

| 保護機能 | 内容 |
|----------|------|
| 入力逆接続保護 | あり |
| 入力過電圧保護 | あり |
| 入力低電圧保護 | あり |
| 出力過電流保護 | あり |
| 出力過電圧保護 | あり |
| 出力低電圧保護 | あり |
| 短絡保護 | あり |
| 過熱保護 | あり |

#### 特徴

- デュアルUSB-C出力で2台同時給電可能 (各ポート3A/15W)
- 降圧型 (Buck) コンバータ
- IP68防水で屋外使用可能
- Raspberry Pi 4に最適

---

## Raspberry Pi用電源変換

| 項目 | 仕様 |
|------|------|
| 入力電圧 | 12-24V (バッテリー電圧) |
| 出力電圧 | 5V |
| 出力電流 | 3A以上推奨 (Pi 4), 5A推奨 (Pi 5) |
| 使用ボード | Raspberry Pi 4 |

> **注意 (Raspberry Pi 5)**: Pi 5はUSB-PDプロトコルで5A供給可能か確認します。標準的なBuckコンバータはUSB-PDに対応していないため、Pi 5では電流制限がかかる場合があります。

---

## 配線例

```
バッテリー (20V)
    ↓
DC-DC入力 (VIN+, VIN-)
    ↓
DC-DC出力 (USB-C)
    ↓
Raspberry Pi 電源
```

