
![image](https://user-images.githubusercontent.com/47384524/144275381-12bd6ee1-ced8-4a4f-a5df-9aad0437952d.png)

# Introduction
Provided in this repository are EFI configurations for installing other macOS on Lenovo Yoga 720-15IKB using OpenCore. This EFI repository has been optimized to run macOS Big Sur 11.5.2 and above.

###
###
###

![image](https://user-images.githubusercontent.com/47384524/164774459-bea30f58-3d5b-45c7-a228-25f347fbb2af.png) 
![image](https://user-images.githubusercontent.com/47384524/164774497-60d8a0e3-51cd-4a4b-a336-d3a2daffdd14.png)


### Hardware Configuration
| | |
| :--: | -- |
| **Machine** | Lenovo Yoga 720 15-IKB |
| **Processor** | Intel Core i7-7700HQ |
| **Graphics** | Intel HD630 (Integrated GPU) |
| **Renderer** | NVIDIA GTX 1050 (2GB VRAM) |
| **RAM** | 16GB DDR4 (Stock) |
| **Internal Display** | 4K UHD @60Hz with Touchscreen & Pen |
| **Storage** | WD_Black SN750 NVMe SSD (Replacement) |
| **Audio** | Realtek ALC236 |
| **WLAN + Bluetooth** | Fenvi BCM94360NG (Replacement) |
| **Touchpad** | Elantech |
| **BIOS Version** | 4MCN33WW(V2.05) 2018 |

### Features
|  |  |
| ---| --- |
| ✅ | OpenCore v0.8.3 |
| ✅ | macOS 12.5.1 |
| ✅ | Apple Power Management (enhanced with VoltageShift) |
| ✅ | Sleep, Wake and Hibernate |
| ✅ | Hot-swappable USB-C/Thunderbolt 3 |
| ✅ | 4K@60Hz 24-bit Color Internal Display |
| ✅ | HDMI 2.0 and DisplayPort (up to 4K@60Hz) |
| ✅ | Hotkeys (Brightness, Volume, and Fn Keys) |
| ✅ | macOS Touchpad Gestures (enhanced with BetterTouchTool) |
| ✅ | Multipoint Touchscreen and Pen Support |
| ✅ | Speakers and Headphone jack (enhanced with Boom3D) |
| ✅ | Built-in Camera and Microphone |
| ✅ | Wi-Fi and Bluetooth |
| ✅ | AirDrop |
| ✅ | Continuity: Sidecar, Universal Clipboard and HandOff |
| ✅ | Monterey Features: Universal Control, AirPlay to Mac |
| ✅ | iServices (iMessage, FaceTime, and App Store) |
| ❌ | Dedicated Graphics (NVIDIA GTX 1050) |
| ❌ | Fingerprint Reader |

# Updates
#### (20/08/22) - Updated to OpenCore 0.8.3 and macOS 12.5.1

##### Changes
- Updated OpenCore Files to v0.8.3
- Reverted ACPI Files to 22/04/22 Changes due to stability. Changes in 02/06/22 have been reverted. (Auto Brightness not working, default enabled touchscreen seems to only supports single touch)

#### (06/07/22) - Updated to OpenCore 0.8.2

##### Changes
- Updated OpenCore Files to v0.8.2
- Updated Kexts

#### (06/06/22) - Updated to OpenCore 0.8.1

##### Changes
- Updated OpenCore Files to v0.8.1
- Updated Kexts

#### (02/06/22) - Updated to macOS 12.4, Added Touchscreen SSDT, Added Auto-Brightness

##### Changes
- No need to patch System DSDT, Touchscreen enabled by default. To disable touchscreen, go [here](https://github.com/dikamsiyoung/Lenovo-Yoga-720-15IKB-EFI-OpenCore-0.8.0/blob/main/README.md#enabling-touchscreen).
- `Automatically Adjust Brightness` now available in Display Preferences.

#### (22/04/22) - Updated to OpenCore 0.8.0

##### Changes
- Updated OpenCore Files to v0.8.0
- Updated Kexts

#### (14/04/22) - Updated to macOS 12.3.1, Changed WiFi/Bluetooth Card, Fixed Wake-from-Sleep with One Key Press, Deprecated Big Sur EFI

##### Changes
- Replaced Intel Dual Band Wireless-AC 8265 with Fenvi BCM94360NG Wireless Card.
- Removed WiFi and Bluetooth kexts.
- Continuity features working properly.
- WiFi speed halved due to Fenvi drivers. See issue https://github.com/acidanthera/bugtracker/issues/1532
- Added SSDT-USBW patch to allow system wake after pressing a button once.
- Stopped updating Big Sur Kexts. Update Kexts using [Hackintool](https://github.com/headkaze/Hackintool)

#### (11/03/22) - Updated to OpenCore 0.7.9 and macOS 12.2.1

##### Changes
- Updated OpenCore files to v0.7.9
- Updated Kexts.
- Continuity still works one way.

#### (17/12/21) - Updated to OpenCore 0.7.6 and macOS 12.1

##### Changes
- Updated OpenCore to v0.7.6
- Updated Kexts.
- Continuity still works one way.

#### (01/12/21) - Updated to macOS 12.0.1 (Monterey)
Successfully installed macOS Monterey with most features working. However, Continuity only works one-way (from other devices to the hack). Provided Monterey EFI folder. Installation process remains relatively the same however I have included `Monterey` portions in this guide. 

##### Monterey EFI Changes
- Replaced `IntelBluetoothInjector.kext` with `BluetoolFixup.kext`.
- Set `MinKernel` to 21.00.0 and `MaxKernel` to 20.99.9.
- Removed `FakePCIID.kext` and `FakePCIID_Intel_HDMI_Audio.kext`.

# Installation
This is guide is provided for educational purposes and is based off numerous contributions by outstanding developers. If you are new to Hackintosh and OpenCore, please read through the entire [OpenCore macOS Installation Guide](https://dortania.github.io/OpenCore-Install-Guide/). I shall be making references to several portions of it. 

>  All disclaimers in the OpenCore Guide and any other guide in this post duly apply.

## Need to know
Knowledge in this section will help you debug issues quickly and potentially prevent future challenges.
- #### Extensible Firmware Interface (EFI) 
  Following the widespread adoption of Unified Extensible Firmware Interface (UEFI) by PC manufacturers as the standard interface between operating systems and their corresponding hardware, PCs can now boot directly from nonvolatile storage devices instead of a read-only chip embedded on their motherboard. The boot files are located in the first partition of a GPT-formatted storage device, which is known as the EFI System Partition (or ESP). The switch to UEFI vastly increases boot speed, the amount of external storage that can be addressed by the system, and for the purpose of this guide, it affords us the ability to configure the boot process with more ease. Read more about UEFI [here](https://whatis.techtarget.com/definition/Unified-Extensible-Firmware-Interface-UEFI#:~:text=Unified%20Extensible%20Firmware%20Interface%20(UEFI)%20is%20a%20specification%20for%20a,its%20operating%20system%20(OS).&text=Like%20BIOS%2C%20UEFI%20is%20installed,runs%20when%20booting%20a%20computer.).
   
  The EFI configuration for a successful macOS boot with OpenCore requires a `BOOT` folder containing `BOOTx64.efi` (a file that initializes the boot sequence) and an `OC` folder containing files necessary for OpenCore to be loaded successfully. These files and their settings are defined in `Config.plist`. 
  
  Refer to the [OpenCore EFI Documentation](https://dortania.github.io/docs/latest/Configuration.html) for a detailed explanation of each directory in this repository.
  
- #### Config.plist
  Located in the OC folder `EFI\OC\Config.plist`, `Config.plist` defines various files to be loaded during UEFI boot and others to be injected into macOS along with their configurations. It also defines the order of precedence with which these files will be loaded.
- #### Installing and updating Kexts with OpenCore Configurator  
  Download the correct Kext version from Github, copy it to `EFI\OC\Kexts` in your USB Installer and also to `Kernel -> Add` in `EFI\OC\Config.plist`.  It is advisable to store your configured EFI safely and use USB installers to test any new updates or features before moving them to your sytem EFI.
  > `Debug:`  The order in which you arrange kexts and SSDTs matters. Try as much as possible to retain the arrangement provided in this EFI. OpenCore Configurator should automatically arrange your files when you add a new one however if your touchpad stops working, compare your current arrangement with the repository provided here and make the necessary corrections.
  
- #### Running downloaded apps and commands in macOS  
  Right click the file and select `Open`.  

Also read up on these.
- [Firmware Drivers](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#firmware-drivers)
- [Kexts](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#kexts)
- [SSDTs or DSDTs](https://dortania.github.io/OpenCore-Install-Guide/ktext.html#laptop-input)

## 1. Making the USB Installer
*Requires a 16GB+ USB 2.0 (or higher) storage device.*

You can prepare the USB installer using [macOS](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html), [Windows](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html#downloading-macos), or [Linux](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/linux-install.html). 
I have linked each individual guides to the OS names highlighted. Please go through the guide for your preferred OS. I recommend using a real Mac or a macOS virtual machine to create the installer in order to follow conveniently with this guide. 

At this point, you have created a macOS Big Sur USB Installer. Now, you'd need to make it bootable. You'd also need to continue the rest of this guide on a real Mac or a macOS virtual machine.

### Configuring your EFI Folder
Clone this repository, unzip the file and copy the EFI folder of your preferred macOS version to your newly created EFI partition. This EFI is pretty much ready to go, however a few things need to be set before you are ready for installation and after you've installed macOS.  

Download [MountEFI](https://github.com/corpnewt/MountEFI) and [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/) if you haven't. OpenCore Configurator is an alternative to [ProperTree](https://github.com/corpnewt/ProperTree) which provides easy-to-use GUI however, do not use it to download/update kexts. Simply copy and replace the particular kext in `EFI\OC\Kexts`. 

- #### PlatformInfo
You need to set the Serial Number, UUID, MLB, and ROM for your hackintosh. This can all be set in the `Config.plist` located in `EFI\OC\Config.plist`. Open the file with OpenCore Configurator and navigate to `PlatformInfo -> DataHub - Generic - PlatformNVRAM`. Select the closest MacBook version to your processor from the list at the bottom. 

You can set the correct value for your ROM under `Generic` tab if you have the Mac Address of your Wi-Fi module. If you don't have it, follow [this](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#fixing-rom) part of the OpenCore Guide. This step is essential in order to have iServices work immediately. Follow this [guide](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html) if iServices don't work immediately after installation.

After setting your SMBIOS, while still in OpenCore Configurator, head over to `Kernel` and uncheck `CustomSMBIOSGUID` quirk.

- #### Kernel: Wi-Fi and Bluetooth
If you are using the stock Intel Wi-Fi and Bluetooth module, you can skip this step.  

However, if you are using a Broadcom module (check this [list](https://www.reddit.com/r/hackintosh/wiki/faq#wiki_wifi_compatibility) for macOS compatible modules), make sure to download acidanthera's BRCM kexts for [Wi-Fi](https://github.com/acidanthera/AirportBrcmFixup/releases) and [Bluetooth](https://github.com/acidanthera/BrcmPatchRAM/releases). Copy:  
- `AirportBrcmFixup.kext`  
- `BrcmBluetoothInjector.kext`  
- `BrcmFirmwareData.kext`  
- `BrcmPatchRAM3.kext`  

to `EFI\OC\Kexts` and also to `Config.plist -> Kernel -> Add`. Also, remove Intel kexts: `AirportItlwm`, `IntelBluetoothInjector`, and `IntelBluetoothFirmware` from `EFI\OC\Kexts` and `Config.plist`

> **Monterey**  
> Ensure that `IntelBluetoothInjector.kext` or `BrcmBluetoothInjector.kext` is replaced with `BluetoolFixup.kext`. This comes with [BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM/releases).
> Also, make sure all kexts are updated then set `MinKernel` to 21.00.0 and `MaxKernel` to 20.99.9 in order to prevent Big Sur kexts from loading into Monterey.

> **Fenvi BCM94360NG Wi-Fi Card**  
> If you have opted to use the Fenvi BCM94360NG Wi-Fi card, there is no need to use any Wi-Fi or Bluetooth kext as most macOS Continuity features work out-of-the-box. I recommend removing all Wi-Fi and Bluetooth kexts from your EFI config. However, if you opt to use the Fenvi BCM94360NG Wi-Fi card, you will only be able to use half the speed of your internet connection on macOS due to driver incompatibilities.

## 2. Configuring BIOS
At this point, your USB Installer should be bootable and ready for installation. With the USB installer bootable, all that remains is configuring the BIOS of your Hackintosh-to-be. 

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

## 3. Installing macOS
Refer to this [guide](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#double-checking-your-work) during installation. 

Plug in the USB installer, restart your computer, and press `F12`. This would bring up your Boot Menu. Select the EFI option that has the name of your USB. You should see another set options to select. Select `Install macOS Big Sur` and follow the on-screen instructions when it is booted.

> `Debug:` The installer will restart a couple of times. Ensure that the USB installer is selected after each restart. You can change the Boot Order in your BIOS Configuration.

## 4. Post-Installation
If all goes well, you have successfully installed macOS on your machine with most of the hardware working. Make sure to sign into your Apple account at this point. 

Now it's time to perform post-installations that requires some data created after macOS was installed. Fetch `MountEFI` and `OpenCore Configurator` again. You'd need them to mount EFI and configure some more setting. After setting up post-installations and advanced features, you should copy the installer's EFI folder to your system EFI partition.

### Sleep, Wake, and Hibernation
These features, especially Hibernation seem to be working out of the box on later OpenCore versions. However, constant writing to SSDs through Hibernation reduces their lifespans, and there have even been reports that it can lead to data corruption. In order to disable Hibernation leaving just Sleep and Wake, run the following code in Terminal:
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
### USB Mapping
In direct conjunction with enabling Sleep and Wake, you have to define your USB ports to macOS to have a bug-free sleep cycle. Follow this [part](https://dortania.github.io/OpenCore-Post-Install/usb/intel-mapping/intel.html) of the OpenCore guide to map your USB. 

After following the instructions, `USBmap.kext` would be created. Install that kext to your USB installer EFI partition and proceed.

>`Debug:`  Always-on USB also causes sleep problems in macOS. Ensure it is disabled in your BIOS Configuration.

You now have a 90% working Hackintosh and quite frankly could go on without the next few steps as those require advanced knowledge, patience, and the ability to follow guides thoroughly.

## 5. Advanced Features
Great choice to continue further! Why not since you've already come all this way. All that is left is to get a perfect Power Management going on, activate Touchscreen and install third-party applications to enhance Audio, Touchpad gestures and Thermal Throttling. 

## 🚨 Warning! 
Remember, be patient and read through all the guides before you begin to tweak your PC. If possible, take a picture of your previous settings before making any edit, compare the picture with your editted settings and the guide before you hit the 'OK' button. Ensure you don't tweak anything else in your BIOS that is not included in this next section.

### Enhancing Power Management (CFG-Unlock)
Most BIOS come with an option to set a feature called CFG-Lock (read more about it [here](https://dortania.github.io/OpenCore-Post-Install/misc/msr-lock.html#what-is-cfg-lock)). This feature allows an operating system gain more control over the system's power management. macOS needs such control to effect more stringent power management on your system.

> `Warning!` This step can potentially brick your system. Make sure to read through this next part thoroughly before clicking on any link or downloading any software! If you downloaded the wrong version and your keyboard doesn't work: turn off your computer, take out the battery, hold down the power button for 20+ secs, reinstall the battery and turn your system on again.  

Unfortunately, Lenovo has sealed this feature away. Luckily, this [guide](https://www.reddit.com/r/hackintosh/comments/hz2rtm/cfg_lockunlocking_alternative_method/) can help you get started. Use this version of [RU](https://ruexe.blogspot.com/2019/11/ru-5240370-beta.html) as other versions may not work with your keyboard. `0x3C` is the offset value of this machine.

After you've cleared the CFG-Lock, restart your system and select `VerifyMsrE2` from OpenCore boot options. It should look like [this](https://drive.google.com/file/d/1tItmnh3WlMhKXUy7UtoapPLpg6mEsW-L/view). 

Now boot to macOS, mount your USB installer EFI and disable `AppleXcpmCfgLock` quirk in `Config.plist -> Kernel`. Restart macOS from the USB drive to see if it works.

### Reducing Thermal Throttling (Undervolting)
Download Intel Power Gadget for macOS [here](https://www.intel.com/content/www/us/en/developer/articles/tool/power-gadget.html) and test your machine on `All Thread Frequency`, see if it throttles (caps at 2.8GHz for this machine below 70 degrees). If it does, you may want to consider undervolting. Undervolting your CPU can reduce heat, improve performance, and provide longer battery life. However, if done incorrectly, it may cause an unstable system. My preferred method is using [VoltageShift](https://github.com/sicreative/VoltageShift).

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

> \<CPU> and \<CPUCache> must be the same value. 

> Ensure that `csr-active-config` in `Config.plist -> NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82` is greater than `00000000` (SIP Enabled). I've set it partially enabled without kext signing `03000000`. Check this [part](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/extended/post-issues.html#disabling-sip) of the OpenCore Guide to see the different settings

Reboot your system and test with Intel Power Gadget to see if your system still throttles. Run several Geekbenches and measure how well your machine performs against others in its class.

> `Debug:`  If turbo fails to load on boot, add `VoltageShift.kext` to `EFI\OC\kexts` and install it to `Config.plist -> Kernel -> Add`.

> `Tip:` Create a shortcut to enable or disable Turbo when you need to. You can even have Siri run it for you
<img width="914" alt="image" src="https://user-images.githubusercontent.com/47384524/185748948-455fce32-3aef-464f-aa88-93fb6601a5e9.png">
<img width="913" alt="image" src="https://user-images.githubusercontent.com/47384524/185748863-9153cd0d-f4dc-4c43-adca-89feba1de155.png">

### Enabling Low Frequency Mode
Another step towards achieving good power management is setting the lowest frequency your CPU will output when idle. The processor in this machine can handle a low power state of 800MHz. I recommend [acidanthera](https://github.com/acidanthera)'s [CPUFriend](https://github.com/acidanthera/CPUFriend/releases) kext and [corpnewt](https://github.com/corpnewt)'s [CPUFriendFriend](https://github.com/corpnewt/CPUFriendFriend) data provider kext to achieve this.

Download and install `CPUFriend.kext` to your USB installer EFI folder. Run `CPUFriendFriend.command` and follow the instructions on-screen. Enter `08` for Low Frequency Mode to set it to 800MHz. After you've finished configuring your power options, `CPUFriendDataProvider.kext` will be created in the `Results` folder. Install that kext to your USB installer EFI folder. Reboot your system using the USB installer and launch Intel Power Gadget to confirm `CoreMin` under the `Frequency` tab is around 800MHz (0.8GHz).

### Enabling Touchscreen

`Update:` Touchscreen is activated by default with latest EFI version! However, it doesn't support multitouch. To enable multitouch, continue with this section.
  
You have to patch your System DSDT to enable multi-touch touchscreen. Refer to this [part](https://dortania.github.io/Getting-Started-With-ACPI/#a-quick-explainer-on-acpi) of the OpenCore Guide. Download this decompiler [MaciASL](https://github.com/acidanthera/MaciASL/releases) and open it. It should open your `System DSDT`. Search using `CMD + F` for `TPNL` and scroll down slowly within its french bracket till you see `Method(_CRS, 0, Serialized)`. Delete this section:
```
 If ((OSYS < 0x07DC))
 {
     Return (SBFI) /* \_SB_.PCI0.I2C1.TPNL.SBFI */
 }
 If (Zero)
 {
     Return (ConcatenateResTemplate (SBFB, SBFG))
 }
```
Add this code at the end if it isn't already present:
```
Return (ConcatenateResTemplate (SBFB, SBFI))
```
The method should looks like this afterwards:

![image](https://user-images.githubusercontent.com/47384524/143611671-f1564e45-40ae-4a58-9098-d8ad46cbb692.png)

Save the file as `DSDT.aml` in another directory. Copy this file to your USB installer `EFI\OC\ACPI` folder and also to `Config.plist -> ACPI -> Add`. Make sure it is at the top of the list. Restart macOS through the USB Installer and test your touchscreen.

Consider installing [BetterTouchTool](https://folivora.ai/) to add more gestures to both Touchpad and Touchscreen (Touchscreen behaves like a giant Touchpad)

> To disable touchscreen, remove `SSDT-I2C1_SPED.aml` & `SSDT-I2C2_SPED.aml` (and `DSDT.aml` if you activated multi-touch) from `Config.plist -> ACPI`.

### Enhancing Audio (Not much needed here)
Your audio should be working just fine, however not compared to the Dolby Atmos you are most likely used to. Consider installing [Boom3D](https://www.globaldelight.com/boom/boom-ppc.php?utm_source=google&utm_medium=cpc&utm_campaign=extension3) to optimize your sound.

> **Monterey**  
> Remove `FakePCIID.kext` and `FakePCIID_Intel_HDMI_Audio.kext` as they are not needed any longer.

## 6. Finalizing your Installation
Up to this point, you have been booting from your USB installer. If you want to do away with the installer at boot, you can do so by copying its EFI folder to your system EFI partition.

### Dual Boot
Rearrange your BIOS boot order to desired preferrence. If you have a dual-boot, ensure each boot entry is correctly named. Use [Bootice](https://www.softpedia.com/get/System/Boot-Manager-Disk/Bootice.shtml) to modify your boot entry if you are running Windows. Head over to `BOOTICE -> UEFI` to make the necessary configurations.

### OpenCore Default Boot
To select a default boot entry within OpenCore itself, select the entry and press `CTRL` + `ENTER` to make it default. 

> `Debug:` After rebooting or hiberbating Windows, booting from OpenCore may result in an `ACPI_BIOS_ERROR`. Ensure to boot Windows from your UEFI boot menu after rebooting or hibernating Windows. On Lenovo systems, you can access the boot menu at startup by pressing `F12`.

### Boot Straight to macOS
To boot straight to macOS without going through the OS picker, go to `Config.plist -> Misc -> Boot` and uncheck `Show Picker`. 

> To display the OS picker momentarily while it is disabled, hold `Esc` during boot.

## Additional Information
### Stock Samsung PM981 NVMe SSD 
This SSD (or more precise the Phoenix controller it uses) is known to cause random kernel panics in macOS. Up until now, there was no way to even install macOS on the PM981 and the only option was to replace it with either a SATA or a known working NVMe SSD. However, recently a new set of patches, namely [NVMeFix](https://github.com/acidanthera/NVMeFix) was released. It greatly improves compatibility with non-apple SSDs including the PM981. Thanks to those patches, you can now install macOS, but there is still a chance for kernel panics to occur while booting.

## Acknowledgements
- [acidanthera](https://github.com/acidanthera) for providing almost all kexts and drivers
- [dortania](https://github.com/dortania) for an amazing in-depth guide to hackintoshing.
- [alexandred](https://github.com/alexandred) for providing VoodooI2C
- [RehabMan](https://github.com/rehabman) for providing many laptop hotpatches and guides
- [corpnewt](https://github.com/corpnewt) for providing many of the scripts required to conveniently install macOS
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
- [Baio1977](https://github.com/baio1977) for Touchscreen SSDT.
- Everyone else involved in Hackintosh development
