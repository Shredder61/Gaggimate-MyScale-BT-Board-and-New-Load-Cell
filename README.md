# Gaggimate-MyScale-BT-Board-and-New-Load-Cell
Provides a correction factor in the display code (myscale.h, myscale.cpp) to calibrate a new load cell.
The original code is intended for a manufacturer-calibrated scale which has a hard-coded calibration in its firmware.
This revision allows for a custom correction factor to be applied to the weight before it is broadcast to the display.
Only the display code is changed, not the controller - The code changes are identified by "//Correction factor added here" - obviously, you will need to figure out your own correction factor for your scale.

Note that these changes will be overwritten if you subsequently update the display firmware via the App UI so you would need to re-do the process below.

You will need to download the latest version of Gaggimate and the Bluetooth scales library.

You will need to use Visual Studio (free) and the platformio IDE plug-in (free).

Note that this change requires the following:

1. Download a copy of the latest Gaggimate repository; https://github.com/jniebuhr/gaggimate to your PC
2. Add this as a new project in Visual Studio
3. Open the platformio.ini file in Visual Studio, remove the call in lib_deps_default to download [https://github.com/<username>/esp-arduino-ble-scales.git] (https://github.com/gaggimate/esp-arduino-ble-scales) otherwise the new build will create a second bluetooth scale library without any of the myscale changes
4. Download the Bluetooth scales (esp-arduino-ble-scales folder) library for ESP on Arduino Framework [(https://github.com/<username>/esp-arduino-ble-scales.git)](https://github.com/gaggimate/esp-arduino-ble-scales) and save it alongside (not inside) the Gaggimate repository on your PC
5. Replace the myscale.h and myscale.cpp files in this folder with the edited (correction factor) files from this Github
6. Add the entire contents of this revised esp-arduino-ble-scales folder into the /lib folder in your local copy of the Gaggimate repository
7. In Visual Studio, ensure that only the display environment is selected for clean/build/upload - this is all you need
8. Clean, Build
9. Connect the Lily display, select the correct COM port, and upload the firmware

You can add a serial monitor output so that you can test the implementation by amending the code to the following (output is original weight, correction factor, new weight):
    Serial.printf("RAW: %ld  BASE: %.3f  FACTOR: %.3f  FINAL: %.3f\n",
                  raw, baseWeight, correctionFactor, finalWeight);
