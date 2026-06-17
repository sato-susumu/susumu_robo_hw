# Anker Prime Power Bank (27650mAh, 250W) 技術資料

> **引用元**: [Anker Prime Power Bank (27650mAh, 250W) 製品ページ (Anker Japan)](https://www.ankerjapan.com/products/a1340)

> [!NOTE]
> 本資料は**検討段階**の資料です。採用が確定した場合はリポジトリ直下に移動します。

## 目次

- [製品概要](#製品概要)
- [容量・出力仕様](#容量出力仕様)
- [入力 (充電) 仕様](#入力充電仕様)
- [ポート構成](#ポート構成)
- [機能](#機能)
- [外形・物理仕様](#外形物理仕様)
- [本構成での想定用途](#本構成での想定用途)

---

## 製品概要

Anker Prime Power Bank (27650mAh, 250W) [型番 A1340] は、大容量・超高出力のモバイルバッテリー。USB-C × 2 + USB-A × 1 の3ポートで合計最大250W出力に対応し、ノートPC級の機器も給電可能。LEDディスプレイで残量・充電時間をリアルタイム表示し、Ankerアプリ連携にも対応する。

> **引用元**: [Anker Prime Power Bank 製品ページ](https://www.ankerjapan.com/products/a1340)

---

## 容量・出力仕様

| 項目 | 仕様 |
|------|------|
| バッテリー容量 | 27,650 mAh |
| 合計最大出力 | 250 W (3ポート合計) |
| USB-C1 / C2 | 各最大 140 W |
| USB-A | 最大 65 W |
| 対応規格 | USB PD (Power Delivery)、PPS、PowerIQ 3.0 (Gen2) |

> **引用元**: [Anker Prime Power Bank 製品ページ](https://www.ankerjapan.com/products/a1340)

---

## 入力 (充電) 仕様

| 項目 | 仕様 |
|------|------|
| USB-C1 / C2 入力 | 各最大 140 W |
| 合計最大入力 | 170 W (C1+C2 同時入力時) |
| 専用充電スタンド | 最大 99 W |

> **引用元**: [Anker Prime Power Bank 製品ページ](https://www.ankerjapan.com/products/a1340) / [楽天市場 アンカー・ダイレクト](https://item.rakuten.co.jp/anker/a1340/)

---

## ポート構成

| ポート | 数 | 最大出力 |
|--------|-----|----------|
| USB-C | 2 | 各 140 W |
| USB-A | 1 | 65 W |

> **引用元**: [Anker Prime Power Bank 製品ページ](https://www.ankerjapan.com/products/a1340)

---

## 機能

- LEDディスプレイ搭載 (バッテリー残量・充電時間をリアルタイム表示)
- Ankerアプリ連携 (充電最適化)
- USB PD 3.1 / PPS 対応
- PSE技術基準適合

> **引用元**: [Anker Prime Power Bank 製品ページ](https://www.ankerjapan.com/products/a1340) / [楽天市場 アンカー・ダイレクト](https://item.rakuten.co.jp/anker/a1340/)

---

## 外形・物理仕様

| 項目 | 仕様 |
|------|------|
| サイズ | 約 162 × 57 × 50 mm |
| 重量 | 約 665 g |

> **引用元**: [Anker Prime Power Bank 製品ページ](https://www.ankerjapan.com/products/a1340)

---

## 本構成での想定用途

- 母艦PC [MINISFORUM UM790 Pro](MINISFORUM_UM790Pro.md) への給電 (USB-C PD 最大140W → 120W付属アダプタ相当をカバー、DCトリガーケーブル併用)
- [Raspberry Pi 5](RaspberryPi5_USB_PD_Power.md) 等のUSB-PD機器への給電
- 開発・デバッグ時のポータブル電源、ロボット系統 (DeWalt 20V / 24V系) とは別系統の補助電源

> [!NOTE]
> USB-C PD最大140Wは、UM790 Proの付属アダプタ (19V/120W) を上回るため給電能力上は十分。ただしDC給電にはPDトリガー (19V出力) ケーブルが別途必要。容量27,650mAh ≒ 約100Wh のため、機内持込・運用時間の目安として把握しておく。

> **関連**: 別系統の電源検討として [24V系電源 (LiTime)](LiTime_24V_LiFePO4.md) 、Kit標準電源は確定構成の [Battery.md](../Battery.md) を参照。
