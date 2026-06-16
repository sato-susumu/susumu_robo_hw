# LiTime 24V LiFePO4バッテリー (検討中)

> [!NOTE]
> BotWheel Explorer の電源候補として検討した LiFePO4 バッテリーの調査資料。
> Kit標準電源 (DeWalt 20V) とは別系統の **24V系・大容量** 案として検討中。確定構成は [バッテリー技術資料](../Battery.md) を参照。

## 目次

1. [LiTime 24V 50Ah Bluetooth付き](#litime-24v-50ah-bluetooth付き)
2. [比較: LiTime 24V 25Ah (電動工具用)](#比較-litime-24v-25ah-電動工具用)
3. [LiTime 24V 電圧設定](#litime-24v-電圧設定)

> **関連資料**: [バッテリー技術資料](../Battery.md) / [低電圧カットオフモジュール (LVD) 技術資料](../LowVoltageDisconnect.md)

---

## LiTime 24V 50Ah Bluetooth付き

> **購入リンク**: [LiTime公式](https://jp.litime.com/products/24v-50ah-bluetooth)
>
> 「小型船舶・船検適合品」エレキモーター用バッテリー

### 基本仕様

> **引用元**: [LiTime 24V 50Ah 製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

| 項目 | 仕様 |
|------|------|
| 容量 | 1280Wh |
| 定格電圧 | 25.6V |
| サイズ | 260 × 168 × 211 mm |
| 重量 | 9.6 kg |
| 防水等級 | IP65 |

### 対応・認証

> **引用元**: [LiTime 24V 50Ah 製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

| 項目 | 内容 |
|------|------|
| 対応モーター | 24V 70~100lb エレキモーター |
| 認証 | PSE, UN38.3, IEC62619 |

### 保護機能

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

### Bluetooth機能

> **引用元**: [LiTime 24V 50Ah 製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

| 項目 | 仕様 |
|------|------|
| Bluetooth | 5.0 |
| アプリ | LiTimeアプリ |
| 確認可能情報 | 充放電状態、残量、サイクル回数 |

### 価格

> **引用元**: [LiTime 24V 50Ah 製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth) (2024年時点の価格、変動あり)

| 項目 | 価格 |
|------|------|
| 公式価格 | ¥39,980 |
| 24V20A充電器 (オプション) | +¥19,082 |

> **備考**: ネット上にクーポンあり。公式が安い場合あり。

### 参考動画

| 内容 | リンク |
|------|--------|
| 別容量の分解動画 | [YouTube](https://www.youtube.com/watch?v=F_o5R5ewZZw) |
| 別電圧の分解動画 | [YouTube](https://www.youtube.com/watch?v=jR5MkFRSucc) |
| 別製品の動画 | [YouTube](https://www.youtube.com/watch?v=YEsXRusV_zY) |

---

## 比較: LiTime 24V 25Ah (電動工具用)

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

## LiTime 24V 電圧設定

> **引用元**: [Hardware Configuration - ODrive Documentation](https://docs.odriverobotics.com/v/latest/manual/hardware-config.html), [BLUETTI LiFePO4 Voltage Chart](https://www.bluettipower.eu/blogs/news/lifepo4-voltage-chart), [LiTime 24V 50Ah製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

| バッテリー | セル | 公称電圧 | 低電圧トリップ | 過電圧トリップ |
|------------|------|----------|----------------|----------------|
| **LiTime 24V 50Ah** | 8S LiFePO4 | 25.6V | 24.0V | 29.2V |

> **LiFePO4 計算式**:
>
> - 公称電圧 = 3.2V × セル数
> - 低電圧トリップ = 3.0V × セル数 (約10% SOC)
> - 過電圧トリップ = 3.65V × セル数 (最大50.5V)

### 電圧詳細

| 項目 | 電圧 | 備考 |
|------|------|------|
| **LiTime 24V 満充電** | 29.2V | 3.65V × 8セル (LiFePO4) |
| **LiTime 24V 公称** | 25.6V | 3.2V × 8セル |
| **LiTime 24V 低電圧** | 24.0V | 3.0V × 8セル (約10% SOC) |

> [!NOTE]
> ODrive S1 の動作電圧は 12-48V (最大50.5V)。LiTime 24V系 (24.0〜29.2V) はこの範囲内に収まる。
