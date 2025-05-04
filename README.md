# The K4 has been merged to the ***sn32_develop*** branch of SonixQMK
I have written this guide when the K4V2 was not merged into SonixQMK after some changes. You should probably just build from there now.
If you run into any issues the branch I made the PR from is still available here: [branch](https://github.com/ephb/qmk_firmware/tree/k4v2_fixes).

The ANSI and ISO version binaries in the release section have been built from there. 
Also some steps in this guide might be outdated. If you encounter issue please open an issue here on GitHub so I can help you and fix it for others.

# Installing QMK on Keychron K4 V2 RGB
This guide will walk you through the steps necessary to flashing [SonixQMK](https://github.com/SonixQMK/qmk_firmware) on a Keychron K4 V2 RGB keyboard.
I have been using SonixQMK for more than 2 years now. Everything works but bluetooth. The necessary driver has been [merged](https://github.com/SonixQMK/qmk_firmware/commit/37a0cb7237300db0aa9882e7cf78631746ffc08c) but the K4V2 needs to be updated to work with that.

This guide and SonixQMK on the K4V2 were made possible by the efforts of [dexter93](https://github.com/dexter93/keychron-k4) and based on the documentation of [CanUnesi/QMK-on-K6](https://github.com/CanUnesi/QMK-on-K6) and [aathma2071/QMK-on-K2V2](https://github.com/aathma2071/QMK-on-K2V2).

These steps are mostly the same as for other keyboards supported by SonixQMK and are documented to help others with the same keyboard to get started more easily.
Fortunately the K4 V2 is one of the easiest to flash because the version and boot pins are located right under the space bar.

Even though repos exist for other models, this guide will only cover the K4 V2 RGB model.

**If you just want to use VIA or get started quickly with a default keymap, you can actually skip to [5. Instructions for VIA](#5-instructions-for-via)**

**There is a small chance that you may brick your keyboard in the flashing process, continue at your own risk. Use an appropriate cable, make sure you won’t lose power during flashing and follow the steps carefully.**

I have not tried reverting to the original firmware so proceed at your own risk.
This guide assumes that you have the stock bootloader and not Sonix Jumploader.


## Contents
[1. Get Sonix Flasher](#1-get-sonix-flasher)

[2. Setting Up the Environment - QMK MSYS](#2-setting-up-the-environment---qmk-msys)

[3. Checking Your MCU and Entering Boot Mode](#3-checking-your-mcu-and-entering-boot-mode)

[4. Flash the Keyboard](#4-flash-the-keyboard)

[5. Instructions for VIA](#5-quick-start-instructions-for-via)

&nbsp; 

## 1. Get Sonix Flasher
 1.1. Go to https://github.com/SonixQMK/sonix-flasher/releases/latest

 1.2. Download "flasher-win.zip"

 1.3. Unzip the archive to a convenient place such as your desktop

 1.4. Open "Sonix Keyboard Flasher.exe" and check whether the keyboard is identified as Keychron.

## 2. Setting Up the Environment - QMK MSYS
 2.1. Download the latest release (QMK_MSYS.exe) from [this repo](https://github.com/qmk/qmk_distro_msys/releases/latest).

 2.2. Run the .exe and follow instructions.

 2.3. Run QMK MSYS

You can hit the windows key and type “QMK MSYS” to find the program

 2.4. Clone the SonixQMK repository

    git clone https://github.com/SonixQMK/qmk_firmware.git
    git checkout sn32_master

    or use this if you want to build the current version for an iso K4

    git clone https://github.com/ephb/qmk_firmware.git
    git checkout k4v2_update

    or use this if you want to build the current version for an ansi K4
    
    git clone https://github.com/PythonDeployer/qmk_firmware_k4.git
    

 2.5. Change directory to qmk_firmware

	cd qmk_firmware

 2.6. Pull the submodules

	make git-submodule

 2.7. Install utilities

	util/qmk_install.sh

>Note: You might need to run this twice if the QMK MSYS terminal is closed in the process.

 2.8. Make default firmware

Depending on your [keyboard layout](https://upload.wikimedia.org/wikipedia/commons/1/14/Physical_keyboard_layouts_comparison_ANSI_ISO.png):
The last paramater is the keymap. Use either *default* or *via* here if you did not make your own. We will use via for this example.

    qmk compile -kb keychron/k4/rgb/v2/ansi -km via
    or
    qmk compile -kb keychron/k4/rgb/v2/iso -km via
    
 2.9. Navigate to the qmk directory

 2.10. Locate and copy the .bin file

Depending on your layout, copy "keychron_k4_rgb_v2_iso_via.bin” or “keychron_k4_rgb_v2_iso_via.bin” to a folder for easily locating it later

## 3. Checking Your MCU and Entering Boot Mode
 3.1. Remove the space bar key to view the version and boot pins

 3.2. Check whether the version is FK52332UB-G Ver10. This is the version I have confirmed working.

 3.3. Disconnect the keyboard and use something to short the boot pins

 3.4. Plug in the keyboard with boot pins shorted

 3.5. Open Sonix Flasher and check if the Keyboard is identified as SN32F248B (bootloader)

**If the SN32 bootloader is correctly identified, proceed to next section else stop at this point and troubleshoot**

 3.6. Remove the tweezers shorting the boot pins

## 4. Flash the Keyboard
 4.1. Make sure you have picked SN32F24x for the device and 0x00 for qmk offset.

 4.2. This is the point of no return, click “Flash QMK…” and choose the .bin file you created. It will flash as soon as you choose the file.

## *Congratulations, you have flashed QMK into your K4!*

## 5. Quick-Start Instructions for VIA

 5.1 Download VIA [here](https://github.com/the-via/releases/releases/). Note that VIA 3.0 is quite old by now but works fine for me.
 
 5.2 Download Prebuilt binaries
[ https://github.com/PythonDeployer/Keychron-k4-qmk/releases/tag/10.0](https://github.com/ephb/QMK-on-K4V2/releases/tag/10bbc1f)
Prebuilt binaries that are built last year are available here.
 
 5.3 Flash: Follow steps 3 and 4 using the .bin file you extracted.

 5.4  Download k4_via_ansi.json or k4_iso.json from the corresponding sub-folders here: [ansi](https://github.com/SonixQMK/qmk_firmware/blob/sn32_develop/keyboards/keychron/k4/rgb/v2/ansi/keymaps/via/k4_via_ansi.json)
  or [iso]([url](https://github.com/SonixQMK/qmk_firmware/blob/sn32_develop/keyboards/keychron/k4/rgb/v2/via_json/k4_iso.json))

 5.5 Open VIA and navigate to settings.

 5.4 Enable show design tab.

 5.5 Navigate to Design tab and load the via_ansi.json to load the K4 design into VIA.
 This step has to be repeated every time you open VIA for a board that has not been approved.

## 6. Recomended Reading
[QMK Keycodes](https://github.com/qmk/qmk_firmware/blob/master/docs/keycodes.md)
