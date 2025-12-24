# フェルール (棒端子) 技術資料

---

## 目次

1. [概要](#概要)
2. [DIN 46228 色コード規格](#din-46228-色コード規格)
3. [サイズ別寸法仕様](#サイズ別寸法仕様)
4. [AWGとmm²の対応表](#awgとmm²の対応表)
5. [2本用ツインフェルール](#2本用ツインフェルール)
6. [BotWheel Explorerでの使用](#botwheel-explorerでの使用)
7. [関連リンク](#関連リンク)

---

## 概要

> **引用元**: [Electric wire ferrule - Wikipedia](https://en.wikipedia.org/wiki/Electric_wire_ferrule), [DIN 46228 Ferrule Standards](https://www.ferrulesdirect.com/pages/ferrule-documents)

フェルール (棒端子、ワイヤーエンドスリーブ) は、より線を束ねてスクリュー端子に確実に接続するための圧着端子です。

---

## DIN 46228 色コード規格

> **引用元**: [DIN 46228 Teil 4](https://www.knipex.com/), [Ferrule Color Code Standards](https://www.americanelectrical.com/blog/cracking-the-codes-for-insulated-wire-ferrules/)

DIN (ドイツ工業規格) 46228 Part 4 に基づく色分けです。

### 標準色コード表

| サイズ (mm²) | AWG相当 | DIN色 | 備考 |
|--------------|---------|-------|------|
| 0.14 | 26 | グレー | 極細線用 |
| 0.25 | 24 | ライトブルー | 信号線 |
| 0.34 | 22 | ターコイズ | - |
| 0.5 | 20 | オレンジ | - |
| 0.75 | 18 | 白/グレー | - |
| 1.0 | 18-17 | 赤 | - |
| 1.5 | 16 | 黒 | - |
| 2.5 | 14 | 青 | - |
| 4.0 | 12 | グレー | - |
| 6.0 | 10 | 黄 | - |
| 10.0 | 8 | 赤 | 大電力 |
| 16.0 | 6 | 青 | 大電力 |
| 25.0 | 4 | 黒 | 大電力 |
| 35.0 | 2 | 赤 | 大電力 |
| 50.0 | 1/0 | 青 | 大電力 |

> **注意**: DIN、T、W の3種類のカラーコード規格があり、メーカーによって異なる場合があります。

---

## サイズ別寸法仕様

> **引用元**: [Knipex DIN 46228/4 Specifications](https://web-assets.knipex.com/sites/default/files/documents/AEH-HUELSEN-UBERSICHT_EN_V01_RZ20210624.PDF)

### 寸法定義

```
    ←─── L1 (全長) ───→
    ┌──────────────────┐
    │  絶縁カラー      │  金属スリーブ
    │  ┌──────────────┼──────────────┐
    │  │              │              │
    │  │     d2       │     d1       │
    │  │   (外径)     │   (内径)     │
    │  │              │              │
    │  └──────────────┼──────────────┘
    └──────────────────┘
        ←── L2 (金属部長さ) ──→
```

### 絶縁付きフェルール寸法表 (DIN 46228 Part 4)

| サイズ (mm²) | L1 全長 (mm) | L2 金属部 (mm) | d1 内径 (mm) | d2 外径 (mm) |
|--------------|--------------|----------------|--------------|--------------|
| 0.25 | 12.0 | 6.0 | 0.8 | 2.0 |
| 0.34 | 12.0 | 6.0 | 0.9 | 2.2 |
| 0.5 | 14.0 | 8.0 | 1.0 | 2.6 |
| 0.75 | 14.0 | 8.0 | 1.2 | 2.8 |
| 1.0 | 14.0 | 8.0 | 1.4 | 3.0 |
| 1.5 | 14.0 | 8.0 | 1.7 | 3.5 |
| 2.5 | 14.0 | 8.0 | 2.2 | 4.2 |
| 4.0 | 17.0 | 10.0 | 2.8 | 4.8 |
| 6.0 | 18.0 | 12.0 | 3.4 | 5.8 |
| 10.0 | 22.0 | 12.0 | 4.6 | 7.0 |
| 16.0 | 27.0 | 18.0 | 5.8 | 8.8 |
| 25.0 | 32.0 | 22.0 | 7.3 | 10.5 |

### 材質

| 項目 | 仕様 |
|------|------|
| スリーブ材質 | E-Copper (電気銅) |
| 表面処理 | 電解錫メッキ (厚さ 3μm以上) |
| 絶縁材質 | PP (ポリプロピレン) または PA (ナイロン) |

---

## AWGとmm²の対応表

> **引用元**: [American Wire Gauge - Wikipedia](https://en.wikipedia.org/wiki/American_wire_gauge), [DIN 46228 Ferrule Standards](https://www.ferrulesdirect.com/pages/ferrule-documents)

| AWG | mm² (公称) | mm² (実際) | 推奨フェルール |
|-----|------------|------------|----------------|
| 26 | 0.14 | 0.13 | 0.14 mm² |
| 24 | 0.25 | 0.20 | 0.25 mm² |
| 22 | 0.34 | 0.33 | 0.34 mm² |
| 20 | 0.5 | 0.52 | 0.5 mm² |
| 18 | 0.75 | 0.82 | 1.0 mm² |
| 16 | 1.5 | 1.31 | 1.5 mm² |
| 14 | 2.5 | 2.08 | 2.5 mm² |
| 12 | 4.0 | 3.31 | 4.0 mm² |
| 10 | 6.0 | 5.26 | 6.0 mm² |
| 8 | 10.0 | 8.37 | 10.0 mm² |

> **注意**: AWGはインチ系、mm²はメトリック系のため完全には一致しません。AWG18 (0.82mm²) の場合、0.75mm²フェルールは小さすぎるため1.0mm²を使用します。

---

## 2本用ツインフェルール

> **引用元**: [Knipex Twin Ferrules](https://www.knipex.com/), [Ferrules Direct - Twin Ferrules](https://www.ferrulesdirect.com/pages/ferrule-documents)

2本の線を1つのフェルールで束ねる場合に使用します。

### サイズ選定

| 元の線 (各1本) | 合計断面積 | 推奨ツインフェルール |
|----------------|------------|---------------------|
| 0.5 mm² × 2 | 1.0 mm² | 2 × 0.5 mm² |
| 0.75 mm² × 2 | 1.5 mm² | 2 × 0.75 mm² |
| 1.0 mm² × 2 | 2.0 mm² | 2 × 1.0 mm² |
| 1.5 mm² × 2 | 3.0 mm² | 2 × 1.5 mm² |
| 2.5 mm² × 2 | 5.0 mm² | 2 × 2.5 mm² |

> **ポイント**: AWGで同サイズ2本の場合、AWGを3つ上げた合計サイズに相当

---

### 剥き長さ目安

> **引用元**: [Knipex DIN 46228/4 Specifications](https://web-assets.knipex.com/sites/default/files/documents/AEH-HUELSEN-UBERSICHT_EN_V01_RZ20210624.PDF) (L2金属部長さに対応)

| フェルールサイズ | 剥き長さ (mm) |
|-----------------|---------------|
| 0.25-2.5 mm² | 8 mm |
| 4.0 mm² | 10 mm |
| 6.0-10.0 mm² | 12 mm |
| 16.0 mm² | 18 mm |
| 25.0 mm² | 22 mm |

---

## BotWheel Explorerでの使用

> **引用元**: [ODrive S1 Datasheet](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html), [BotWheel Explorer REV-B Hardware Build (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-REV-B-Hardware-Build-0eb19815a7b847a2a037a4246647d13c)

ODrive S1のスクリュー端子接続に推奨:

| 用途 | 線サイズ | フェルール |
|------|----------|------------|
| モーター電源 | 10-12 AWG | 4.0-6.0 mm² |
| モーター相 | 12-14 AWG | 2.5-4.0 mm² |
| ブレーキ抵抗器 | 14-16 AWG | 1.5-2.5 mm² |
| バッテリーメイン | 10-12 AWG | 4.0-6.0 mm² |

---

## 関連リンク

| リンク | 説明 |
|--------|------|
| [Ferrules Direct - Documents](https://www.ferrulesdirect.com/pages/ferrule-documents) | カラーコード表・サイズ表 |
| [Knipex Ferrule Overview (PDF)](https://web-assets.knipex.com/sites/default/files/documents/AEH-HUELSEN-UBERSICHT_EN_V01_RZ20210624.PDF) | 寸法詳細 |
| [American Electrical - Ferrule Codes](https://www.americanelectrical.com/blog/cracking-the-codes-for-insulated-wire-ferrules/) | DIN/T/W コード解説 |
| [DigiKey - Crimp Wire Ferrules](https://www.digikey.com/en/product-highlight/a/american-electrical/crimp-wire-ferrules) | 製品カタログ |
| [Phoenix Contact Ferrules (PDF)](https://dam-mdc.phoenixcontact.com/asset/156443151564/d8ed400fa93d944a8c496c0a1d791928/Ferrules_whitepaper_U003124B_FINAL.pdf) | 技術資料 |
