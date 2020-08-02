# Marlin-2.0.x-07-30-2020-bug-fix
 iDJMic updates for CR-10 with MODS

I'm new to the Firmware editing but learning as I go as brought me here with a working compiled firmware.  As updates come and changes to the setup so do the bugs. If you have a similar setup hopefuly this will help you with yours.

YouTube Channel :
https://www.youtube.com/idjmic

Changes so far using Marlin's configuration example for the CR-10.
This was originally a HICTOP CR-10 from Amazon, and uses many of the same parts Creality uses including the original board.

After trying to update and install the bootloader only to fail, we wanted the SKR mini e3 v2.0 but stock was out from the local dealer and we were in a crunch with no working printer, so we went with the one they had in stock a SKR mini e3 v1.2.

MODS Included in this setup and firmware are :
1) BTT SKR mini e3 v1.2
2) BLTouch (mounted front left of nozzle)
3) 81 NeoPixel LED
4) BTT Smart Filament Sensor

* Any other mods we've done are not applicable to the firmware changes.

Some key note changes are :

Configure any mod connections to your specific board in your specific board file:
Mine being the SKR mini e3 v1.2 I had to confirm/edit one line and one file for my BLTouch
...\Marlin\src\pins\stm32f1\pins_BTT_SKR_MINI_E3_common.h
Around Line : 59
// Filament Runout Sensor
//
#ifndef FIL_RUNOUT_PIN
#define FIL_RUNOUT_PIN                    PC15 // "E0-STOP"
// #define FIL_RUNOUT_PIN                    PC12 // "PT-DET" (I have my NeoPixels on PT-DET)
#endif

Next to get my NeoPixels working properly I had to add and edit these files:
...\Marlin\.pio\libdeps\STM32F103RC_btt_512K_USB\Adafruit NeoPixel\Adafruit_NeoPixel.cpp
Around Line : 51
//Locate Delay.h file in your local Marlin copy: Marlin 2.0/Marlin/Marlin/src/HAL/shared/Delay.h
//and enter full path to this file below

#include <..\..\..\..\Marlin\src\HAL\shared\Delay.h>

Outside the regular files needing tweaking these were the changes needed for me to compile and get a working firmware.bin

Go through and tweak the following files to your setup/configuration settings.
Configuration_adv.h
Configuration.h
platformio.ini
(Remember that _Bootscreen.h and _Statusscreen.h were also copied over from the Marlin CR-10 sample configurations so be sure to grab those for YOUR printer).