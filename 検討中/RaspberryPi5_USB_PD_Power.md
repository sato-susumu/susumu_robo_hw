# Raspberry Pi 5 / USB-PD 電源変換 (検討中)

> [!NOTE]
> Raspberry Pi 5 への給電や USB-PD 対応デバイスへの給電を見据えた電源変換の検討資料。
> Kit標準の Buck コンバータ (Pi 4 用 5V) は確定構成側の [DC-DCコンバータ技術資料](../DCDC_Converter.md) を参照。
> 本案は [LiTime 24V LiFePO4バッテリー (検討中)](LiTime_24V_LiFePO4.md) を入力電源とする構成と連動する。

## 目次

1. [Raspberry Pi用電源変換 (Pi 4 / Pi 5)](#raspberry-pi用電源変換-pi-4--pi-5)
2. [Coolgear CG-PD200MAX (USB-PD対応)](#coolgear-cg-pd200max-usb-pd対応)
3. [配線例 (CG-PD200MAX使用時)](#配線例-cg-pd200max使用時)

> **関連資料**: [DC-DCコンバータ技術資料](../DCDC_Converter.md) / [バッテリー技術資料](../Battery.md) / [LiTime 24V LiFePO4バッテリー (検討中)](LiTime_24V_LiFePO4.md)

---

## Raspberry Pi用電源変換 (Pi 4 / Pi 5)

> **引用元**: [Raspberry Pi 4 Model B Specifications](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/), [Raspberry Pi 5 Power Requirements](https://www.raspberrypi.com/documentation/computers/raspberry-pi-5.html)

| 項目 | 仕様 |
|------|------|
| 入力電圧 | 12-24V (バッテリー電圧) |
| 出力電圧 | 5V |
| 出力電流 | 3A以上推奨 (Pi 4), 5A推奨 (Pi 5) |
| 使用ボード | Raspberry Pi 4 |

> **注意 (Raspberry Pi 5)**: Pi 5はUSB-PDプロトコルで5A供給可能か確認します。標準的なBuckコンバータはUSB-PDに対応していないため、Pi 5では電流制限がかかる場合があります。

---

## Coolgear CG-PD200MAX (USB-PD対応)

> **購入リンク**: [Coolgear製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input)

DC入力で動作する産業用USB-C PDチャージャーモジュール。Raspberry Pi 5などUSB-PD対応デバイスへの給電に最適。

### 基本仕様

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

### 出力プロファイル

> **引用元**: [Coolgear CG-PD200MAX製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input)

| 電圧 | 対応 |
|------|------|
| 5V | ○ |
| 9V | ○ |
| 12V | ○ |
| 15V | ○ |
| 20V | ○ |
| PPS | 3.3V〜21V (20mVステップ) |

### 対応プロトコル

> **引用元**: [Coolgear CG-PD200MAX製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input)

| プロトコル | 対応 |
|------------|------|
| USB PD 2.0 | ○ |
| USB PD 3.0 (PPS) | ○ |
| QC 2.0 / 3.0 / 4.0 | ○ |
| Apple 2.4A / DCP 1.5A | ○ |

### 保護機能

> **引用元**: [Coolgear CG-PD200MAX製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input)

| 保護種別 | 対応 |
|----------|------|
| 過電圧保護 | ○ |
| 低電圧保護 | ○ |
| 過電流保護 | ○ |
| 短絡保護 | ○ |
| ESDサージ保護 | 4kV |

### LiTime 24V LiFePO4バッテリーとの互換性

> **引用元**: [Coolgear CG-PD200MAX製品ページ](https://www.coolgear.com/product/chargeit-mini-200w-dual-type-c-pd-charger-100w-output-each-port-24v-input) (入力電圧範囲), [LiTime 24V 50Ah製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth) (バッテリー電圧)
>
> **関連資料**: [LiTime 24V LiFePO4バッテリー (検討中)](LiTime_24V_LiFePO4.md) - LiTime 24V LiFePO4の詳細仕様

| バッテリー状態 | 電圧 | CG-PD200MAX対応 |
|---------------|------|-----------------|
| 満充電時 | 29.2V | ○ (最大30V以内) |
| 公称時 | 25.6V | ○ (推奨範囲24〜28V) |
| 低充電時 | 20〜24V | △ (最小22V以上必要) |

> **注意**: バッテリーSOC 25%以下 (約26V未満) では動作可能だが、20V付近では電圧不足の可能性あり

---

## 配線例 (CG-PD200MAX使用時)

```
LiTime 24V LiFePO4バッテリー (25.6V公称)
    ↓
CG-PD200MAX入力 (ターミナルブロック)
    ↓
USB-C PD出力 (100W/ポート)
    ↓
Raspberry Pi 5 / ノートPC等
```
