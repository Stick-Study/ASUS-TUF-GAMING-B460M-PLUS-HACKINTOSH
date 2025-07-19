# ASUS TUF GAMING B460M PLUS Hackintosh EFI

EFI configuration for ASUS TUF GAMING B460M PLUS.

简体中文（当前）  
[English](https://github.com/Stick-Study/ASUS-TUF-GAMING-B460M-PLUS-HACKINTOSH/blob/main/README.md)

---

## ⚠️ 免责声明

**您的保修已失效。**  
在使用本项目前请务必充分了解相关内容。本人不对任何损失负责，包括但不限于：内核崩溃、设备无法启动、硬件故障、存储损坏、数据丢失、原子弹爆炸、第三次世界大战、CK级重构事件（SCP基金会）及其他不可预见的后果。

---

## 📖 用户手册

- [中文用户手册 (PDF)](https://dlsvr04.asus.com.cn/pub/ASUS/mb/LGA1200/TUF_GAMING_B460M-PLUS/C17227_TUF_GAMING_B460M-PLUS_UM_V3_WEB.pdf)

---

## 🖥️ 硬件规格

| 规格             | 详情                                   |
|:-----------------|:---------------------------------------|
| 主板             | ASUS TUF GAMING B460M PLUS             |
| 处理器           | Intel Core i3-10100                    |
| 内存             | DDR4 2666 MHz，8 GB                    |
| NVMe 固态硬盘    | WD SN550 500 GB                        |
| 核显             | Intel UHD Graphics 630                 |
| 无线网卡         | BCM943602CS                            |
| [BIOS 版本](https://www.asus.com.cn/motherboards-components/motherboards/tuf-gaming/tuf-gaming-b460m-plus/helpdesk_bios/?model2Name=TUF-GAMING-B460M-PLUS) | 1301 版 |

---

## ✅ 兼容性

### 不可用功能

| 功能   | 状态 | 依赖项              | 备注 |
|--------|:----:|:-------------------:|------|
| Wi-Fi  | ❌   | IO80211FamilyLegacy | macOS Sonoma 需 [OCLP](https://github.com/dortania/OpenCore-Legacy-Patcher/pull/1077) |

### 显示与音频

| 功能                                 | 状态 | 依赖项             | 备注   |
|--------------------------------------|:----:|:------------------:|--------|
| 图形加速（QE/CI）                    | ✅   | WhateverGreen.kext |        |
| 3.5mm 麦克风音频录制                 | ✅   | AppleALC.kext      |        |
| 3.5mm 接口音频播放                   | ✅   | AppleALC.kext      |        |
| 耳机自动输出切换                     | ✅   | AppleALC.kext      |        |

### 电源、睡眠与休眠

| 功能                        | 状态 | 依赖项      | 备注                                                                                   |
|-----------------------------|:----:|:-----------:|----------------------------------------------------------------------------------------|
| CPU 电源管理（SpeedShift）  | ✅   | SSDT-PLUG   | 使用 iMac20,1 SMBIOS                                                                   |
| NVMe 硬盘电源管理           | ✅   |             |                                                                                        |
| S3 睡眠                     | ✅   |             |                                                                                        |
| 休眠模式 25                 | ✅   |             | 1. 终端运行 `sudo pmset hibernatemode 25`<br>2. 启用 Booter-DiscardHibernateMap<br>3. 设置 Misc-Boot-Hibernate Mode 为 Auto<br>4. 第三方 SSD 启用 Kernel-Quirks-ThirdPartyDrivers |

### 输入与输出

| 功能           | 状态 | 依赖项        | 备注                                   |
|----------------|:----:|:-------------:|----------------------------------------|
| USB 2.0、USB 3.0| ✅   | USBPorts.kext | 推荐**自定义** USB 定制                |

### 显示

| 功能   | 状态 | 依赖项 | 备注                                   |
|--------|:----:|:------:|----------------------------------------|
| HiDPI  | ✅   |        | 原生支持 UHD DP 外接显示器             |

---

## 📚 参考资料

- [dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [dortania's OpenCore Post Install Guide](https://dortania.github.io/OpenCore-Post-Install/)
- [dortania Getting Started with ACPI](https://dortania.github.io/OpenCore-Post-Install/)
- *Configuration.pdf* and *Differences.pdf* in each OpenCore release
- [daliansky/OC-little](https://github.com/daliansky/OC-little)
- [OpenCore 简体中文参考手册 (Unofficial)](https://oc.skk.moe)

**请认真阅读以上资源。**

---

## 🛠️ 准备工作

### 基础

- U 盘（4GB 及以上）
- [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools) 编辑 plist 文件（Windows/macOS）
- [ProperTree](https://github.com/corpnewt/ProperTree) 编辑 plist 文件（Windows/macOS）
- [MaciASL](https://github.com/acidanthera/MaciASL) 用于 ACPI 补丁
- [HackinTool](https://github.com/headkaze/Hackintool) 仅用于诊断（内置补丁已过时）
- 耐心和时间，尤其是首次黑苹果安装

### 硬件修改

#### 固态硬盘

三星 PM981/PM981a/PM991 及美光 2200S **不支持**。请使用兼容的 SSD。

#### 无线网卡

推荐使用 Broadcom 网卡以获得最佳性能和原生苹果生态体验。  
> 在 macOS Sonoma 中，Apple 移除了 IO80211FamilyLegacy。Broadcom 网卡需 [OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher/pull/1077) 才能正常使用。

### BIOS 设置

- Advanced > System Agent (SA) Configuration > VT-D: **Disabled**
- Advanced > System Agent (SA) Configuration > Above 4G Decoding: **Enabled**
- Advanced > USB Configuration > XHCI Hand-off: **Enabled**
- Boot > CSM (Compatibility Support Module) > Launch CSM: **Disabled**
- Boot > Secure Boot > OS Type: **Other OS**
- Boot > Boot\Boot Configuration > Wait For 'F1' If Error: **Disabled**

### 修复 Windows 8 小时时差

在 Windows 中运行以下命令：

```
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

---

## 🤝 贡献

如果本项目对你有帮助，请考虑支持：

- 点个 Star！
- [请我喝咖啡](https://ko-fi.com/fuyuxuan) 😝  
  或通过 [微信](https://github.com/Fu-Yuxuan-hub/Generic-EFI-for-H610-B660-Z690-B760-Z790/blob/main/Donation/WeChat.JPG) 或 [支付宝](https://github.com/Fu-Yuxuan-hub/Generic-EFI-for-H610-B660-Z690-B760-Z790/blob/main/Donation/Alipay.JPG)
- 有问题或建议请提交 Issue  
  > 请使用提供的 Issue 模板

---

## 🙏 鸣谢

- [acidanthera](https://github.com/acidanthera) 提供 OpenCore
- Apple 提供 macOS

---

## 🚫 注意

本仓库仅用于分享和协助黑苹果安装。**禁止商业用途。**

© 杆杆只爱学习, 以 MIT 许可证发布。