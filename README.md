#
<img width="1920" alt="Screen Shot 2021-11-25 at 12 24 50 PM" src="https://user-images.githubusercontent.com/47384524/143482754-b3e5c08f-8826-4286-94fb-a81e5b2f0211.png">

# Introduction
This is a hackintosh EFI built with OpenCore for the Lenovo Yoga 720-15IKB. It has been configured to run optimall on macOS Big Sur 11.5.2 and above versions.

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
| ✅ | 4K@60Hz Internal Display |
| ✅ | HDMI 2.0 and DisplayPort (up to 4K@60Hz) |
| ✅ | Hot-swappable USB-C/Thunderbolt 3 |
| ✅ | Apple Power Management (enhanced with VoltageShift) |
| ✅ | Sleep, Wake and Hibernate |
| ✅ | macOS Touchpad Gestures (enhanced with BetterTouchTool) |
| ✅ | Multipoint Touchscreen and Pen Support |
| ✅ | Speakers and Headphone jack (enhanced with Boom3D) |
| ✅ | Built-in Camera and Microphone |
| ✅ | Wi-Fi and Bluetooth |
| ✅ | Hotkeys (Brightness, Volume, and Fn Keys) |
| ✅ | iServices (iMessage, FaceTime, and App Store) |
| ✅ | Continuity and HandOff |
| 🟨 | AirDrop |
| ❌ | Dedicated Graphics (NVIDIA GTX 1050) |
| ❌ | Fingerprint Reader |

