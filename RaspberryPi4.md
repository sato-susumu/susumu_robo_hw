# Raspberry Pi 4 Model B 資料

---

## 目次

1. [概要](#概要)
2. [基本スペック](#基本スペック)
3. [電源仕様](#電源仕様)
4. [消費電力](#消費電力)
5. [インターフェース](#インターフェース)
6. [BotWheel Explorerでの使用](#botwheel-explorerでの使用)
7. [OS](#os)

---

## 概要

> **公式ページ**: [Raspberry Pi 4 Model B](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/)
>
> **公式仕様**: [Raspberry Pi 4 Model B Specifications](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/)

BotWheel ExplorerではRaspberry Pi 4 Model Bをメインコンピュータとして使用します。

---

## 基本スペック

> **引用元**: [Raspberry Pi 4 Model B Specifications](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/)

### プロセッサ

| 項目 | 仕様 |
|------|------|
| SoC | Broadcom BCM2711 |
| CPU | Quad-core Cortex-A72 (ARM v8) 64-bit |
| クロック | 1.5GHz (リビジョンにより1.8GHz) |
| アーキテクチャ | ARMv8-A |

### メモリ

| モデル |
|--------|
| 2GB |
| 4GB |
| 8GB |

> **BotWheel Explorer推奨**: 4GB以上

### ストレージ

| 項目 | 仕様 |
|------|------|
| ストレージ | microSDカード |
| 推奨容量 | 16GB以上 (32GB推奨) |
| 推奨速度 | Class 10 / U1以上 |

---

## 電源仕様

> **引用元**: [Raspberry Pi 4 Model B Specifications](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/), [Raspberry Pi Power Supply](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#power-supply)

### 電源要件

| 項目 | 仕様 |
|------|------|
| 入力コネクタ | USB Type-C |
| 入力電圧 | 5V DC |
| 推奨電圧 | 5.1V DC (電圧降下対策) |
| 推奨電流 | 3A |
| 推奨電力 | 15W |
| 最小電流 | 2.5A (USB機器500mA以下時) |

### 電圧許容範囲

| 項目 | 電圧 |
|------|------|
| 動作電圧範囲 | 4.75V - 5.25V (USB規格 ±5%) |
| 低電圧警告 | 4.63V以下で検出 |
| 絶対最大定格 | 6.0V |

> **注意**: 低電圧時は画面右上に雷マーク (⚡) が表示されます

---

## 消費電力

> **引用元**: [Raspberry Pi Documentation - Power](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#power-supply), [RasPi.TV Power Measurements](https://raspi.tv/2019/how-much-power-does-the-pi4b-use-power-measurements)

### 状態別消費電力

| 状態 | 電流 | 電力 |
|------|------|------|
| アイドル | 575mA | 2.9W |
| デスクトップ起動 (ピーク) | 885mA | 4.4W |
| 1080p動画再生 | 600mA | 3.0W |
| 高負荷時 | ~1.2A | ~6W |
| シャットダウン (待機) | 69mA | 0.34W |

> **BotWheel Explorer**: DC-DCコンバータは3A出力で十分 (6A出力あれば余裕あり)

---

## インターフェース

> **引用元**: [Raspberry Pi GPIO Pinout](https://pinout.xyz/), [Raspberry Pi 4 Model B Specifications](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/)

### GPIO

| 項目 | 仕様 |
|------|------|
| ピン数 | 40ピン |
| GPIO数 | 28 (BCM2711) |
| 電圧レベル | 3.3V |

### 通信インターフェース

| インターフェース | 備考 |
|------------------|------|
| SPI | CAN HAT接続用 |

### ネットワーク

| 項目 | 仕様 |
|------|------|
| 有線LAN | Gigabit Ethernet |
| Wi-Fi | 802.11ac (2.4GHz / 5GHz) |
| Bluetooth | 5.0, BLE |

### 映像出力

| 項目 | 仕様 |
|------|------|
| HDMI | micro HDMI × 2 |
| 最大解像度 | 4K@60Hz (1画面) / 4K@30Hz (2画面) |

---

## BotWheel Explorerでの使用

> **引用元**: [BotWheel Explorer Guide - ODrive Documentation](https://docs.odriverobotics.com/v/latest/guides/botwheel-explorer.html), [CAN Bus Guide - ODrive Documentation](https://docs.odriverobotics.com/v/latest/guides/can-guide.html)

### CAN通信

Raspberry Pi 4は**CAN非内蔵**のため、外部モジュールが必要です。

| 項目 | 仕様 |
|------|------|
| 接続方式 | SPI経由 |
| CANコントローラ | MCP2515等のHAT使用 |
| ビットレート | 250kbps (BotWheel Explorer標準) |

### CAN設定コマンド

```bash
# SPIを有効化
sudo raspi-config
# → Interface Options → SPI → Enable

# can-utilsインストール
sudo apt-get install can-utils

# CANインターフェース起動
sudo ip link set can0 up type can bitrate 250000

# python-canインストール
pip3 install python-can
```

### ODrive接続

| ODrive | Node ID | 用途 |
|--------|---------|------|
| 左側 | 0 | 左ホイール制御 |
| 右側 | 1 | 右ホイール制御 |



---

## OS

> **引用元**: [Raspberry Pi OS](https://www.raspberrypi.com/software/), [ROS 2 Documentation](https://docs.ros.org/en/humble/), [ros_odrive (GitHub)](https://github.com/odriverobotics/ros_odrive)

### 推奨OS

| OS | バージョン | 備考 |
|----|------------|------|
| Raspberry Pi OS | 64-bit (Bookworm) | 公式推奨 |
| Ubuntu | 22.04 / 24.04 LTS | ROS2対応 |

### Raspberry Pi OS

| 項目 | 仕様 |
|------|------|
| ベース | Debian |
| 現行版 | Bookworm (Debian 12ベース) |
| アーキテクチャ | 64-bit |
| デスクトップ | LXDE |

### ROS2対応 (Ubuntu)

| ROS2バージョン | Ubuntu | サポート期限 |
|----------------|--------|--------------|
| Humble | 22.04 LTS | 2027年5月 |
| Jazzy | 24.04 LTS | 2029年5月 |

> **参考**: [ros_odrive (GitHub)](https://github.com/odriverobotics/ros_odrive)

