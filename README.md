# Practical-notes-for-Duoqin-Qin-F25
I have imported the Duoqin F25 to Denmark and i'm sharing some important QoL fixes i've implemented on mine that works as of 29.11.2025.

*First off i want to say you should always double check sources and packages for yourself, and what works for someone may not work for everyone. I do not claim any responsibility if you brick your phone doing this, but if you take proper precautions you should be fine. This guide involves rooting, as it's currently the only way to attain device integrity, which is needed for most banking apps etc.*
### The following tools will be used in the initial process
- [MTKCLIENT](https://github.com/bkerler/mtkclient?tab=readme-ov-file) to make backup, and flash new magisk ROM. 
- [ADB](https://developer.android.com/tools/adb) Android Debug Bridge, check if boot img A or B (for me it was A)
- [MAGISK] (https://topjohnwu.github.io/Magisk/install.html) To root the phone!

My phone came with the bootloader unlocked and google play store installed by default. That is some hacked chinese ROM with suprisingly no bloatware, just a barebones android version.
I cannot stress how important it is to **not** lock the bootloader if it is already unlocked, this will brick your device. If your phone came with a stock ROM you may not need
to root it as you already may have device integrity, but likely not google play store. Here are the next steps:

### 1. Turn off the phone completely 
After this, take your computer and if you're running it in windows with python as i was write `python mtk_gui.py` then connect your phone with usbc AS YOU HOLD DOWN THE VOLUME DOWN BUTTON AND NO OTHER KEYS!
For me, MTKClient tried to connect but couldnt, so i just disconnected the usbc cable and put it in again as i was holding down the volume down button and it connected. A screen like this should pop up:
 <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/86e8e8a5-a980-4610-8c93-d32dc0aef99e" />
### 2. MOST IMPORTANT STEP: BACKUP THE ENTIRE PHONE!!!
So, you'll want to go to the "Read Partitions" Tab and select all partitions and copy them over to your computer. This takes +-6 Hours but you will need the boot image, which if you lose will be
impossible to find ever again. And it is always good to have a backup anyway and with this you will have a complete device snapshot.
### 3. Find boot slot and make magisk boot img.
In your device backup you will have boot_a.bin and boot_b.bin, for my phone boot slot A was the correct one but it may be different. You should run the ADB command:
`adb shell getprop ro.boot.slot_suffix` 
and you will get out either _A or _B . The result is the correct boot img to copy over to the phone
Once you have copied over the boot image, download the Magisk app. *It should say you have Boot RAMdisk*, if it doesnt try following magisk documentation for recovery.img instead.
In the Magisk app press Install on the first card named "Magisk" then select your boot img. **NOTE:** Magisk takes .img files but mtkclient has .bin files. These are identical and you can rename either boot_a.bim or boot_b.bin to boot_a.img / boot_b.img and magisk will be able to patch them.
### 4. Transfer the patched boot image back to your computer, then connect to MTK client following step 1. 
Go to flash partitions and flash your now magisk patched boot_a.img to the boot_a partiton. DO NOT INTERRUPT THE CONNECTION AS YOU FLASH THE ROM! When mtkclient says its done, disconnect the cable and reboot the phone.
Congratulations, your phone is now rooted with magisk. You now have no play integrity, not even basic but we will get to fixing that below!
