# 低電圧カットオフモジュール (LVD) 技術資料

---

## 目次

1. [概要](#概要)
2. [製品ラインナップ](#製品ラインナップ)
3. [OONO 18V 30A LVD Module](#oono-18v-30a-lvd-module)
4. [共通仕様](#共通仕様)
5. [動作モード](#動作モード)
6. [バッテリー別推奨設定](#バッテリー別推奨設定)

> **検討中の電源案**: [CZH-LABS 24V 30A LVD Module (検討中)](検討中/CZH-LABS_24V_LVD.md) — 24V LiFePO4 (LiTime) 用 LVD

---

## 概要

> **引用元**: [OONO LVD (Amazon.com)](https://www.amazon.com/18V-30Amp-Voltage-Disconnect-Module/dp/B08H14XTZ8)

LVD (Low Voltage Disconnect) モジュールは、バッテリーの過放電を防ぐため、電圧が設定値以下になると自動で負荷を遮断する保護デバイスです。



---

## 製品ラインナップ

> **引用元**: [OONO 18V 30A (Amazon.com)](https://www.amazon.com/18V-30Amp-Voltage-Disconnect-Module/dp/B08H14XTZ8)

| 製品 | 対応電圧 | 定格電流 | 推奨バッテリー |
|------|----------|----------|----------------|
| OONO 18V 30A | DC 9-28V | 30A | DeWalt 20V (5S Li-ion) |

> **メーカー情報**: OONO、CZH-LABS、Electronics-Salon、Chunzehui は同系列ブランド (Xiken Technology Co., Ltd)
>
> **24V系の検討案**: 24V LiFePO4 用の [CZH-LABS 24V 30A LVD Module は検討中](検討中/CZH-LABS_24V_LVD.md)

---

## OONO 18V 30A LVD Module

> **購入リンク**: [Amazon.com](https://www.amazon.com/18V-30Amp-Voltage-Disconnect-Module/dp/B08H14XTZ8) | [Amazon.co.jp](https://www.amazon.co.jp/OONO-18V-30Amp-LVD-%E4%BD%8E%E9%9B%BB%E5%9C%A7%E5%88%87%E6%96%AD%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB/dp/B08H14XTZ8)

### 基本仕様

> **引用元**: [OONO 18V 30A LVD (Amazon.com)](https://www.amazon.com/18V-30Amp-Voltage-Disconnect-Module/dp/B08H14XTZ8)

| 項目 | 仕様 |
|------|------|
| 動作電圧範囲 | DC 9-28V |
| 定格電流 | 30A |
| 遅延時間 | 5秒 (電圧保持) |
| LED表示 | 緑/赤 デュアルカラー |

### 電圧設定 (DIPスイッチ)

> **引用元**: [OONO 18V 30A LVD (Amazon.com)](https://www.amazon.com/18V-30Amp-Voltage-Disconnect-Module/dp/B08H14XTZ8)

| 項目 | 説明 |
|------|------|
| 設定方式 | 赤色DIPスイッチ |
| カットオフ電圧 | DIPスイッチで設定 |
| 再接続電圧 | DIPスイッチで設定 |

> **設定ルール**: 再接続電圧 > カットオフ電圧 である必要あり
>
> **設定方法**: モジュール側面のラベルでDIPスイッチ設定値を確認
>
> **設定画像**: [Amazon.co.jp 製品ページ](https://www.amazon.co.jp/OONO-18V-30Amp-LVD-%E4%BD%8E%E9%9B%BB%E5%9C%A7%E5%88%87%E6%96%AD%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB/dp/B08H14XTZ8) でDIPスイッチ設定表を確認可能

### DeWalt 20V バッテリー用推奨設定

> **引用元**: [Battery University - Lithium-ion Discharge Guidelines](https://batteryuniversity.com/article/bu-808-how-to-prolong-lithium-based-batteries) (3.3V/セル推奨値)

| 項目 | 設定値 | 備考 |
|------|--------|------|
| カットオフ電圧 | 16.5V | 3.3V × 5セル |
| 再接続電圧 | 17.5V | カットオフ+1V程度 |

---

## 共通仕様

> **引用元**: [OONO 18V 30A LVD (Amazon.com)](https://www.amazon.com/18V-30Amp-Voltage-Disconnect-Module/dp/B08H14XTZ8) (同系列ブランドでシリーズ共通仕様)

### 動作タイミング

| 状態 | 動作 |
|------|------|
| 正常 | 緑LED点灯、負荷に給電 |
| 低電圧検出 (5秒継続) | 赤LED点灯、負荷を遮断 |
| 電圧復帰 (5秒継続) | 緑LED点灯、自動再接続 |

### 保護機能

| 機能 | 説明 |
|------|------|
| 過放電保護 | 設定電圧以下で自動遮断 |
| 自動復帰 | 電圧復帰時に自動再接続 |
| 手動オーバーライド | 緊急時の強制ON/OFF |

---

## 動作モード

> **引用元**: [OONO 18V 30A LVD (Amazon.com)](https://www.amazon.com/18V-30Amp-Voltage-Disconnect-Module/dp/B08H14XTZ8) (同系列ブランドでシリーズ共通仕様)

ロッカースイッチで動作モードを切り替えます。

| モード | 説明 | 用途 |
|--------|------|------|
| AUTO | 電圧に応じて自動ON/OFF | 通常運用 |
| ON | 強制ON (電圧監視無効) | 緊急時、テスト時 |
| OFF | 強制OFF | メンテナンス、長期保管 |

> **注意**: LED自体の消費電流があるため、長期保管時はバッテリーを外すか、OFFモードにしてください

---

## バッテリー別推奨設定

> **引用元**: [Battery University - Lithium-ion Safety Concerns](https://batteryuniversity.com/article/bu-304a-safety-concerns-with-li-ion), [BLUETTI LiFePO4 Voltage Chart](https://www.bluettipower.eu/blogs/news/lifepo4-voltage-chart)

### 18V LVD モジュール用

| バッテリー | セル構成 | カットオフ電圧 | 再接続電圧 |
|------------|----------|----------------|------------|
| DeWalt 20V | 5S Li-ion | 16.5V | 17.5V |
| 6S LiPo | 6S Li-ion | 19.8V | 21.0V |

> **計算式**:
>
> - Li-ion カットオフ = 3.3V × セル数 (約10% SOC)
> - LiFePO4 カットオフ = 3.0V × セル数 (約10% SOC)
> - 再接続電圧 = カットオフ電圧 + 1.5~2V
>
> **24V系**: 24V LiFePO4 / 7S Li-ion / 24V鉛蓄電池の推奨設定は [CZH-LABS 24V 30A LVD Module (検討中)](検討中/CZH-LABS_24V_LVD.md) を参照

