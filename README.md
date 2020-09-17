# Dell XPS 9500 macOS X

This is an OpenCore EFI that allows you to install and boot macOS X Catalina on your Dell XPS 15 9500 (2020).

<b>OpenCore Version:</b> 0.6.0

<b>macOS Version:</b> Catalina 10.15.6 (19G2021)

![alt text](https://github.com/zachs78/MacOS-XPS-9500-OpenCore/blob/master/OpenCore-Catalina-XPS-15-9500.png?raw=true)

---

## Functional Status
|Function / Hardware|Status|
|-|-|
|iGPU UHD630 Acceleration|Working|
|CPU Power Management|Working - idles at 800MHz|
|Laptop Keyboard|Working|
|Laptop Trackpad|Working|
|Built-in Speakers|Working|
|Built-in Mic|Not working|
|Hotkeys for audio|Working|
|USB 3.x|Working|
|USB 2.0|Working|
|Fingerprint Sensor|Not working|
|SD Card Slot|Not working|
|Screen brightness|Partial - no hotkeys|
|Built-in Wifi|Working via HeliPort|
|Built-in Bluetooth|Working|
|Dell USB3.1 dock|Working|
|Ethernet from Dell dock|Working - via driver download|
|Built-in webcam|Working|
|Sleep|Partial - Can't enter S3 so need to enable "block sleep" in BIOS|

---
## BIOS Settings
Disable the following
 - VT-d
 - TPM
 - Sleep (Enable block sleep)
 - SD Card slot
 - Touchscreen (if you have one)
 - Non M.2 SATA ports
 - Secure boot
 - Fingerprint reader

---
## Important

This EFI was created from scratch using Dortania's vanilla laptop guide with additional info from the Comet Lake setup https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake-plus.html#starting-point

You are strongly advised to read the guide fully before using the EFI in this repository. Do not use the EFI as is. You will need to learn how to replace the serial number with GenSMBios at the very least.

Note: If you have an incompatible M.2 SSD, you'll get kernel panic. There are some models of XPS 15 9500 that are equipped with Toshiba M.2 SSD which does not have a 4k sector size and will require a firmware fix. Refer to Dortania's guide for more info https://dortania.github.io/OpenCore-Install-Guide/

