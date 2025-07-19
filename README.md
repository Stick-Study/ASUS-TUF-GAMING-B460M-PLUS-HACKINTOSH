# ASUS TUF GAMING B460M PLUS Hackintosh EFI

EFI configuration for ASUS TUF GAMING B460M PLUS.

English (current)  
[简体中文](https://github.com/Stick-Study/ASUS-TUF-GAMING-B460M-PLUS-HACKINTOSH/blob/main/README_CN.md)

---

## ⚠️ Disclaimer

**Your warranty is now void.**  
Please research thoroughly before using this project. I am not responsible for any loss, including but not limited to: kernel panics, device boot failures, hardware malfunction, storage damage, data loss, atomic bombing, World War III, CK-Class Restructuring Scenario (SCP Foundation), and other unforeseen consequences.

---

## 📖 User Manual

- [English Manual (PDF)](https://dlsvr04.asus.com.cn/pub/ASUS/mb/LGA1200/TUF_GAMING_B460M-PLUS/E17227_TUF_GAMING_B460M-PLUS_UM_V3_WEB.pdf)

---

## 🖥️ Hardware Specifications

| Specification      | Detail                                  |
|:-------------------|:----------------------------------------|
| Motherboard        | ASUS TUF GAMING B460M PLUS              |
| CPU                | Intel Core i3-10100                     |
| Memory             | DDR4 2666 MHz, 8 GB                     |
| NVMe SSD           | WD SN550 500 GB                         |
| Integrated Graphics| Intel UHD Graphics 630                  |
| Wireless Card      | BCM943602CS                             |
| [BIOS Version](https://www.asus.com.cn/motherboards-components/motherboards/tuf-gaming/tuf-gaming-b460m-plus/helpdesk_bios/?model2Name=TUF-GAMING-B460M-PLUS) | Version 1301 |

---

## ✅ Compatibility

### Non-Functional

| Feature | Status | Dependency | Remarks |
|--------|:------:|:----------:|---------|
| Wi-Fi  | ❌     | IO80211FamilyLegacy | Requires [OCLP](https://github.com/dortania/OpenCore-Legacy-Patcher/pull/1077) for macOS Sonoma |

### Video & Audio

| Feature                              | Status | Dependency           | Remarks                        |
|---------------------------------------|:------:|:--------------------:|--------------------------------|
| Full Graphics Acceleration (QE/CI)    | ✅     | WhateverGreen.kext   |                                |
| Audio Recording via 3.5mm Microphone  | ✅     | AppleALC.kext        |                                |
| Audio Playback via 3.5mm Jack         | ✅     | AppleALC.kext        |                                |
| Automatic Headphone Output Switching  | ✅     | AppleALC.kext        |                                |

### Power, Sleep & Hibernation

| Feature                        | Status | Dependency      | Remarks                                                                                   |
|-------------------------------|:------:|:---------------:|-------------------------------------------------------------------------------------------|
| CPU Power Management (SpeedShift) | ✅     | SSDT-PLUG       | Use iMac20,1 SMBIOS                                                                        |
| NVMe Drive Power Management    | ✅     |                 |                                                                                           |
| S3 Sleep                      | ✅     |                 |                                                                                           |
| Hibernate Mode 25             | ✅     |                 | 1. Run `sudo pmset hibernatemode 25` in Terminal<br>2. Enable Booter-DiscardHibernateMap<br>3. Set Misc-Boot-Hibernate Mode to Auto<br>4. Enable Kernel-Quirks-ThirdPartyDrivers for third-party SSDs |

### Input & Output

| Feature         | Status | Dependency      | Remarks                                 |
|-----------------|:------:|:---------------:|------------------------------------------|
| USB 2.0, USB 3.0| ✅     | USBPorts.kext   | Recommended to **customize** USB mapping |

### Display

| Feature | Status | Dependency | Remarks                                 |
|---------|:------:|:----------:|------------------------------------------|
| HiDPI   | ✅     |            | Native support for UHD DP external screen|

---

## 📚 References

- [dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [dortania's OpenCore Post Install Guide](https://dortania.github.io/OpenCore-Post-Install/)
- [dortania Getting Started with ACPI](https://dortania.github.io/OpenCore-Post-Install/)
- *Configuration.pdf* and *Differences.pdf* in each OpenCore release
- [daliansky/OC-little](https://github.com/daliansky/OC-little)

**Please read these resources carefully.**

---

## 🛠️ Requirements

### Basic

- USB flash drive (4GB or larger)
- [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools) for editing plist files (Windows/macOS)
- [ProperTree](https://github.com/corpnewt/ProperTree) for editing plist files (Windows/macOS)
- [MaciASL](https://github.com/acidanthera/MaciASL) for ACPI patching
- [HackinTool](https://github.com/headkaze/Hackintool) for diagnostics only (built-in patches are outdated)
- Patience and time, especially if this is your first Hackintosh

### Hardware Modifications

#### SSD

Samsung PM981/PM981a/PM991 and Micron 2200S are **not supported**. Please use a compatible SSD.

#### Wireless Card

Broadcom wireless cards are recommended for best performance and native Apple ecosystem features.  
> In macOS Sonoma, Apple removed IO80211FamilyLegacy. Broadcom cards require [OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher/pull/1077) for functionality.

### BIOS Settings

- Advanced > System Agent (SA) Configuration > VT-D: **Disabled**
- Advanced > System Agent (SA) Configuration > Above 4G Decoding: **Enabled**
- Advanced > USB Configuration > XHCI Hand-off: **Enabled**
- Boot > CSM (Compatibility Support Module) > Launch CSM: **Disabled**
- Boot > Secure Boot > OS Type: **Other OS**
- Boot > Boot\Boot Configuration > Wait For 'F1' If Error: **Disabled**

### Fix Windows 8-Hour Time Difference

Run the following command in Windows:

```
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

---

## 🤝 Contribution

If you find this project helpful, please consider supporting it:

- Give it a star!
- [Buy me a coffee](https://ko-fi.com/fuyuxuan) 😝  
  Or via [WeChat](https://github.com/Fu-Yuxuan-hub/Generic-EFI-for-H610-B660-Z690-B760-Z790/blob/main/Donation/WeChat.JPG) or [Alipay](https://github.com/Fu-Yuxuan-hub/Generic-EFI-for-H610-B660-Z690-B760-Z790/blob/main/Donation/Alipay.JPG)
- Open an issue for problems or suggestions  
  > Please use the provided issue template

---

## 🙏 Credits

- [acidanthera](https://github.com/acidanthera) for OpenCore
- Apple for macOS

---

## 🚫 Notice

This repository is for sharing and assisting with Hackintosh installations. **Commercial use is not permitted.**

© 杆杆只爱学习, Released under the MIT License.