# Introduction
This is a hackintosh EFI built with OpenCore for the Lenovo Yoga 720-15IKB, i7-7700HQ, 4K laptop, designed in order to run macOS Big Sur 11.5.2 and above versions.
#
<img width="1920" alt="Screen Shot 2021-11-25 at 12 24 50 PM" src="https://user-images.githubusercontent.com/47384524/143482754-b3e5c08f-8826-4286-94fb-a81e5b2f0211.png">

## Hardware Configuration
- **Machine**: Lenovo Yoga 720 15-IKB
- **CPU**: Intel i7-7700HQ
- **GPU**: Intel HD630 (Integrated GPU)
- **RAM**: 16GB DDR4 (Stock)
- **Internal Display**: 4K UHD @60Hz with Touchscreen
- **Storage**: WD_BLACK SN750 NVMe 1TB SSD (Replaced Stock PM981 PCIe NVMe SSD)
- **Audio**: Realtek ALC236
- **WLAN + Bluetooth**: Intel Dual Band Wireless-AC 8265 (Stock)
- **Touchpad**: Elantech
- **BIOS Version**: 4MCN33WW(V2.05) 2018

## Features
|  |  |
| ---| --- |
| ✅ | OpenCore v0.7.5 |
| ✅ | 4K@60Hz internal display |
| ✅ | HDMI 2.0 and DisplayPort (up to 4K@60Hz) |
| ✅ | Apple Power Management (enhanced with VoltageShift) |
| ✅ | Sleep, Wake and Hibernate |
| ✅ | macOS Touchpad Gestures (enhanced with BetterTouchTool) |
| ✅ | Multipoint Touchscreen and Pen Support |
| ✅ | Speakers and Headphone jack (enhanced with Boom3D) |
| ✅ | Built-in Camera and Microphone |
| ✅ | Wi-Fi and Bluetooth |
| ✅ | Hot-swappable USB-C/Thunderbolt 3 |
| ✅ | Hotkeys (Brightness, Volume and Fn Keys) |
| ✅ | iServices (iMessage, FaceTime, App Store) |
| ✅ | Continuity and HandOff |
| 🟨 | AirDrop |
| ❌ | Dedicated Graphics (NVIDIA GTX 1050) |
| ❌ | Fingerprint Reader |

# Installation
If you are new to Hackintosh, please through the entire [OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/)

## Making the USB Installer

### BIOS Configuration
|  |  |
| ------- | ------- |
| Secure Boot | *Disabled* |
| Intel Platform Trust | *Disabled* |
| Fastboot | *Disabled* |
| Always-on USB | *Disabled* |
| Intel SGX | Software-Controlled |
| SATA Mode | AHCI |
| Intel Virtualization | Enabled |



