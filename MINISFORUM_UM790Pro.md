# MINISFORUM Venus UM790 Pro 技術資料

> **引用元**: [MINISFORUM UM790 Pro 製品ページ](https://store.minisforum.com/products/minisforum-um790-pro)

## 目次

- [製品概要](#製品概要)
- [CPU・GPU](#cpugpu)
- [メモリ・ストレージ](#メモリストレージ)
- [インターフェース・ポート](#インターフェースポート)
- [無線・ネットワーク](#無線ネットワーク)
- [電源仕様](#電源仕様)
- [外形・冷却](#外形冷却)
- [本構成での想定用途](#本構成での想定用途)

---

## 製品概要

MINISFORUM Venus UM790 Proは、AMD Ryzen 9 7940HSを搭載した小型 (ミニ) PC。高性能なZen 4世代CPUと内蔵GPU Radeon 780Mを備え、ロボットの母艦PC (ROS 2実行・センサ処理・SLAM・推論) として十分な処理能力を持つ。USB4・2.5GbE・豊富なUSBポートを備え、各種センサ・デバイスとの接続性に優れる。

> **引用元**: [MINISFORUM UM790 Pro 製品ページ](https://store.minisforum.com/products/minisforum-um790-pro) / [MINISFORUM UK UM790 Pro](https://www.minisforum.uk/products/minisforum-um790-pro)

---

## CPU・GPU

| 項目 | 仕様 |
|------|------|
| CPU | AMD Ryzen 9 7940HS (Zen 4、TSMC 4nm) |
| コア / スレッド | 8コア / 16スレッド |
| クロック | 最大 5.2 GHz (16M キャッシュ) |
| 内蔵GPU | AMD Radeon 780M (RDNA 3、最大 2.8 GHz) |

> **引用元**: [MINISFORUM UK UM790 Pro](https://www.minisforum.uk/products/minisforum-um790-pro)

---

## メモリ・ストレージ

| 項目 | 仕様 |
|------|------|
| メモリ規格 | DDR5-5600 SODIMM、デュアルチャネル |
| メモリスロット | 2スロット (最大 64 GB = 32 GB × 2) |
| ストレージ | M.2 2280 PCIe 4.0 SSD × 2 (RAID 0/1 対応) |

> **引用元**: [MINISFORUM UK UM790 Pro](https://www.minisforum.uk/products/minisforum-um790-pro) / [Newegg 製品ページ](https://www.newegg.com/p/2SW-002G-000E2)

---

## インターフェース・ポート

| 項目 | 仕様 |
|------|------|
| USB4 | × 2 (Alt PD、最大 8K@60Hz 映像出力) |
| USB 3.2 Gen2 Type-A | × 4 |
| HDMI 2.1 | × 2 (4K@144Hz) |
| 有線LAN | RJ45 2.5GbE × 1 |
| オーディオ | 3.5mm ジャック × 1、DMIC × 1 |
| その他 | Clear CMOS ボタン |

> **引用元**: [MINISFORUM UK UM790 Pro](https://www.minisforum.uk/products/minisforum-um790-pro) / [Amazon (UM790 Pro)](https://www.amazon.com/MINISFORUM-7940HS-Radeon-USB3-2-PCIe4-0/dp/B0C7V29HBQ)

---

## 無線・ネットワーク

| 項目 | 仕様 |
|------|------|
| Wi-Fi | Wi-Fi 6E (M.2 2230 スロット) |
| Bluetooth | Bluetooth 5.3 |
| 有線LAN | 2.5 Gbps (RJ45) |

> **引用元**: [MINISFORUM UK UM790 Pro](https://www.minisforum.uk/products/minisforum-um790-pro)

---

## 電源仕様

| 項目 | 仕様 |
|------|------|
| 入力電圧 (DC) | 19 V |
| 付属ACアダプタ | 19 V / 6.3 A / 120 W |
| 給電方式 | DCバレルジャック (付属アダプタ)。USB4ポートはAlt PD対応 |

> **引用元**: [ServeTheHome UM790 Pro レビュー (120W電源)](https://www.servethehome.com/minisforum-um790-pro-review-big-upgrade-to-a-small-amd-system/minisforum-um790-pro-120w-power-adapter/)

> [!NOTE]
> 19V DC入力のため、ロボット側で19V系を供給できれば付属ACアダプタなしでの駆動も検討余地あり。検討中の [24V系電源](検討中/LiTime_24V_LiFePO4.md) からのDCDC降圧、または [Anker Prime Power Bank (250W)](Anker_Prime_PowerBank.md) のUSB-C PD (最大140W) → DCトリガーケーブル経由給電が候補。120W付属アダプタに対しPD140Wは余裕がある。

---

## 外形・冷却

| 項目 | 仕様 |
|------|------|
| 外形寸法 | 130 × 126 × 52.3 mm |
| 冷却 | Cold Wave 2.0 (液体金属 + アクティブ冷却、メモリ・SSD個別冷却) |
| OS | Windows 11 (Linux/Ubuntu 動作報告あり) |

> **引用元**: [MINISFORUM UK UM790 Pro](https://www.minisforum.uk/products/minisforum-um790-pro) / [Newegg 製品ページ](https://www.newegg.com/p/2SW-002G-000E2)

---

## 本構成での想定用途

- ロボット母艦PC: ROS 2スタックの実行、センサ統合、SLAM、推論処理
- 高帯域センサの接続先: [Intel RealSense D435i](検討中/RealSense_D435i.md) (USB 3.0)、[Livox MID-360](Livox_MID360.md) (2.5GbE経由)
- 検討中の [Raspberry Pi 4](検討中/RaspberryPi4.md) / [Pi 5](検討中/RaspberryPi5_USB_PD_Power.md) に対し、より高い処理能力が必要な場合の代替・上位構成

> **関連**: 給電は [Anker Prime Power Bank](Anker_Prime_PowerBank.md) ・ [24V系電源](検討中/LiTime_24V_LiFePO4.md) 、周辺機器接続は [USB-HUB-7U](USB-HUB-7U.md) を参照。
