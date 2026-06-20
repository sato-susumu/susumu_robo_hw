# バッテリー技術資料

---

## 目次

1. [BotWheel Explorer Kit 標準電源](#botwheel-explorer-kit-標準電源)
2. [マキタ 18V バッテリー仕様](#マキタ-18v-バッテリー仕様)
3. [バッテリー別電圧設定早見表](#バッテリー別電圧設定早見表)
4. [電圧関連まとめ](#電圧関連まとめ)
5. [電圧保護の流れ](#電圧保護の流れ)
6. [電圧監視ポイント](#電圧監視ポイント)
7. [利用ヒューズ](#利用ヒューズ)
8. [ブレードヒューズ色別規格](#ブレードヒューズ-atoatc-色別規格)

> **関連資料**: [低電圧カットオフモジュール (LVD) 技術資料](LowVoltageDisconnect.md) / [電源接続図 (BotWheel Explorer ベース)](Power_Wiring.md)
>
> **検討中の電源案**: [LiTime 24V LiFePO4バッテリー (検討中)](検討中/LiTime_24V_LiFePO4.md)

---

## BotWheel Explorer Kit 標準電源

BotWheel Explorer Kit の標準電源は **DeWalt 20V バッテリー** (5S Li-ion)。ODrive S1 の動作電圧範囲 (12-48V) に収まる。

### 電源仕様

> **引用元**: [BotWheel Explorer Kit - ODrive Shop](https://shop.odriverobotics.com/products/botwheel-explorer), [ODrive S1 Datasheet](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html)

| 項目 | 仕様 |
|------|------|
| 電圧範囲 | 12-48V (最大50.5V) |
| 標準バッテリー | DeWalt 20V (5S Li-ion, 16.5-21V) |
| 付属バッテリー容量 | 110Wh |
| バッテリータイプ | DeWalt DCB205等互換 |

### DeWalt 20V バッテリー仕様

> **引用元**: [DeWalt 20V MAX Battery System](https://www.dewalt.com/systems/cordless-platforms/20v), [BotWheel Explorer Required Components (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-Required-Components-c154381af2354fc185e7c71082be498e)

| 項目 | 仕様 |
|------|------|
| セル構成 | 5S (5直列) |
| 満充電電圧 | 21.0V (4.2V/セル) |
| 低電圧カットオフ | 16.5V (3.3V/セル) |
| 公称電圧 | 18-20V |

### DeWalt 20V バッテリーアダプター

> **購入リンク**: [Amazon](https://www.amazon.com/dp/B0CDGFXVLK)
>
> **引用元**: [Amazon製品ページ](https://www.amazon.com/dp/B0CDGFXVLK)

| 項目 | 仕様 |
|------|------|
| 対応バッテリー | DeWalt 20V (DCB205, DCB206, DCB204等) |
| 最大電流 | 20A |
| ワイヤー | 12AWG |
| 材質 | 耐熱ABS |

---

## マキタ 18V バッテリー仕様

> **引用元**: [マキタ BL1860B 製品ページ](https://www.makita.co.jp/product/li_batter_charg/bl1860b/bl1860b.html), [Amazon.co.jp BL1860B](https://www.amazon.co.jp/dp/B0194NE1A8)

| 項目 | 仕様 |
|------|------|
| 型番 | BL1860B |
| セル構成 | 5S2P (5直列2並列、18650 Li-ion / NMC) |
| 満充電電圧 | 21.0V (4.2V/セル) |
| 低電圧カットオフ | 15.0V (3.0V/セル) |
| 公称電圧 | 18V |
| 容量 | 6.0Ah / 108Wh |
| 重量 | 約 670 g |
| 寸法 | 約 113 × 75 × 62 mm |
| 充電時間 | 約55分 (急速充電器使用時) |

### 保護機能 (BMS)

> **引用元**: [マキタ BL1860B 製品ページ](https://www.makita.co.jp/product/li_batter_charg/bl1860b/bl1860b.html)

| 保護機能 | 内容 |
|----------|------|
| 過充電保護 | 4.2V/セル で充電停止 |
| 過放電保護 | 3.0V/セル でカットオフ |
| 過電流保護 | あり |
| 温度保護 | 過熱・低温時に充放電制限 |
| セルバランス | 各セルペアに個別バランス回路 |
| 残量表示 | LED 4段階表示 + 自己診断機能 |

---

## バッテリー別電圧設定早見表

> **引用元**: [Hardware Configuration - ODrive Documentation](https://docs.odriverobotics.com/v/latest/manual/hardware-config.html), [BLUETTI LiFePO4 Voltage Chart](https://www.bluettipower.eu/blogs/news/lifepo4-voltage-chart)

| バッテリー | セル | 公称電圧 | 低電圧トリップ | 過電圧トリップ |
|------------|------|----------|----------------|----------------|
| 12V LiFePO4 | 4S LiFePO4 | 12.8V | 12.0V | 14.6V |
| 48V LiFePO4 | 16S LiFePO4 | 51.2V | 48.0V | 50.5V (上限) |

> **LiFePO4 計算式 (参考)**:
>
> - 公称電圧 = 3.2V × セル数
> - 低電圧トリップ = 3.0V × セル数 (約10% SOC)
> - 過電圧トリップ = 3.65V × セル数 (最大50.5V)

---

## 電圧関連まとめ

> **引用元**: [ODrive S1 Datasheet](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html), [Raspberry Pi 4 Model B Specifications](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/)

システム全体の電圧に関する情報を一覧にまとめます。

### 電圧一覧表

| 項目 | 電圧 | 備考 |
|------|------|------|
| **ODrive S1 動作電圧** | 12-48V (最大50.5V) | メイン電源入力 |
| **ODrive S1 ロジック電源** | 10-14V | オプション、12V IN |
| **絶縁IO電源 (V+ ISO)** | 3.3V または 5V | 外部から供給 |
| **センサー電源 (+5V)** | 5V | J11 Pin18から出力 |
| **DeWalt バッテリー満充電** | 21.0V | 4.2V × 5セル (Li-ion) |
| **DeWalt バッテリー公称** | 18-20V | 通常使用範囲 |
| **DeWalt バッテリー低電圧** | 16.5V | 3.3V × 5セル |
| **マキタ バッテリー満充電** | 21.0V | 4.2V × 5セル (Li-ion) |
| **マキタ バッテリー公称** | 18V | 3.6V × 5セル |
| **マキタ バッテリー低電圧** | 15.0V | 3.0V × 5セル (BMS カットオフ) |
| **Raspberry Pi** | 5V | DC-DC変換必要 |

---

## 電圧保護の流れ

> **引用元**: [Hardware Configuration - ODrive Documentation](https://docs.odriverobotics.com/v/latest/manual/hardware-config.html)

```
バッテリー → ヒューズ (30A) → ODrive S1
                              ↓
              ┌───────────────┴───────────────┐
              ↓                               ↓
     過電圧検出 (回生時)              低電圧検出 (放電時)
              ↓                               ↓
     ブレーキ抵抗器で消費              モーター停止
```

---

## 電圧監視ポイント

> **引用元**: [odrivetool - ODrive Documentation](https://docs.odriverobotics.com/v/latest/interfaces/odrivetool.html)

| 監視項目 | 方法 | 備考 |
|----------|------|------|
| バス電圧 | ODrive内蔵ADC | `odrv0.vbus_voltage`で確認 |
| セル電圧 | 外部リポチェッカー | バランスコネクタ接続 |
| 低電圧警告 | リポチェッカーブザー | 3.3V/セル設定推奨 |
| 過電圧保護 | ODrive内蔵 | 回生時に発動 |

---

## 利用ヒューズ

> **公式ビルドガイド**: [BotWheel Explorer REV-B Hardware Build (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-REV-B-Hardware-Build-0eb19815a7b847a2a037a4246647d13c)
>
> 詳細な部品リストは公式ビルドガイドを参照してください。

| 項目 | 推奨仕様 |
|------|----------|
| メインヒューズ | 30A 自動車用ブレードヒューズ |
| ワイヤーゲージ | 12AWG (高電力用) |
| ヒューズホルダー | 防水ゴムキャップ付き推奨 |

---

## ブレードヒューズ (ATO/ATC) 色別規格

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

> **画像引用**: ブレードヒューズサイズ比較
>
> ![Blade Fuse Types](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Electrical_fuses%2C_blade_type.svg/500px-Electrical_fuses%2C_blade_type.svg.png)
>
> *出典: [Wikimedia Commons - Electrical fuses, blade type](https://commons.wikimedia.org/wiki/File:Electrical_fuses,_blade_type.svg)*
>
> 左から: Micro2, Micro3, Low-Profile Mini, Mini, ATO (標準), Maxi

| タイプ | 説明 | サイズ | 定格範囲 |
|--------|------|--------|----------|
| Micro2 | 超小型、2端子 | 9.1mm x 12.3mm x 4.0mm | 5-30A |
| Micro3 | 超小型、3端子 | 14.4mm x 12.3mm x 4.0mm | 5-15A |
| LP-Mini | 低背Mini | 10.9mm x 8.7mm x 3.8mm | 2-30A |
| Mini (ATM) | 小型版 | 10.9mm x 16.3mm x 3.8mm | 2-30A |
| ATO/ATC | 標準サイズ | 19.1mm x 18.5mm x 5.1mm | 0.5-40A |
| Maxi (APX) | 大型版 | 29.2mm x 34.3mm x 8.5mm | 20-120A |

> **BotWheel Explorer推奨**: ATO/ATC 30A (標準サイズ、緑色)
>
> **注意**: ATO/ATCは互換性あり。Maxiヒューズは色と定格の対応が異なるので注意
