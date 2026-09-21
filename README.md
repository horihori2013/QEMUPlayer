# QEMUPlayer

**高速・軽量・高機能な、オープンソースのゲーム向けAndroidエミュレーター。**

QEMUをベースに、ホストのCPUアーキテクチャに合わせたAndroid環境を動かします。
広告なし。不要なソフトウェアなし。ユーザーが自由に使えるAndroidエミュレーターを目指します。

## 特徴

* オープンソース・広告なし
* Windows / Linux対応
* x86_64 / ARM64対応
* QEMUベース
* Windows: WHPX / Hyper-V
* Linux: KVM
* VulkanベースのGPUアクセラレーション
* キーボード・マウス・ゲームパッド対応
* キーマッピング・マクロ
* マルチインスタンス
* スナップショット・インスタンス複製
* ゲームごとの設定
* ADB対応
* 軽量なネイティブUI

## アーキテクチャ

ホストと同じCPUアーキテクチャのAndroidを使用します。

### x86_64

```text
Windows / Linux x86_64
          │
          ▼
    Android x86_64
          │
    ┌─────┴─────┐
    ▼           ▼
x86_64      ARM64 apps
native      translation
```

x86_64アプリはネイティブで実行し、ARM64アプリのみTranslationを使用します。

### ARM64

```text
Windows / Linux ARM64
          │
          ▼
     Android ARM64
          │
          ▼
    Native execution
```

ARM64ホストではCPU Translationを必要としません。

## 仮想化

```text
Windows → QEMU → WHPX → Hyper-V
Linux   → QEMU → KVM
```

QEMUを共通の仮想化バックエンドとして使用することで、プラットフォーム間で可能な限り共通の構成を維持します。

## ストレージ

対応環境ではBtrfsとzstd圧縮を利用する予定です。

スナップショットやCopy-on-Writeを活用し、インスタンスの複製やロールバック、ディスク使用量の削減を可能にします。

## UI

デスクトップUIには **Rust + Slint** を使用する予定です。

エミュレーターコア、QEMU管理、ストレージ、入力処理などもRustを中心に実装します。

## 対応状況

| Host           | Android | Translation |
| -------------- | ------- | ----------- |
| Windows x86_64 | x86_64  | ARM64 apps  |
| Windows ARM64  | ARM64   | None        |
| Linux x86_64   | x86_64  | ARM64 apps  |
| Linux ARM64    | ARM64   | None        |
| macOS          | —       | Planned     |

macOSは仮想化・GPU周りの実装が大きく異なるため、初期リリースでは対応しません。

## 開発状況

**Early development**

現在はQEMU統合、Android起動、仮想化、GPUアクセラレーションなどの基盤部分を開発しています。

仕様や対応状況は今後変更される可能性があります。

## ライセンス

QEMUPlayerは **GNU General Public License v3.0 (GPL-3.0)** の下で公開します。

---

# English

**A fast, lightweight, and feature-rich open-source Android emulator for gaming.**

QEMUPlayer is built on QEMU and runs an Android guest matching the host CPU architecture whenever possible.

No advertisements. No unnecessary bundled software. Just an open Android gaming environment that users can control.

## Features

* Open source and ad-free
* Windows and Linux support
* x86_64 and ARM64 support
* QEMU-based virtualization
* WHPX / Hyper-V on Windows
* KVM on Linux
* Vulkan-based graphics acceleration
* Keyboard, mouse, and gamepad support
* Key mapping and macros
* Multiple instances
* Snapshots and instance cloning
* Per-game configuration
* ADB support
* Lightweight native UI

## Architecture

QEMUPlayer uses an Android guest matching the host CPU architecture.

### x86_64

```text
Windows / Linux x86_64
          │
          ▼
    Android x86_64
          │
    ┌─────┴─────┐
    ▼           ▼
x86_64      ARM64 apps
native      translation
```

x86_64 applications run natively, while ARM64 applications use translation when required.

### ARM64

```text
Windows / Linux ARM64
          │
          ▼
     Android ARM64
          │
          ▼
    Native execution
```

ARM64 hosts do not require CPU translation.

## Virtualization

```text
Windows → QEMU → WHPX → Hyper-V
Linux   → QEMU → KVM
```

QEMU provides a common virtualization layer across supported platforms.

## Storage

QEMUPlayer is planned to support Btrfs with zstd compression where appropriate.

Copy-on-Write and snapshots can be used for efficient instance cloning, rollback, and reduced storage usage.

## UI

The desktop UI is planned to use **Rust + Slint**.

The emulator core, QEMU management, storage, and input handling will also be primarily implemented in Rust.

## Platform Support

| Host           | Android | Translation |
| -------------- | ------- | ----------- |
| Windows x86_64 | x86_64  | ARM64 apps  |
| Windows ARM64  | ARM64   | None        |
| Linux x86_64   | x86_64  | ARM64 apps  |
| Linux ARM64    | ARM64   | None        |
| macOS          | —       | Planned     |

macOS support is planned for a later stage due to its different virtualization and graphics stack.

## Development Status

**Early development**

The project is currently focused on the core infrastructure, including QEMU integration, Android boot, hardware acceleration, and graphics.

Features and platform support may change during development.

## License

QEMUPlayer is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.
