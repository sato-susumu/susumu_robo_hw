# Intel RealSense D435i 技術資料

> **引用元**: [Intel RealSense Depth Camera D435i 製品ページ](https://www.intelrealsense.com/depth-camera-d435i/)

> [!NOTE]
> 本資料は**検討段階**の資料です。採用が確定した場合はリポジトリ直下に移動します。

## 目次

- [製品概要](#製品概要)
- [外形・物理仕様](#外形物理仕様)
- [深度カメラ仕様](#深度カメラ仕様)
- [RGBカメラ仕様](#rgbカメラ仕様)
- [測距・精度](#測距精度)
- [内蔵IMU](#内蔵imu)
- [インターフェース・電源](#インターフェース電源)
- [ソフトウェア・SDK](#ソフトウェアsdk)
- [本構成での想定用途](#本構成での想定用途)

---

## 製品概要

Intel RealSense D435iは、ステレオ方式の深度カメラ「D435」にIMU (慣性計測ユニット) を追加したモデル。グローバルシャッター搭載の広視野ステレオ深度センサ、RGBカメラ、IRプロジェクタ、6軸IMUを一体化しており、移動ロボットのSLAM・障害物検出・3D認識に適する。

> **引用元**: [Intel RealSense D435i 製品ページ](https://www.intelrealsense.com/depth-camera-d435i/) / [CNX Software 紹介記事](https://www.cnx-software.com/2018/11/14/intel-realsense-d435i-stereo-depth-camera-6-dof-tracking/)

---

## 外形・物理仕様

| 項目 | 仕様 |
|------|------|
| 外形寸法 | 90 × 25 × 25 mm |
| 重量 | 約 72 g |
| 筐体マウント | 1/4-20 UNC ネジ穴 × 1、M3 ネジ穴 × 2 |
| 深度技術 | ステレオビジョン (アクティブIR対応) |

> **引用元**: [Intel RealSense D435i Depth Camera Guide (OpenELAB)](https://openelab.io/blogs/learn/intel-realsense-d435i-depth-camera-guide-complete-overview)

---

## 深度カメラ仕様

| 項目 | 仕様 |
|------|------|
| 深度FOV | 87° × 58° (±3°) |
| 深度方式 | ステレオ深度 (グローバルシャッター) |
| 深度解像度 | 最大 1280 × 720 |
| 深度フレームレート | 最大 90 fps |
| シャッター方式 | グローバルシャッター (深度センサ) |
| IRプロジェクタ | 内蔵 (暗所・無模様面でのステレオマッチング補助) |

> **引用元**: [Intel RealSense D435i Depth Camera Guide (OpenELAB)](https://openelab.io/blogs/learn/intel-realsense-d435i-depth-camera-guide-complete-overview)

---

## RGBカメラ仕様

| 項目 | 仕様 |
|------|------|
| RGB FOV | 69° × 42° (±3°) |
| RGB解像度 | 最大 1920 × 1080 |
| RGBフレームレート | 30 fps |
| シャッター方式 | ローリングシャッター (RGBセンサ) |

> **引用元**: [Intel RealSense D435i Depth Camera Guide (OpenELAB)](https://openelab.io/blogs/learn/intel-realsense-d435i-depth-camera-guide-complete-overview)

---

## 測距・精度

| 項目 | 仕様 |
|------|------|
| 理想動作範囲 | 0.3 m ～ 3 m |
| 最小深度距離 (Min-Z) | 約 28 cm (最大解像度時) |
| 最大範囲 | 約 10 m (精度は照明・キャリブレーション・対象に依存) |
| 深度誤差 | < 2% @ 2 m (代表値) |

> **引用元**: [Intel RealSense D435i 製品ページ](https://www.intelrealsense.com/depth-camera-d435i/) / [OpenELAB ガイド](https://openelab.io/blogs/learn/intel-realsense-d435i-depth-camera-guide-complete-overview)

---

## 内蔵IMU

| 項目 | 仕様 |
|------|------|
| IMUチップ | Bosch BMI055 |
| 構成 | 6軸 (3軸加速度計 + 3軸ジャイロスコープ) |
| 用途 | 6DoF (ピッチ・ヨー・ロール + XYZ並進) のモーション検出、SLAM補助 |

> **引用元**: [CNX Software 紹介記事](https://www.cnx-software.com/2018/11/14/intel-realsense-d435i-stereo-depth-camera-6-dof-tracking/) / [OpenELAB ガイド](https://openelab.io/blogs/learn/intel-realsense-d435i-depth-camera-guide-complete-overview)

---

## インターフェース・電源

| 項目 | 仕様 |
|------|------|
| データインターフェース | USB-C 3.1 Gen 1 (USB 3.0、5 Gbps) |
| 給電 | USBバスパワー (5V) |
| 推奨ケーブル | USB 3.1対応ケーブル (高解像度・高fpsでは帯域が必要) |

> **引用元**: [Intel RealSense D435i 製品ページ](https://www.intelrealsense.com/depth-camera-d435i/) / [OpenELAB ガイド](https://openelab.io/blogs/learn/intel-realsense-d435i-depth-camera-guide-complete-overview)

> [!NOTE]
> USB 3.0帯域を必要とするため、Raspberry Pi等に接続する場合はUSB 3.0ポート (またはUSB 3.0対応ハブ) への直結が望ましい。[USB-HUB-7U](../USB-HUB-7U.md) はUSB 2.0仕様のため、本カメラの高帯域用途には非対応。

---

## ソフトウェア・SDK

| 項目 | 仕様 |
|------|------|
| SDK | Intel RealSense SDK 2.0 (librealsense2) |
| 対応OS | Windows / Linux (Ubuntu) / macOS (限定) |
| ROS対応 | realsense-ros (ROS / ROS 2 対応ラッパー) |
| 出力 | 深度・RGB・IR・IMU (加速度/ジャイロ) ストリーム |

> **引用元**: [Intel RealSense SDK 2.0 (GitHub)](https://github.com/IntelRealSense/librealsense) / [realsense-ros (GitHub)](https://github.com/IntelRealSense/realsense-ros)

---

## 本構成での想定用途

- 低位置・近距離の障害物検出 (Livox MID-360の最小検出距離0.1m以遠を補完、近接の凹凸検出)
- RGB-D点群による3D認識・物体検出
- IMUを用いたVisual-Inertial Odometry / SLAM補助 (MID-360のLiDAR-SLAMとの統合検討)

> **関連**: 確定構成の3D LiDAR [Livox MID-360](../Livox_MID360.md) との役割分担、および [逆さ・下向き 2D LiDAR 調査](Inverted_2D_LiDAR.md) と併せて低位置障害物検出の手段として比較検討。
