# MIX RMK Firmware

![Keyboard](https://img.shields.io/badge/Keyboard-MIX-black)
![Firmware](https://img.shields.io/badge/Firmware-RMK%200.9-orange)
![Controller](https://img.shields.io/badge/Controller-nRF52840-green)

[RMK](https://github.com/rmk-rs/rmk) firmware for the **CUBE_STUDIO MIX** wireless split keyboard (nRF52840). Configured entirely in `keyboard.toml` and built in the cloud by GitHub Actions; remap live with Vial.

**CUBE_STUDIO MIX** 无线分体键盘的 RMK 固件（nRF52840）。所有配置都在 `keyboard.toml` 里，由 GitHub Actions 云端编译，可用 Vial 实时改键。

## 官方资源 / Official Resources

购买、使用说明和教程都在工作室官网 [cubekb.com](https://cubekb.com)。 / Shop, user guides and tutorials live on the studio website [cubekb.com](https://cubekb.com).

* MIX 使用说明 / MIX user guide: [cubekb.com/wiki/products/mix](https://cubekb.com/wiki/products/mix)
* 刷机教程 / Flashing firmware: [guides/flash-firmware](https://cubekb.com/wiki/guides/flash-firmware)
* 蓝牙配对 / Bluetooth pairing: [guides/bluetooth](https://cubekb.com/wiki/guides/bluetooth)
* Vial 改键 / Vial remapping: [guides/vial](https://cubekb.com/wiki/guides/vial)
* RMK keyboard.toml: [guides/rmk-keyboard-toml](https://cubekb.com/wiki/guides/rmk-keyboard-toml)
* 故障排查 / Troubleshooting: [guides/troubleshooting](https://cubekb.com/wiki/guides/troubleshooting)
* 邮箱 / Email: [cubekb_studio@outlook.com](mailto:cubekb_studio@outlook.com) · QQ 群 / QQ group: **1037094476**

---

## 固件版本 / Firmware Editions

MIX 有三种固件，按购买时选择的配置使用对应的仓库。 / MIX ships with one of three firmwares — use the repository that matches your configuration.

| 版本 Edition | 仓库 Repository | 连接 Connection | 主控 Controller | 触控板 Touchpad | 改键 Remapping |
| --- | --- | --- | --- | --- | --- |
| ZMK | [zmk-mix](https://github.com/felixm12138/zmk-mix) | 无线 BLE + USB / Wireless | nRF52840 | ✓ | ZMK Studio |
| QMK + Vial | [qmk-vial-mix](https://github.com/felixm12138/qmk-vial-mix) | 有线 USB / Wired | RP2040 | ✓ | Vial |
| RMK | [rmk_mix](https://github.com/felixm12138/rmk_mix) | 无线 BLE + USB / Wireless | nRF52840 | — | Vial |

三个版本的默认键位一致。 / All three share the same default keymap.

---

## 功能特性 / Features

* 无线分体（BLE），**主机端在左手**（RMK 版无触控板） / Wireless BLE split, **central on the left half** (this edition has no touchpad)
* 5 个蓝牙配置 / 5 Bluetooth host profiles
* 左右各一个滚轮（EC11） / A roller (EC11 encoder) on each half
* 左右手电量都会上报给电脑 / Battery level of both halves is reported to the host
* 30 分钟无操作进入休眠，按任意键唤醒 / Idle sleep after 30 min, any key wakes it
* Vial 实时改键，6 层 / Live remapping in Vial, 6 layers

---

## 下载固件 / Getting Firmware

1. 打开仓库的 **Actions** 页面，点击 **Build RMK firmware** 最新一次成功的构建。
2. 在页面底部 **Artifacts** 下载 `Mix-firmware_uf2` 并解压，里面有 central（主机端）和 peripheral（从机端）两个 `.uf2` 文件。

1. Open **Actions** → the latest successful **Build RMK firmware** run.
2. Download `Mix-firmware_uf2` under **Artifacts** and unzip it; it holds a central and a peripheral `.uf2`.

## 刷机 / Flashing

1. 快速双击控制器上的复位键，电脑上会出现一个 U 盘。 / Double-tap the reset button; a USB drive appears.
2. **左手**拖入 central 文件，**右手**拖入 peripheral 文件，键盘会自动重启。 / Copy the **central** file to the **left** half and the **peripheral** file to the **right** half; each reboots automatically.
3. 在电脑蓝牙设置中搜索 `Mix` 并配对。 / Search for `Mix` in your computer's Bluetooth settings and pair.

左手也可以用组合键 **Esc + Backspace + 拇指区 Space + Enter** 进入刷机模式（只对左手/主机端有效）。
On the left half you can also press **Esc + Backspace + thumb Space + Enter** to enter the bootloader (central only).

> 从 RMK 0.9 以前的固件升级后，请在电脑上删除旧的 Mix 配对再重新配对。
> After upgrading from firmware older than RMK 0.9, remove the old Mix pairing on your computer and pair again.

---

## 按键 / Keymap

默认键位与 [ZMK 版](https://github.com/felixm12138/zmk-mix) 一致。 / The default keymap matches the [ZMK edition](https://github.com/felixm12138/zmk-mix).

| 层 Layer | 名称 Name | 进入方式 Access | 内容 Contents |
| --- | --- | --- | --- |
| 0 | `Default` | — | 数字行 + QWERTY / Number row + QWERTY |
| 1 | `layer_1` | 按住左手 `MO 1` / hold left `MO 1` | F1–F12、`- = [ ]` |
| 2 | `layer_2` | 按住右手 `MO 2` / hold right `MO 2` | 上档符号 / Shifted symbols `! @ # … { } < > ?` |
| 3 | `BT` | 按住 RCtrl 左侧的 Space（单击为空格） / hold the `Space` next to RCtrl (tap = space) | 蓝牙配置 / Bluetooth profiles |
| 4–5 | — | Vial | 空层，可自定义 / Spare layers for your own use |

**蓝牙层 / Bluetooth layer**

* 数字 `1`–`5`：切换蓝牙配置 1–5；**长按 5 秒**清除该配置并重新配对 / `1`–`5`: select BT profile 1–5; **hold 5 s** to clear that profile and re-pair
* `Esc` 位置：清除当前配置的配对 / `Esc` position: clear the current profile's bond

**滚轮 / Rollers**

| 层 Layer | 左滚轮 Left | 右滚轮 Right |
| --- | --- | --- |
| 0 | 音量 / Volume | 滚动 / Scroll |
| 1 | 音量 / Volume | 翻页 / Page Up · Down |
| 2、3 | 音量 / Volume | 方向键 / Arrow Up · Down |

**Vial 改键 / Remapping in Vial**

USB 连接左手（主机端），用 [Vial](https://get.vial.today) 或 [vial.rocks](https://vial.rocks) 实时改键。解锁组合键为 **Esc + 1**。
Connect the left (central) half over USB and open [Vial](https://get.vial.today) or [vial.rocks](https://vial.rocks). The unlock combo is **Esc + 1**.

---

## 修改配置 / Customizing

编辑 `keyboard.toml` 并推送，GitHub Actions 会自动编译。配置格式见 [RMK 文档](https://rmk.rs/docs/configuration)。
Edit `keyboard.toml` and push; GitHub Actions builds automatically. See the [RMK docs](https://rmk.rs/docs/configuration) for the format.

编译固定使用 RMK **0.9**（`.github/workflows/build.yml` 中的 `rmk_version`），避免新版本的配置格式变化导致编译失败。升级 RMK 时请先阅读官方迁移指南。
Builds are pinned to RMK **0.9** (`rmk_version` in `.github/workflows/build.yml`) so a new release cannot break the build unannounced. Read the official migration guide before upgrading.

```text
.
├── .github/workflows/build.yml   # Cloud build (RMK user_build workflow, pinned to 0.9)
├── keyboard.toml                 # Matrix, pins, keymap, BLE, split, encoders
└── vial.json                     # Vial layout definition
```

---

## 常见问题 / Troubleshooting

* **左右手不通 / Halves not linking**：确认左手刷 central、右手刷 peripheral，且来自同一次构建。 / Make sure the left half runs central and the right half runs peripheral, from the same build.
* **蓝牙连不上 / Can't connect**：长按对应配置的数字键 5 秒清除后重新配对。 / Hold the profile's number key for 5 s to clear it, then pair again.
* 更多 / More: [蓝牙配对 Bluetooth pairing](https://cubekb.com/wiki/guides/bluetooth) · [故障排查 Troubleshooting](https://cubekb.com/wiki/guides/troubleshooting)

---

## 致谢 / Credits

* [RMK](https://github.com/rmk-rs/rmk) · [Vial](https://get.vial.today)