# Installation
If you are new to Hackintosh, please read through the entire [OpenCore Guide](https://dortania.github.io/OpenCore-Install-Guide/)

`Note` All disclaimers in the OpenCore Guide and any other guide in this post duly apply.

## Need to know
Knowledge in this section will help you debug issues quickly and potentially prevent future challenges.
- [What are Firmware Drivers](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#firmware-drivers)
- [What are Kexts](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#kexts)
- [What are SSDTs or DSDTs](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#laptop-input)
- How to install and update Kexts with OpenCore Configurator: _Download the correct Kext version from Github, copy it to `EFI\OC\Kexts` in your USB Installer and also to `Kernel -> Add` in `EFI\OC\Config.plist`.  It is advisable to store your configured EFI safely and use USB installers to test any new updates or features before moving them to your sytem EFI_.
- How to run downloaded apps and commands on macOS: _Right click the file and select `Open`_.

## Making the USB Installer
*Requires a 16GB+ USB 2.0 (or higher) device.*

You can prepare the USB installer using [macOS](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html), [Windows](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html#downloading-macos), or [Linux](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/linux-install.html). 
I recommend using a real Mac or a virtual machine to create the installer in order to follow conveniently with this guide. 

At this point, you have created a macOS Big Sur USB Installer. Now, you'd need to make it bootable. You'd also need to continue the rest of this guide on a Mac.

### Configuring EFI

Clone this repository, unzip the file and copy the EFI folder your newly opened EFI partition. This EFI is pretty much ready to go, however a few things need to be set before you are ready for installation.  

Download [MountEFI](https://github.com/corpnewt/MountEFI) and [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/) if you haven't. OpenCore Configurator is an alternative to [ProperTree](https://github.com/corpnewt/ProperTree) which provides easy-to-use GUI however, do not use it to download/update kexts. Simply copy and replace the particular kext in `EFI\OC\Kexts`.  

### SMBIOS
You need to set the Serial Number, UUID, MLB, and ROM for your hackintosh. This can all be set in the `Config.plist` located in `EFI\OC\Config.plist`. Open the file with OpenCore Configurator and navigate to `PlatformInfo`. Select the closest MacBook version to your processor from the list at the bottom. You can set your ROM now if you have the Mac Address of your Wi-Fi module. If you don't have it, you can find it [here](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-rom). This step is essential in order to have iServices work immediately. Follow this [guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html) if iServices don't work immediately after installation.

After setting your SMBIOS, while still in OpenCore Configurator, head over to `Kernel` and uncheck `CustomSMBIOSGUID` quirk.

### Wi-Fi and Bluetooth Kext
If you are using the stock Intel Wi-Fi and Bluetooth module, you can skip this step.  

However, if you are using a Broadcom module (check this [list](https://www.reddit.com/r/hackintosh/wiki/faq#wiki_wifi_compatibility) for macOS compatible modules), make sure to download acidanthera's BRCM kexts for [Wi-Fi](https://github.com/acidanthera/AirportBrcmFixup/releases) and [Bluetooth](https://github.com/acidanthera/BrcmPatchRAM/releases). Copy:  
- `AirportBrcmFixup.kext`  
- `BrcmBluetoothInjector.kext`  
- `BrcmFirmwareData.kext`  
- `BrcmPatchRAM3.kext`  

to `EFI\OC\Kexts` and also to `Config.plist -> Kernel -> Add`. Also, remove Intel kexts: `AirportItlwm`, `IntelBluetoothInjector`, and `IntelBluetoothFirmware` from `EFI\OC\Kexts` and `Config.plist`

At this point, your USB Installer should be bootable and almost ready for installation.

## Configuring BIOS
With the USB installer bootable, all that remains is configuring the BIOS of your Hackintosh-to-be.  
Restart the computer and press `F2` to boot to your BIOS Configuration. Use the navigation instructions provided on-screen and make sure the features below are properly set.  
|  |  |
| ------- | ------- |
| **Secure Boot** | *Disabled* |
| **Intel Platform Trust** | *Disabled* |
| **Fastboot** | *Disabled* |
| **Always-on USB** | *Disabled* |
| **Intel SGX** | Software-Controlled |
| **SATA Mode** | AHCI |
| **Intel Virtualization** | Enabled |

Now you are ready to begin the installation.

## Installing macOS
Refer to this [guide](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#double-checking-your-work) during installation. 

Plug in the USB installer, restart your computer, and press `F12`. This would bring up your Boot Menu. Select the EFI option that has the name of your USB. You should see another set options to select. Select `Install macOS Big Sur` and follow the on-screen instructions when it is booted.

`Note` The installer will restart a couple of times. Ensure that the USB is selected after each restart. You can change the Boot Order in your BIOS Configuration.

## Post-Installation
If all goes well, you have successfully installed macOS on your machine with most of the hardware working. Make sure to sign into your Apple account at this point.  

Now, you have to move your configured EFI folder from the USB installer to your system's EFI partition. Fetch `MountEFI` and `OpenCore Configurator` again and mount the EFI partitions of both your USB installer and your system (system partition is usually `disk0`). Copy `Boot` and `OC` from the EFI folder in your USB installer to the EFI folder of your system.

### Sleep, Wake, and Hibernation
These features, especially Hibernation seem to be working on later OpenCore versions. However, constant writing to SSDs through Hibernation reduces their lifespans, and there have even been reports that it can lead to data corruption. In order to disable Hibernation leaving just Sleep and Wake, run the following code in Terminal:
```
sudo pmset -a hibernatemode 0
sudo rm -f /var/vm/sleepimage
sudo mkdir /var/vm/sleepimage
sudo pmset -a standby 0
sudo pmset -a autopoweroff 0
sudo pmset -a powernap 0
sudo pmset -a proximitywake 0
sudo pmset -b tcpkeepalive 0      //Optional
```
At this point, your system is now bootable without the need for your USB installer.  

You now have a 90% working Hackintosh and quite frankly could go on without the next few steps as they require advanced knowledge, patience, and the ability to follow guides thoroughly.

## Remaining 9.99% Post-Installation
Great choice! Why not since you've already come all this way. All that is left is to get a perfect Power Management going on, activate Touchscreen and install third-party applications to enhance Audio, Touchpad gestures and Thermal Throttling.

### Enhancing Power Management (CFG-Unlock)
Most BIOS come with an option to set a feature called CFG-Lock (read more about it [here](https://dortania.github.io/OpenCore-Post-Install/misc/msr-lock.html#what-is-cfg-lock)). This feature allows an operating system gain more control over the system's power management. macOS needs such control to effect more stringent power management on your system.

`Warning` This step can potentially brick your system. Make sure to read through this next part thoroughly before clicking on any link or downloading any software! If you downloaded the wrong version and your keyboard doesn't work: turn off your computer, take out the battery, hold down the power button for 20+ secs, reinstall the battery and turn your system on again

Unfortunately, Lenovo has sealed this feature away. Luckily, this [guide](https://www.reddit.com/r/hackintosh/comments/hz2rtm/cfg_lockunlocking_alternative_method/) can help you get started. Use this version of [RU](https://ruexe.blogspot.com/2019/11/ru-5240370-beta.html) as other versions may not work with your keyboard. 

After you've cleared the CFG-Lock, restart your system and select `VerifyMsrE2` from OpenCore boot options instead of booting to macOS to verify that CFG-Lock is indeed unlocked. 

It should look like [this](https://drive.google.com/file/d/1tItmnh3WlMhKXUy7UtoapPLpg6mEsW-L/view). 

Now boot to macOS, mount your USB installer EFI and disable `AppleXcpmCfgLock` quirk in `Config.plist -> Kernel`. Restart macOS from the USB drive to see if it works.

If all goes well, your can repeat the immediate previous step for your system's EFI partition this time around.

### Enabling Low Frequency Mode
Another step towards achieving good power management is setting the lowest frequency your CPU will output when idle. The processor in this machine can handle a low power state of 800MHz. I recommend [acidanthera](https://github.com/acidanthera)'s [CPUFriend](https://github.com/acidanthera/CPUFriend/releases) kext and [corpnewt](https://github.com/corpnewt)'s [CPUFriendFriend](https://github.com/corpnewt/CPUFriendFriend) data provider kext to achieve this.

Download and install `CPUFriend.kext` to your USB installer EFI folder. Run `CPUFriendFriend.command` and follow the instructions on-screen. Enter `08` for the Low Frequency Mode to 800MHz. After you've finished configuring your power options, `CPUFriendDataProvider.kext` will be created in the `Results` folder. Install that kext to your USB installer EFI folder. Reboot your system using the USB installer and launch Intel Power Gadget to confirm `CoreMin` under the `Frequency` tab is around 800MHz (0.8GHz).

If all goes well, your can repeat the immediate previous step for your system's EFI partition this time around.

### Reducing Thermal Throttling (Undervolting)
Download Intel Power Gadget for macOS [here](https://www.intel.com/content/www/us/en/developer/articles/tool/power-gadget.html) and test your machine on `All Thread Frequency` and see if it throttles (caps at 2.8GHz for this machine below 70 degrees) unnecessarily. If it does, you may want to consider undervolting. Undervolting your CPU can reduce heat, improve performance, and provide longer battery life. However, if done incorrectly, it may cause an unstable system. My preferred method is using [VoltageShift](https://github.com/sicreative/VoltageShift).

VoltageShift binary and kext are already provided in the link above, hence no need to build with XCode. Open Terminal in the folder of your prefered version and run this command:

```
sudo chown -R root:wheel VoltageShift.kext
```
Follow the guide provided in the VoltageShift link above to test your settings and build a launch daemon that starts at log-in.

A good starting voltage for this machine \<CPU> \<GPU> \<CPUCache> is -110 -50 -110. Experiment with various settings below -125mV (CPU) and -90mV (GPU) until your system becomes stable. Use this code to create a launch daemon with your desired voltage, turbo-boost enabled, and PL1 and PL2 set to 45 and 60 Watts respectively:

```
./voltageshift removelaunchd
sudo ./voltageshift buildlaunchd -110 -50 -110 0 0 0 1 45 60 1 160
```

Reboot your system and test with Intel Power Gadget to see if your system still throttles. If all goes well, you have just enhanced your system performance. Run several Geekbenches and see how your machine performs against others in its class.

### Enabling Touchscreen (DSDT Patching)
In order to enable touchscreen, you have to patch your System DSDT. Refer to this [part](https://dortania.github.io/Getting-Started-With-ACPI/#a-quick-explainer-on-acpi) of the OpenCore Guide.
  
Download this decompiler [MaciASL](https://github.com/acidanthera/MaciASL/releases) and open it. It should open your `System DSDT`. Search using `CMD + F` for `TPNL` and scroll down slowly within its french bracket till you see `Method(_CRS, 0, Serialized)`. Delete the entire `If ((...)` Statement at the end of the method and add this code if it isn't already present:
```
Return (ConcatenateResTemplate (SBFB, SBFI))
```
Save the file as `DSDT.aml` in another directory. Copy this file to your USB installer `EFI\OC\ACPI` folder and also to `Config.plist -> ACPI -> Add`. Make sure it is at the top. Restart macOS through the USB Installer and test your touchscreen.
 
If all goes well, your touchscreen is now working. Repeat the immediate previous step on your system EFI.

Consider installing [BetterTouchTool](https://folivora.ai/) to add more gestures to both Touchpad and Touchscreen (Touchscreen behaves like a giant Touchpad)

### Enhancing Audio (Not much needed here)
Your audio should be working just fine, however not compared to the Dolby Atmos you are most likely used to.  
Consider installing [Boom3D](https://www.globaldelight.com/boom/boom-ppc.php?utm_source=google&utm_medium=cpc&utm_campaign=extension3) to optimize your sound.

## Additional Information
### Stock PM981 NVMe SSD 
The Samsung PM981 (or more precise the Phoenix controller it uses) is known to cause random kernel panics in macOS. Up until now, there was no way to even install macOS on the PM981 and the only option was to replace it with either a SATA or a known working NVMe SSD. However, recently a new set of patches, namely [NVMeFix](https://github.com/acidanthera/NVMeFix) was released. It greatly improves compatibility with non-apple SSDs including the PM981. Thanks to those patches, you can now install macOS, but there is still a chance for kernel panics to occur while booting.

## Acknoledgements
- [acidanthera](https://github.com/acidanthera) for providing almost all kexts and drivers
- [dortania](https://github.com/dortania) for an amazing in-depth guide to hackintoshing.
- [alexandred](https://github.com/alexandred) for providing VoodooI2C
- [RehabMan](https://github.com/rehabman) for providing many laptop hotpatches and guides
- [knnspeed](https://www.tonymacx86.com/threads/guide-dell-xps-15-9560-4k-touch-1tb-ssd-32gb-ram-100-adobergb.224486/) for providing ComboJack, well-explained hotpatches and a working USB-C hot plug solution
- [jaromeyer](https://github.com/jaromeyer) for providing detailed installation guides and configurations for the XPS 9570
- [frbuccoliero](https:/frbuccoliero) for PM981 related testing and extending the guide
- [mr-prez](https://github.com/mr-prez) for the Native Power Management guide
- [folivora](https://folivora.ai/) for creating BetterTouchTool
- [globaldelight](https://www.globaldelight.com/boom/thankyou-download-mac?reseller=googleppc) for creating Boom3D.
- [sicreative](https://github.com/sicreative/VoltageShift) for creating VoltageShift
- [openintelwireless](https://github.com/OpenIntelWireless) for providing Intel Wi-Fi and Bluetooth Kexts
- [wouter](https://www.reddit.com/user/Wouter_001/) for his CFG-Unlock Guide
- [jiashun zheng](https://jiashun-zheng.medium.com/) for his Yoga 720 Medium Guide
- [jlp](https://www.tonymacx86.com/members/jlp.123582/) and [thefiredragon](https://www.tonymacx86.com/members/thefiredragon.1412039/) for compiling [EFI](https://www.tonymacx86.com/threads/yoga-720-try-out-high-sierra-issues.227222/page-22) for Yoga 720 15-IKB
- Everyone else involved in Hackintosh development
