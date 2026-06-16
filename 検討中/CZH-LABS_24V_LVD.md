# CZH-LABS 24V 30A LVD Module (検討中)

> [!NOTE]
> 24V系バッテリー (LiTime 24V LiFePO4 など) の過放電保護用 LVD モジュールの検討資料。
> Kit標準電源 (DeWalt 20V) 用の 18V LVD (OONO 18V 30A) は確定構成側の [低電圧カットオフモジュール (LVD) 技術資料](../LowVoltageDisconnect.md) を参照。
> 本案は [LiTime 24V LiFePO4バッテリー (検討中)](LiTime_24V_LiFePO4.md) を保護対象とする構成と連動する。

## 目次

1. [CZH-LABS 24V 30A LVD Module](#czh-labs-24v-30a-lvd-module)
2. [LiTime 24V LiFePO4 バッテリー用推奨設定](#litime-24v-lifepo4-バッテリー用推奨設定)
3. [24V LiFePO4 電圧-SOCチャート (参考)](#24v-lifepo4-電圧-socチャート-参考)
4. [24V LVD モジュール用 バッテリー別推奨設定](#24v-lvd-モジュール用-バッテリー別推奨設定)

> **関連資料**: [低電圧カットオフモジュール (LVD) 技術資料](../LowVoltageDisconnect.md) / [バッテリー技術資料](../Battery.md) / [LiTime 24V LiFePO4バッテリー (検討中)](LiTime_24V_LiFePO4.md)

---

## CZH-LABS 24V 30A LVD Module

> **購入リンク**: [Amazon.com](https://www.amazon.com/CZH-LABS-Electronics-Salon-Voltage-Disconnect-Protect/dp/B018TV7NQU) | [CZH-LABS公式](https://czh-labs.com/products/czh-labs-low-voltage-disconnect-module-lvd-24v-30a-protect-prolong-battery-life)

### 基本仕様

> **引用元**: [CZH-LABS 24V 30A LVD (公式)](https://czh-labs.com/products/czh-labs-low-voltage-disconnect-module-lvd-24v-30a-protect-prolong-battery-life)

| 項目 | 仕様 |
|------|------|
| 動作電圧範囲 | DC 18-32V |
| 定格電流 | 30A |
| 遅延時間 | 5秒 (電圧保持) |
| LED表示 | 緑/赤 デュアルカラー |
| 型番 | D-1021 / MD-D1021/24V-1 |

### 電圧設定 (DIPスイッチ)

| 項目 | 説明 |
|------|------|
| 設定方式 | DIPスイッチ |
| カットオフ電圧 | DIPスイッチで設定 (プログラマブル) |
| 再接続電圧 | DIPスイッチで設定 (プログラマブル) |

---

## LiTime 24V LiFePO4 バッテリー用推奨設定

> **引用元**: [BLUETTI LiFePO4 Voltage Chart](https://www.bluettipower.eu/blogs/news/lifepo4-voltage-chart), [LiTime 24V 50Ah製品ページ](https://jp.litime.com/products/24v-50ah-bluetooth)

| 項目 | 設定値 | 備考 |
|------|--------|------|
| カットオフ電圧 | 24.0V | 約10% SOC (3.0V × 8セル) |
| 再接続電圧 | 25.6V | 約20% SOC (3.2V × 8セル) |

> **注意**: 20V (0% SOC) まで放電するとバッテリー寿命が大幅に短くなります。10-20% SOCでカットオフすることを推奨します。

---

## 24V LiFePO4 電圧-SOCチャート (参考)

| SOC | 電圧 | 備考 |
|-----|------|------|
| 100% (充電中) | 29.2V | 充電完了電圧 |
| 100% (静止時) | 27.2V | フロート電圧 |
| 90% | 26.8V | |
| 80% | 26.6V | |
| 70% | 26.4V | |
| 60% | 26.1V | |
| 50% | 26.1V | 平坦領域 |
| 40% | 26.0V | |
| 30% | 25.8V | |
| 20% | 25.6V | 推奨再接続電圧 |
| 10% | 24.0V | 推奨カットオフ電圧 |
| 0% | 20.0V | 絶対下限 (非推奨) |

> **引用元**: [BLUETTI LiFePO4 Voltage Chart](https://www.bluettipower.eu/blogs/news/lifepo4-voltage-chart)

---

## 24V LVD モジュール用 バッテリー別推奨設定

> **引用元**: [Battery University - Lithium-ion Safety Concerns](https://batteryuniversity.com/article/bu-304a-safety-concerns-with-li-ion), [BLUETTI LiFePO4 Voltage Chart](https://www.bluettipower.eu/blogs/news/lifepo4-voltage-chart)

| バッテリー | セル構成 | カットオフ電圧 | 再接続電圧 | SOC目安 |
|------------|----------|----------------|------------|---------|
| 24V LiFePO4 | 8S LiFePO4 | 24.0V | 25.6V | 10-20% |
| 7S Li-ion | 7S Li-ion | 23.1V | 24.5V | 10-20% |
| 24V鉛蓄電池 | - | 22.0V | 24.0V | - |

> **計算式**:
>
> - Li-ion カットオフ = 3.3V × セル数 (約10% SOC)
> - LiFePO4 カットオフ = 3.0V × セル数 (約10% SOC)
> - 再接続電圧 = カットオフ電圧 + 1.5~2V

> [!NOTE]
> 共通の動作タイミング・保護機能・動作モード (AUTO/ON/OFF) は確定構成側の [LVD技術資料](../LowVoltageDisconnect.md) を参照 (OONO 18V とハードウェア仕様は共通)。
