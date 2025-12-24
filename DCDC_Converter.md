# DC-DCコンバータ技術資料

---

## 目次

1. [概要](#概要)
2. [使用製品](#使用製品)
   - [5V出力 Buckコンバータ](#dc-12v24v-to-5v-6a-30w-dual-usb-c-buck-converter)
   - [Coolgear CG-PD200MAX (USB-PD対応)](#coolgear-cg-pd200max-usb-pd対応)
3. [Raspberry Pi用電源変換](#raspberry-pi用電源変換)
4. [配線例](#配線例)
5. [関連リンク](#関連リンク)

---

## 概要

> **公式部品リスト**: [BotWheel Explorer Required Components (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-Required-Components-c154381af2354fc185e7c71082be498e)

BotWheel Explorerでは、バッテリー電圧 (12-24V) からRaspberry Pi用に5V電源を供給するためにDC-DCコンバータが必要です。

---

## 使用製品

### DC 12V/24V to 5V 6A 30W Dual USB-C Buck Converter

> **購入リンク**: [Amazon](https://www.amazon.com/Converter-Charging-Compatible-Raspberry-Cellphone/dp/B0BCP86XPY)

#### 入出力仕様

> **引用元**: [Amazon製品ページ](https://www.amazon.com/Converter-Charging-Compatible-Raspberry-Cellphone/dp/B0BCP86XPY)

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

> **引用元**: [Amazon製品ページ](https://www.amazon.com/Converter-Charging-Compatible-Raspberry-Cellphone/dp/B0BCP86XPY)

| 項目 | 仕様 |
|------|------|
| 出力ポート | USB Type-C × 2 |
| USB-Cケーブル長 | 31cm (12.2インチ) |
| 防水等級 | IP68 |

#### 保護機能

> **引用元**: [Amazon製品ページ](https://www.amazon.com/Converter-Charging-Compatible-Raspberry-Cellphone/dp/B0BCP86XPY)

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

> **引用元**: [Raspberry Pi 4 Model B Specifications](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/), [Raspberry Pi 5 Power Requirements](https://www.raspberrypi.com/documentation/computers/raspberry-pi-5.html)

| 項目 | 仕様 |
|------|------|
| 入力電圧 | 12-24V (バッテリー電圧) |
| 出力電圧 | 5V |
| 出力電流 | 3A以上推奨 (Pi 4), 5A推奨 (Pi 5) |
| 使用ボード | Raspberry Pi 4 |

> **注意 (Raspberry Pi 5)**: Pi 5はUSB-PDプロトコルで5A供給可能か確認します。標準的なBuckコンバータはUSB-PDに対応していないため、Pi 5では電流制限がかかる場合があります。

---

### Coolgear CG-PD200MAX (USB-PD対応)

> **購入リンク**: [Coolgear製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input)

DC入力で動作する産業用USB-C PDチャージャーモジュール。Raspberry Pi 5などUSB-PD対応デバイスへの給電に最適。

#### 基本仕様

> **引用元**: [Coolgear CG-PD200MAX製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input)

| 項目 | 仕様 |
|------|------|
| 型番 | CG-PD200MAX |
| メーカー | Coolgear Inc. |
| 合計出力 | 200W (各ポート100W) |
| ポート数 | USB Type-C × 2 (スクリューロック対応) |
| 入力電圧 | DC 24-28V (最小22V〜最大30V) |
| 入力コネクタ | 2ピンターミナルブロック |
| 動作温度 | 0°C〜55°C |
| サイズ | 120.7 × 63.5 × 38.1 mm |
| 重量 | 約136g |
| 筐体 | 金属シャーシ |

#### 出力プロファイル

> **引用元**: [Coolgear CG-PD200MAX製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input)

| 電圧 | 対応 |
|------|------|
| 5V | ○ |
| 9V | ○ |
| 12V | ○ |
| 15V | ○ |
| 20V | ○ |
| PPS | 3.3V〜21V (20mVステップ) |

#### 対応プロトコル

> **引用元**: [Coolgear CG-PD200MAX製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input)

| プロトコル | 対応 |
|------------|------|
| USB PD 2.0 | ○ |
| USB PD 3.0 (PPS) | ○ |
| QC 2.0 / 3.0 / 4.0 | ○ |
| Apple 2.4A / DCP 1.5A | ○ |

#### 保護機能

> **引用元**: [Coolgear CG-PD200MAX製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input)

| 保護種別 | 対応 |
|----------|------|
| 過電圧保護 | ○ |
| 低電圧保護 | ○ |
| 過電流保護 | ○ |
| 短絡保護 | ○ |
| ESDサージ保護 | 4kV |

#### LiTime 24V LiFePO4バッテリーとの互換性

> **引用元**: [Coolgear CG-PD200MAX製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input) (入力電圧範囲), [LiTime 24V 50Ah製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth) (バッテリー電圧)
>
> **関連資料**: [バッテリー技術資料](Battery.md) - LiTime 24V LiFePO4の詳細仕様

| バッテリー状態 | 電圧 | CG-PD200MAX対応 |
|---------------|------|-----------------|
| 満充電時 | 29.2V | ○ (最大30V以内) |
| 公称時 | 25.6V | ○ (推奨範囲24〜28V) |
| 低充電時 | 20〜24V | △ (最小22V以上必要) |

> **注意**: バッテリーSOC 25%以下 (約26V未満) では動作可能だが、20V付近では電圧不足の可能性あり

---

## 配線例

### 5V Buckコンバータ使用時

```
バッテリー (20V)
    ↓
DC-DC入力 (VIN+, VIN-)
    ↓
DC-DC出力 (USB-C)
    ↓
Raspberry Pi 電源
```

### CG-PD200MAX使用時

```
LiTime 24V LiFePO4バッテリー (25.6V公称)
    ↓
CG-PD200MAX入力 (ターミナルブロック)
    ↓
USB-C PD出力 (100W/ポート)
    ↓
Raspberry Pi 5 / ノートPC等
```

---

## 関連リンク

| リンク | 説明 |
|--------|------|
| [5V Buckコンバータ (Amazon)](https://www.amazon.com/Converter-Charging-Compatible-Raspberry-Cellphone/dp/B0BCP86XPY) | Raspberry Pi 4向け |
| [Coolgear CG-PD200MAX](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input) | USB-PD 200W出力 |
| [LiTime 24Vバッテリー](https://jp.litime.com/collections/litime-24v-batteries) | 入力電源オプション |
| [Raspberry Pi 4 Specifications](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/) | 電源要件 |
