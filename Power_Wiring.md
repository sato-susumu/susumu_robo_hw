# 電源接続図 (BotWheel Explorer ベース)

BotWheel Explorer Kit 標準電源 (DeWalt 20V) をベースとした、本構成の電源・データ接続を示す。

---

## 目次

1. [電源系統の概要](#電源系統の概要)
2. [全体接続図](#全体接続図)
3. [系統別の役割](#系統別の役割)
4. [関連ドキュメント](#関連ドキュメント)

---

## 電源系統の概要

電源は **2 系統独立** で構成する。データ系のみが母艦 PC (UM790 Pro) を中心に両系統をまたいで接続される。

| 系統 | 電源 | 給電対象 |
|------|------|----------|
| 20V 系 | [DeWalt 20V バッテリー](Battery.md) | [ODrive S1](ODrive_S1.md) × 2、[Livox MID-360](Livox_MID360.md)、5V 補機 ([USB-HUB-7U](USB-HUB-7U.md)、[AmiVoice WT01](AmiVoice_WT01.md)) |
| 19V 系 | [Anker Prime Power Bank](Anker_Prime_PowerBank.md) (USB-C PD 140W) → PD トリガケーブル | [MINISFORUM UM790 Pro](MINISFORUM_UM790Pro.md) (母艦 PC) |

---

## 全体接続図

```mermaid
flowchart LR
    %% ===== 20V 系 (DeWalt) =====
    BATT["DeWalt 20V<br/>(5S Li-ion, 16.5-21V, 110Wh)"]
    FUSE["メインヒューズ<br/>30A ATO/ATC"]
    LVD["OONO 18V 30A LVD<br/>カット16.5V / 復帰17.5V"]
    BUS(("20V バス"))

    ODL["ODrive S1 (左)<br/>Node ID 0"]
    ODR["ODrive S1 (右)<br/>Node ID 1"]
    MOTL["BotWheel 左<br/>171mm ハブモータ"]
    MOTR["BotWheel 右<br/>171mm ハブモータ"]
    ENCL["エンコーダ 3200CPR<br/>+ ホール + サーミスタ"]
    ENCR["エンコーダ 3200CPR<br/>+ ホール + サーミスタ"]

    MID["Livox MID-360<br/>9-27V DC, 100BASE-TX"]

    DCDC["Buck DCDC<br/>10-32V → 5V 6A/30W"]
    HUB["Waveshare USB-HUB-7U<br/>5V 入力, 7×USB2.0"]
    WT01["AmiVoice WT01<br/>(BTマイク, USB充電)"]

    %% ===== 19V 系 (PC 専用・独立) =====
    PB["Anker Prime PowerBank<br/>27650mAh / 250W<br/>USB-C PD 最大140W"]
    TRIG["USB-C PD トリガケーブル<br/>(19V 出力)"]
    PC["MINISFORUM UM790 Pro<br/>19V / 120W"]

    D435["RealSense D435i<br/>USB 3.0 (PCへ直結)"]
    SW{{"2.5GbE ポート<br/>(UM790 Pro 内蔵)"}}

    %% --- 電源ライン (太) ---
    BATT ==20V==> FUSE ==> LVD ==> BUS
    BUS ==20V==> ODL
    BUS ==20V==> ODR
    BUS ==9-27V==> MID
    BUS ==10-32V==> DCDC
    DCDC ==5V==> HUB
    HUB ==5V==> WT01

    PB ==USB-C PD==> TRIG ==19V==> PC

    %% --- モータ接続 ---
    ODL --- MOTL
    ODL --- ENCL
    ODR --- MOTR
    ODR --- ENCR

    %% --- データ系 (細) ---
    PC -. USB3.0 .-> D435
    PC -. USB2.0 .-> HUB
    PC === SW
    SW -. Ethernet .-> MID
    PC -. CAN 250kbps<br/>(USBアイソレータ経由) .-> ODL
    PC -. CAN 250kbps .-> ODR

    classDef power fill:#fee,stroke:#c33,color:#000
    classDef logic fill:#eef,stroke:#33c,color:#000
    classDef sensor fill:#efe,stroke:#3a3,color:#000
    class BATT,FUSE,LVD,BUS,DCDC,PB,TRIG power
    class ODL,ODR,PC,HUB logic
    class MOTL,MOTR,ENCL,ENCR,D435,MID,WT01,SW sensor
```

凡例:

- **太線 (==)**: 電源ライン
- **点線 (-.)**: データ・通信ライン
- **実線 (---)**: モータ・エンコーダ等の機械的・電気的直結

---

## 系統別の役割

### 20V 系 (DeWalt 20V バッテリー)

- **保護**: 30A ATO/ATC ヒューズ → [OONO 18V 30A LVD](LowVoltageDisconnect.md) (カット 16.5V / 復帰 17.5V) で過電流・過放電を保護。
- **モータ駆動**: [ODrive S1](ODrive_S1.md) × 2 (動作電圧 12-48V) に直接給電。
- **LiDAR**: [Livox MID-360](Livox_MID360.md) は 9-27V DC 入力なので 20V バスから直接給電可能。
- **5V 補機**: [Buck DCDC (10-32V → 5V 6A)](DCDC_Converter.md) を介して [USB-HUB-7U](USB-HUB-7U.md) を給電。USB Hub 経由で [WT01](AmiVoice_WT01.md) 等の低速 USB デバイスを集約。

### 19V 系 (Anker Prime Power Bank、PC 専用)

- **対象**: [MINISFORUM UM790 Pro](MINISFORUM_UM790Pro.md) (19V / 120W) のみ。
- **給電経路**: [Anker Prime Power Bank](Anker_Prime_PowerBank.md) の USB-C PD (最大 140W) → PD トリガケーブルで 19V 出力 → UM790 Pro DC バレルジャック。
- **20V 系からは完全に独立**: PC の電源ノイズがモータ駆動系に影響しない、PC がバッテリー交換中も別系統で電源維持できる、というメリット。

### データ系 (PC を中心に両系統をまたぐ)

| 接続 | インターフェース | 備考 |
|------|------------------|------|
| PC ↔ ODrive S1 × 2 | CAN 250kbps | USB アイソレータ経由で絶縁 |
| PC ↔ RealSense D435i | USB 3.0 | PC 直結 (USB Hub は USB2.0 なので非経由) |
| PC ↔ USB-HUB-7U | USB 2.0 | WT01 等の低速デバイス集約 |
| PC ↔ Livox MID-360 | 2.5GbE (100BASE-TX 接続) | UM790 Pro 内蔵 LAN ポートに直結 |

---

## 関連ドキュメント

- [バッテリー技術資料](Battery.md) — DeWalt 20V 仕様、電圧設定、ヒューズ
- [低電圧カットオフモジュール (LVD) 技術資料](LowVoltageDisconnect.md) — OONO 18V 30A LVD
- [DC-DCコンバータ技術資料](DCDC_Converter.md) — 5V Buck コンバータ
- [Anker Prime Power Bank 技術資料](Anker_Prime_PowerBank.md) — PC 給電用モバイルバッテリー
- [MINISFORUM UM790 Pro 技術資料](MINISFORUM_UM790Pro.md) — 母艦 PC、19V 給電
- [BotWheel Explorer 技術資料](BotWheel_Explorer.md) — キット標準構成
