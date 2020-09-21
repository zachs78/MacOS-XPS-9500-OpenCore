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
|Laptop Headphones Jack|Not working - distorted sound|
|Built-in Speakers|Working - missing subwoofer|
|Built-in Mic|Working|
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
|Other peripherals on Dell dock|Working|
|Built-in webcam|Working|
|Sleep|Partial - S1 only (Sleep wake failure in EFI. Need to enable "block sleep" in BIOS)|

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

Note: You are recommended to get an M.2 SSD or SATA drive that is compatible with Mac OS. If you have an incompatible M.2 SSD, you'll get kernel panic. There are some models of XPS 15 9500 that are equipped with Toshiba M.2 SSD which does not have a 4k sector size and will require a firmware fix. Refer to Dortania's guide for more info https://dortania.github.io/OpenCore-Install-Guide/

---

## How to disable CFG Lock

This is specific to XPS 15 9500 only (along with its sibling models and previous gen).

Select the modGRUBShell option at startup (OpenCore boot selection page).
At the grub prompt, enter the following commands (the first line unlocks CFG, the second line unlocks overclocking).

```
setup_var CpuSetup 0x3e 0x0
setup_var CpuSetup 0xda 0x0
exit
```

Restart your laptop and boot into the BIOS. Do a factory reset. Now your CFG lock will be disabled. You can confirm that by running the VerifyMSR2 option.

If you update your BIOS, you may need to do this again but so far Dell has been kind to us.

---

## Built-in speaker / headphones jack issue

Layout 11 for ALC289 is a bit different to ours unfortunately. The XPS 9500 has a subwoofer pin config that gets wired to physical subwoofers in the laptop. This config isn't available on any other laptops. The headphones jack on the right side of the laptop isn't working properly either (distorted sound).

It is likely that we need to create our own ALC289 layout. If anyone can work out how to follow the instructions here (https://github.com/F0x1c/AppleALC_Instructions) to create a custom AppleALC layout for our codec, please let me know here where I have also posted the codec dump for the ALC289 specific to our laptop - https://www.insanelymac.com/forum/topic/311293-applealc-%E2%80%94-dynamic-applehda-patching/?page=205&tab=comments#comment-2737928.

The headphones jack on the Dell dock is working fine however, as it uses an external USB audio.