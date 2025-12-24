# ODrive BotWheel Explorer 技術資料

---

## 目次

1. [概要](#概要)
2. [キット内容物](#キット内容物-フルキット)
3. [完成時寸法](#完成時寸法)
4. [環境定格](#環境定格)
5. [BotWheel モーター仕様](#botwheel-モーター仕様)
6. [BotWheel 物理仕様](#botwheel-物理仕様)
7. [BotWheel センサー](#botwheel-センサー)
8. [BotWheel コネクタ](#botwheel-コネクタ)
9. [キャスター (補助輪) 仕様](#キャスター-補助輪-仕様)
10. [Raspberry Pi セットアップ](#raspberry-pi-セットアップ)
11. [リンク集](#リンク集)

---

## 概要

> **公式情報**: [BotWheel Explorer Kit - ODrive Shop](https://shop.odriverobotics.com/products/botwheel-explorer)
>
> **公式ドキュメント**: [BotWheel Explorer Guide](https://docs.odriverobotics.com/v/latest/guides/botwheel-explorer.html)
>
> **公式ビルドガイド**: [BotWheel Explorer REV-B Hardware Build (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-REV-B-Hardware-Build-0eb19815a7b847a2a037a4246647d13c)

BotWheel Explorerは、ODrive S1モータコントローラとBotWheelハブモーターを使用した2輪駆動ロボットプラットフォームです。

---

## キット内容物 (フルキット)

> **引用元**: [BotWheel Explorer Kit - ODrive Shop](https://shop.odriverobotics.com/products/botwheel-explorer)

| 品目 | 数量 |
|------|------|
| ODrive S1 (スクリュー端子付) | 2 |
| ODrive BotWheel | 2 |
| ODrive S1エンクロージャ (ヒートスプレッダ・透明) | 2 |
| USBアイソレータ | 1 |
| シャーシプレート | 1 |
| メカニカルパーツバンドル (キャスター・CANハーネス含む) | 1 |

---

## 完成時寸法

> *出典: [BotWheel Explorer Kit](https://shop.odriverobotics.com/products/botwheel-explorer)*

| 項目 | 仕様 |
|------|------|
| サイズ | 450mm x 500mm x 175mm |
| 最低地上高 | 100mm |
| トラック幅 | 419mm |
| 重量 | 約20kg |
| 最大積載量 | 100kg (中央に均等分布) |

---

## 環境定格

> *出典: [BotWheel Explorer Kit](https://shop.odriverobotics.com/products/botwheel-explorer)*

| 項目 | 仕様 |
|------|------|
| IP等級 | IP10 |
| 使用環境 | 屋内・乾燥環境のみ |

---

## BotWheel モーター仕様

> **引用元**: [BotWheel - ODrive Shop](https://shop.odriverobotics.com/products/botwheels)

| 項目 | 仕様 |
|------|------|
| モータータイプ | ブラシレスハブモーター |
| ポール対数 | 15 |
| Kv値 | 8.7 RPM/V |
| トルク定数 (Kt) | 0.951 N-m/A |
| 定格トルク | 5 Nm |
| 定格速度 (24V時) | 110 rpm |
| 定格連続電流 | 5A |
| 定格連続出力 | 70W |

---

## BotWheel 物理仕様

> **引用元**: [BotWheel - ODrive Shop](https://shop.odriverobotics.com/products/botwheels)

| 項目 | 仕様 |
|------|------|
| ホイール直径 | 171mm |
| ホイール幅 | 約45mm |
| 質量 (1個) | 2.2kg |
| 質量 (2個セット) | 4.4kg |
| 定格負荷 | 80kg/ホイール |
| 取付パターン | 4×M6ネジ穴 (36mm円形パターン) |
| 防水等級 | IP54 (雨天走行可、水没不可) |

---

## BotWheel センサー

> **引用元**: [BotWheel - ODrive Shop](https://shop.odriverobotics.com/products/botwheels)

| センサー | 仕様 |
|----------|------|
| インクリメンタルエンコーダ | 3200 CPR |
| ホールセンサー | 搭載 |
| サーミスタ | R25=20kΩ, β=3950K |

---

## BotWheel コネクタ

> **引用元**: [BotWheel - ODrive Shop](https://shop.odriverobotics.com/products/botwheels)

| コネクタ | 型番 | 用途 |
|----------|------|------|
| 電源/エンコーダ | JST JWPF | 防水、モーター相・エンコーダ |
| サーミスタ | JST WPJ | 防水、温度センサー |

---

## キャスター (補助輪) 仕様

> **公式情報**: [BotWheel Explorer Kit - ODrive Shop](https://shop.odriverobotics.com/products/botwheel-explorer)

BotWheel Explorerには前方にキャスター (補助輪) が1個付属しています。

| 項目 | 仕様 | 公式出典 |
|------|------|----------|
| タイプ | スイベルキャスター (360°回転) | [製品ページ](https://shop.odriverobotics.com/products/botwheel-explorer) |
| 用途 | 2輪駆動の第3支点 | - |
| 地上高確保 | 100mm | [製品ページ: Ground clearance](https://shop.odriverobotics.com/products/botwheel-explorer) |
| バージョン | RevB (改良版キャスター搭載) | [製品ページ](https://shop.odriverobotics.com/products/botwheel-explorer) |



---

## Raspberry Pi セットアップ

> **引用元**: [BotWheel Explorer Guide - ODrive Documentation](https://docs.odriverobotics.com/v/latest/guides/botwheel-explorer.html)

| 手順 | コマンド/説明 |
|------|---------------|
| SPI有効化 | `raspi-config`でSPIを有効化 |
| can-utilsインストール | `sudo apt-get install can-utils` |
| CANインターフェース起動 | `sudo ip link set can0 up type can bitrate 250000` |
| python-canインストール | `pip3 install python-can` |

### ODriveノードID設定

| ODrive | Node ID |
|--------|---------|
| 左側 | 0 |
| 右側 | 1 |

---

## リンク集

| リンク | 説明 |
|--------|------|
| [BotWheel Explorer ガイド](https://docs.odriverobotics.com/v/latest/guides/botwheel-explorer.html) | 組立・セットアップガイド |
| [BotWheel Explorer Kit](https://shop.odriverobotics.com/products/botwheel-explorer) | キット購入ページ |
| [BotWheel 製品ページ](https://shop.odriverobotics.com/products/botwheels) | ホイール単体購入 |
| [公式ビルドガイド (Notion)](https://odriverobotics.notion.site/Botwheel-Explorer-REV-B-Hardware-Build-0eb19815a7b847a2a037a4246647d13c) | 詳細組立手順 |
| [GitHub: ros_odrive](https://github.com/odriverobotics/ros_odrive) | ROS2パッケージ |
| [Python CAN パッケージ](https://dylanballback.github.io/ODriveCan/setup/odrive/setup/) | pyodrivecan セットアップ |

### 3D CAD・設計データ

| リンク | 説明 |
|--------|------|
| [ODrive S1 OnShape CAD](https://docs.odriverobotics.com/v/latest/hardware/s1-datasheet.html) | 公式3Dモデル (データシート内リンク) |
| [ODrive S1 エンクロージャ CAD](https://shop.odriverobotics.com/products/enclosure-for-odrive-s1) | ケース3Dモデル |
| [GrabCAD ODrive モデル](https://grabcad.com/library/tag/odrive) | コミュニティ作成モデル |
