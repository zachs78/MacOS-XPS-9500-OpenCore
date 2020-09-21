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
|CPU Power Management|Working - idles at 800MHz, boosts to max Turbo frequency|
|Laptop Keyboard|Working|
|Laptop Trackpad|Working|
|Built-in Speakers|Working|
|Built-in Mic|Not working*|
|Hotkeys for audio|Working|
|USB 3.x|Working|
|USB 2.0|Working|
|Fingerprint Sensor|Not working|
|SD Card Slot|Not working|
|Screen brightness|Partial - slider working but no hotkeys|
|Built-in Wifi|Working via HeliPort|
|Built-in Bluetooth|Working|
|Dell USB3.1 dock|Working|
|Ethernet on Dell dock|Working - via driver download|
|Built-in webcam|Working|
|Sleep|Partial - S1 only (can't enter S3 so need to enable "block sleep" in BIOS)|

---
## BIOS Settings
Disable the following
 - VT-d
 - TPM
 - Sleep (Enable block sleep)
 - SD Card slot
 - Touchscreen (if you have one)
 - Secure boot
 - Fingerprint reader
 - Disable CFG Lock (via modGRUBShell)

---
## Important

This EFI was created from scratch using Dortania's vanilla laptop guide with additional info from the Comet Lake setup https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake-plus.html#starting-point

You are strongly advised to read the guide fully before using the EFI in this repository. Do not use the EFI as is. You will need to learn how to replace the serial number with GenSMBios and disable cfg lock at the very least.

Note: If you have an incompatible M.2 SSD, you'll get kernel panic. There are some models of XPS 15 9500 that are equipped with Toshiba M.2 SSD which does not have a 4k sector size and will require a firmware fix. Refer to Dortania's guide for more info https://dortania.github.io/OpenCore-Install-Guide/

---
## How to disable CFG Lock

Select the modGRUBShell option at startup (OpenCore boot selection page).
At the grub prompt, enter the following commands.

```
setup_var CpuSetup 0x3e 0x0
setup_var CpuSetup 0xda 0x0
exit
```

Restart your laptop and boot into the BIOS. Do a factory reset. Now your CFG lock will be disabled. You can confirm that by running the VerifyMSR2 option.

---
## Builtin mic issue

Layout 11 for ALC289 is a bit different to ours unfortunately and while mic works, it causes high CPU usage (100% on one core). If anyone can work out how to follow the instructions here (https://github.com/F0x1c/AppleALC_Instructions) to create a custom AppleALC layout for our codec, please let me know - https://www.insanelymac.com/forum/topic/311293-applealc-%E2%80%94-dynamic-applehda-patching/?page=205&tab=comments#comment-2737928.