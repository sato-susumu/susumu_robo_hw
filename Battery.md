# バッテリー技術資料

---

## 目次

1. [推奨電源仕様](#推奨電源仕様)
2. [DeWalt 20Vバッテリー仕様](#dewalt-20vバッテリー仕様)
3. [LiTime 24V LiFePO4バッテリー](#litime-24v-lifepo4バッテリー)
4. [バッテリー別電圧設定早見表](#バッテリー別電圧設定早見表)
5. [電圧関連まとめ](#電圧関連まとめ)
6. [電圧保護の流れ](#電圧保護の流れ)
7. [電圧監視ポイント](#電圧監視ポイント)
8. [利用ヒューズ](#利用ヒューズ)
9. [ブレードヒューズ色別規格](#ブレードヒューズ-atoatc-色別規格)

> **関連資料**: [低電圧カットオフモジュール (LVD) 技術資料](LowVoltageDisconnect.md)

---

## 推奨電源仕様

> **引用元**: [BotWheel Explorer Kit - ODrive Shop](https://shop.odriverobotics.com/products/botwheel-explorer), [ODrive S1 Datasheet](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html)

| 項目 | 仕様 |
|------|------|
| 電圧範囲 | 12-48V (最大50.5V) |
| 推奨バッテリー | DeWalt 20V (5S Li-ion, 16.5-21V) |
| 付属バッテリー容量 | 110Wh |
| バッテリータイプ | DeWalt DCB205等互換 |

---

## DeWalt 20Vバッテリー仕様

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

### キット内容

> **引用元**: [Amazon製品ページ](https://www.amazon.com/dp/B0CDGFXVLK)

| 部品 | 数量 |
|------|------|
| バッテリーアダプター | 2個 |
| スイッチ付きヒューズホルダー | 2個 |
| 30Aヒューズ | 6個 |
| 配線端子 | 2個 |

> **配線**: 赤=プラス、黒=マイナス

---

## LiTime 24V LiFePO4バッテリー

### LiTime 24V 50Ah Bluetooth付き

> **購入リンク**: [LiTime公式](https://jp.litime.com/products/24v-50ah-bluetooth)
>
> 「小型船舶・船検適合品」エレキモーター用バッテリー

#### 基本仕様

> **引用元**: [LiTime 24V 50Ah 製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

| 項目 | 仕様 |
|------|------|
| 容量 | 1280Wh |
| 定格電圧 | 25.6V |
| サイズ | 260 × 168 × 211 mm |
| 重量 | 9.6 kg |
| 防水等級 | IP65 |

#### 対応・認証

> **引用元**: [LiTime 24V 50Ah 製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

| 項目 | 内容 |
|------|------|
| 対応モーター | 24V 70~100lb エレキモーター |
| 認証 | PSE, UN38.3, IEC62619 |

#### 保護機能

> **引用元**: [LiTime 24V 50Ah 製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

| 保護機能 | 内容 |
|----------|------|
| 過充電保護 | あり |
| 過放電保護 | あり |
| 短絡保護 | あり |
| 過電流保護 | あり |
| 高温保護 | あり |
| 低温充電停止 | 0°C以下で自動停止 |
| 低温放電停止 | -20°C以下で自動停止 |

#### Bluetooth機能

> **引用元**: [LiTime 24V 50Ah 製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

| 項目 | 仕様 |
|------|------|
| Bluetooth | 5.0 |
| アプリ | LiTimeアプリ |
| 確認可能情報 | 充放電状態、残量、サイクル回数 |

#### 価格

> **引用元**: [LiTime 24V 50Ah 製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth) (2024年時点の価格、変動あり)

| 項目 | 価格 |
|------|------|
| 公式価格 | ¥39,980 |
| 24V20A充電器 (オプション) | +¥19,082 |

> **備考**: ネット上にクーポンあり。公式が安い場合あり。

#### 参考動画

| 内容 | リンク |
|------|--------|
| 別容量の分解動画 | [YouTube](https://www.youtube.com/watch?v=F_o5R5ewZZw) |
| 別電圧の分解動画 | [YouTube](https://www.youtube.com/watch?v=jR5MkFRSucc) |
| 別製品の動画 | [YouTube](https://www.youtube.com/watch?v=YEsXRusV_zY) |

---

### 比較: LiTime 24V 25Ah (電動工具用)

> **購入リンク**: [LiTime公式](https://jp.litime.com/products/litime-24v25ah)
>
> **引用元**: [LiTime 24V 50Ah](https://jp.litime.com/products/24v-50ah-bluetooth), [LiTime 24V 25Ah](https://jp.litime.com/products/litime-24v25ah) (2024年時点)

| 項目 | 24V 50Ah | 24V 25Ah |
|------|----------|----------|
| 容量 | 1280Wh | 640Wh |
| 電圧 | 25.6V | 25.6V |
| サイズ | 260×168×211mm | 195×166×172mm |
| 重量 | 9.6kg | 6.05kg |
| 価格 | ¥39,980 | ¥25,899 |
| Bluetooth | あり | なし |
| 用途 | エレキモーター | 電動工具 |

> **注意**: 容量が半分だが、サイズ・重量・価格の差は小さい

---

## バッテリー別電圧設定早見表

> **引用元**: [Hardware Configuration - ODrive Documentation](https://docs.odriverobotics.com/v/latest/manual/hardware-config.html), [BLUETTI LiFePO4 Voltage Chart](https://www.bluettipower.eu/blogs/news/lifepo4-voltage-chart), [LiTime 24V 50Ah製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

### Li-ion / LiPo バッテリー

| バッテリー | セル | 公称電圧 | 低電圧トリップ | 過電圧トリップ |
|------------|------|----------|----------------|----------------|
| DeWalt 20V | 5S Li-ion | 18.5V | 16.5V | 21.25V |
| 6S LiPo | 6S | 22.2V | 19.8V | 25.5V |
| 7S LiPo | 7S | 25.9V | 23.1V | 29.75V |
| 10S LiPo | 10S | 37.0V | 33.0V | 42.5V |
| 12S LiPo | 12S | 44.4V | 39.6V | 50.5V (上限) |

> **Li-ion/LiPo 計算式**:
>
> - 低電圧トリップ = 3.3V × セル数 (約10% SOC)
> - 過電圧トリップ = 4.25V × セル数 (最大50.5V)

### LiFePO4 バッテリー

| バッテリー | セル | 公称電圧 | 低電圧トリップ | 過電圧トリップ |
|------------|------|----------|----------------|----------------|
| **LiTime 24V 50Ah** | 8S LiFePO4 | 25.6V | 24.0V | 29.2V |
| 12V LiFePO4 | 4S LiFePO4 | 12.8V | 12.0V | 14.6V |
| 48V LiFePO4 | 16S LiFePO4 | 51.2V | 48.0V | 50.5V (上限) |

> **LiFePO4 計算式**:
>
> - 公称電圧 = 3.2V × セル数
> - 低電圧トリップ = 3.0V × セル数 (約10% SOC)
> - 過電圧トリップ = 3.65V × セル数 (最大50.5V)

### 鉛蓄電池

| バッテリー | 公称電圧 | 低電圧トリップ | 過電圧トリップ |
|------------|----------|----------------|----------------|
| 24V鉛蓄電池 | 24V | 22V | 28V |
| 48V鉛蓄電池 | 48V | 44V | 50.5V (上限) |

---

## 電圧関連まとめ

> **引用元**: [ODrive S1 Datasheet](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html), [Raspberry Pi 4 Model B Specifications](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/), [LiTime 24V 50Ah製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

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
| **LiTime 24V 満充電** | 29.2V | 3.65V × 8セル (LiFePO4) |
| **LiTime 24V 公称** | 25.6V | 3.2V × 8セル |
| **LiTime 24V 低電圧** | 24.0V | 3.0V × 8セル (約10% SOC) |
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
