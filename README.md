#
<img width="1920" alt="Screen Shot 2021-11-25 at 12 24 50 PM" src="https://user-images.githubusercontent.com/47384524/143482754-b3e5c08f-8826-4286-94fb-a81e5b2f0211.png">

# Introduction
This is a hackintosh EFI built with OpenCore for the Lenovo Yoga 720-15IKB, i7-7700HQ, 4K laptop, designed in order to run macOS Big Sur 11.5.2 and above versions.

### Hardware Configuration
| | |
| :--: | -- |
| **Machine** | Lenovo Yoga 720 15-IKB |
| **Processor** | Intel i7-7700HQ |
| **Graphics** | Intel HD630 (Integrated GPU) |
| **RAM** | 16GB DDR4 (Stock) |
| **Internal Display** | 4K UHD @60Hz with Touchscreen |
| **Storage** | WD_Black SN750 NVMe SSD (Replacement) |
| **Audio** | Realtek ALC236 |
| **WLAN + Bluetooth** | Intel Dual Band Wireless-AC 8265 (Stock) |
| **Touchpad** | Elantech |
| **BIOS Version** | 4MCN33WW(V2.05) 2018 |

### Features
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
If you are new to Hackintosh, please read through the entire [OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/)

## Making the USB Installer
*Requires 16GB+ USB 2.0 or higher*

You can prepare the USB installer using [macOS](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html), [Windows](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html#downloading-macos), [Linux](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/linux-install.html). 
I recommend using a real Mac or virtual machine to create the installer in order to follow conveniently with the guide. From here on, I'll assume you have setup your USB Installer and are currently running on macOS.

## Configuring EFI

Clone this repository, unzip the file and copy the EFI folder your newly opened EFI partition. This EFI is pretty much ready to go, however a few things need to set before you are ready for installation.  

Download [MountEFI](https://github.com/corpnewt/MountEFI) and [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/) if you haven't. OpenCore Configurator is an alternative to [ProperTree](https://github.com/corpnewt/ProperTree) which provides easy-to-use GUI however, do not use it to download/update kexts. Simply copy and replace the particular kext in EFI\OC\Kexts.  

### SMBIOS
You need to set the Serial Number, UUID, MLB, and ROM for your hackintosh. This can all be set in the _Config.plist_ located in EFI\OC\Config.plist. Open the file with OpenCore Configurator and navigate to _PlatformInfo_. Select the closest MacBook version to your processor from the list at the bottom. You can set your ROM now if you have the Mac Address of your Wi-Fi module. If you don't have it, you can find it [here](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-rom). This step is essential in order to have iServices work immediately. Follow this [guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html) if iServices don't work immediately after installation.

### Wi-Fi and Bluetooth Kext
If you are using the stock Intel Wi-Fi and Bluetooth module, you can skip this step. However, if you are using a Broadcom module (check this [list](https://www.reddit.com/r/hackintosh/wiki/faq#wiki_wifi_compatibility) for macOS compatible modules), make sure to download acidanthera's BCM kexts for [Wi-Fi](https://github.com/acidanthera/AirportBrcmFixup/releases) and [Bluetooth](https://github.com/acidanthera/BrcmPatchRAM/releases). Copy  
> AirportBrcmFixup.kext  
> BrcmBluetoothInjector.kext  
> BrcmFirmwareData.kext  
> BrcmPatchRAM3.kext  
 
to EFI\OC\Kexts and also to _Config.plist -> Kernel -> Add_. Remove _AirportItlwm, IntelBluetoothInjector, and IntelBluetoothFirmware_ from EFI\OC\Kexts and Config.plist


### BIOS Configuration
|  |  |
| ------- | ------- |
| **Secure Boot** | *Disabled* |
| **Intel Platform Trust** | *Disabled* |
| **Fastboot** | *Disabled* |
| **Always-on USB** | *Disabled* |
| **Intel SGX** | Software-Controlled |
| **SATA Mode** | AHCI |
| **Intel Virtualization** | Enabled |



