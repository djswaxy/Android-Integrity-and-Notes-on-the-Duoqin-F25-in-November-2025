# beating google and making the DuoQin f25 megacool and usable! aka. notes on the Duoqin f25!
I have imported the Duoqin F25 to Denmark and i'm sharing some important QoL fixes i've implemented on mine that works as of 29.11.2025.
<img width="600" height="800" alt="image" src="https://github.com/user-attachments/assets/dd0dbf7c-b2b8-41ac-a036-a98d16f5471c" />

*First off i want to say you should always double check sources and packages for yourself, and what works for someone may not work for everyone. I do not claim any responsibility if you brick your phone doing this, but if you take proper precautions you should be fine. This guide involves rooting, as it's currently the only way to attain device integrity, which is needed for most banking apps etc.*


### The following tools will be used in the initial process
- [MTKCLIENT](https://github.com/bkerler/mtkclient?tab=readme-ov-file) to make backup, and flash new magisk ROM. 
- [ADB](https://developer.android.com/tools/adb) Android Debug Bridge, check if boot img A or B (for me it was A)
- [MAGISK](https://topjohnwu.github.io/Magisk/install.html) To root the phone!

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

## Getting Basic and Device Integrity, Hiding Root etc.
You will need the following Magisk Modules (always download newest releases):
**NOTE**: After september 2025 Google revised its Play Integrity API to be more aggresive, where as before you would only need PIF and Shamiko we will add two modules to get basic and device integrity
- [PLAYINTEGRITYFORK](https://github.com/osm0sis/PlayIntegrityFork) By osm0sis and chiteroman @xdadevelopers
- [Shamiko](https://github.com/LSPosed/LSPosed.github.io) by LSPOSED
- + required since new google integrity patches
- [Tricky Store](https://github.com/5ec1cff/TrickyStore) 
- [Tricky Addon](https://github.com/KOWX712/Tricky-Addon-Update-Target-List) to configure target list!
- [Zygisk - LSPOSED](https://github.com/LSPosed/LSPosed) you can run native zygisk from magisk but with this module you can also run LSPOSED modules such as HMA:


### 1. Download Play Integrity Fork and Shamiko and Tricky Store + addon and Zygisk/or enable magisk zygisk + KSUwebUI
and then reboot the phone. 
Go under "Configure Denylist" in Magisk settings, DO NOT ENFORCE DENYLIST as Shamiko does this :-3. Then choose all google play services and google play itself, press it and make sure to select all the services relating to these.There should now be an Action Button next to PIF. Press the action button to get a new device fingerprint which you will need!
It will trick google into thinking you are a pixel!


### 2. Press the tricky store action button.
This will let you configure tricky addon. Open the hamburger menu and select all, then deselect unnessecary and press SAVE. then open the menu again and press Keybox, then Valid. Then Set Security Patch and choose "Auto"
### 3. Reboot the phone
Then enable flight mode/disable wifi and mobile data. Go into APPS in settings and delete storage and cache for **Google Play Store** and **Google Play Services**. Wait 2 minutes and enable internet again.
To test for integrity do it directly in the google play store (max 10 checks per hour or google will get suspicious). Press your profile picture, then settings, then about, then press *Play Store version* 7 times
to become a developer. Then go to General, Scroll to developer options and press "Check Integrity" under Play Integrity. now HOPEFULLY! you will get
**Labels: [MEETS_BASIC_INTEGRITY, MEETS_DEVICE_INTEGRITY]** if you don't please retry previous steps regarding magisk modules and/or google it and you will find more things to try. This exact formula worked for me with the DuoQin F25 in November of 2025.
### 4. Optional, install HMA in LSPOSED.
Search for it in the LSPOSED framework or [github](https://github.com/Dr-TSNG/Hide-My-Applist) and install it. Here i recommend making a blacklist and choosing all your rooting apps + termux and other root related apps. Then add the blacklist for all apps you want to hide root from. For example banking apps!
<img width="600" height="250" alt="image" src="https://github.com/user-attachments/assets/2b7c5e84-db79-4435-afa0-970114e9fb46" />


## Now you are :-P rooted and integrity-ied :3 yayyyy!
<img width="1250" height="1500" alt="image" src="https://github.com/user-attachments/assets/51fdf54d-f390-4587-9d45-ed167303138e" />
[pixelart source](https://www.pixilart.com/art/space-af626ff36a50967?ft=topic&ft_id=19)
also thanks to the earlier guides for the Duoqin/Qin [F21 Pro](https://github.com/AlikornSause/Notes-on-QIN-F21-PRO) and [F22 Pro](https://github.com/shuuryou/f22pro) and [this guide](https://binboupan.github.io/2023/08/qin-f22-pro/) too. They were all immensly helpful and while not everything worked, enough did so i could make it work on the F25 and write this guide :3

