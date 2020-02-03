[![License: MIT](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/justcallmekoko/ESP32Marauder/blob/master/LICENSE)
<!---[![Build Status](https://travis-ci.com/justcallmekoko/ESP32Marauder.svg?branch=master)](https://travis-ci.com/justcallmekoko/ESP32Marauder)--->

# ESP32 Marauder v0.4.1
<p align="center"><img alt="Marauder logo" src="https://github.com/justcallmekoko/ESP32Marauder/blob/master/pictures/marauder3L.jpg?raw=true" width="300"></p>
<p align="center">
  <b>A suite of WiFi/Bluetooth offensive and defensive tools for the ESP32</b>
  <br><br>
  <a href="https://www.tindie.com/products/justcallmekoko/esp32-marauder/"><img src="https://d2ss6ovg47m0r5.cloudfront.net/badges/tindie-larges.png" alt="I sell on Tindie" width="200" height="104"></a>
</p>

# Table Of Condensation
- [About](#about)
  - [YouTube](#youtube)
  - [Hackster Article](#hackster-article)
  - [Capabilities](#capabilities)
- [Do It Yourself](#do-it-yourself)
  - [Hardware](#hardware)
    - [Connections](#connections)
  - [Flashing Firmware](#flashing-firmware)
    - [Using Arduino IDE](#setting-up-arduino-ide)
  - [Updating Firmware](#updating-firmware)
- [Under Development](#under-development)
- [Special Thanks](#special-thanks)
- [For Sale Now](#for-sale-now)

# About
Sometimes you just gotta do what you gotta do. Am I right, ladies?
The ESP32 Marauder is a suite of WiFi/Bluetooth offensive and defensive tools created for the ESP32 and was originally inspired by [Spacehuhn's](https://github.com/Spacehuhn) [esp8266_deauther](https://github.com/Spacehuhn/esp8366_deauther) project. The tool itself serves as a portable device used to test and analyze WiFi and Bluetooth devices. Use this tool and its firmware with caution as the use of some of its capabilities without explicit consent from the target owner is unlawful in most countries. For more information about this project and how it's assembled, follow the video link below.  
**Note:** Because of espressif's ESP32-IDF, the ESP32 included with Marauder is incapable of transmitting deauthentication frames.

### YouTube
<p align="left"><a href="https://www.youtube.com/watch?v=BGFO1wA29o8"><img alt="Marauder logo" src="https://github.com/justcallmekoko/ESP32Marauder/blob/master/pictures/esp32marauder_thumbnail.jpg" width="500"></a></p>

### Hackster Article
You can check out the marauder article written [here](https://www.hackster.io/news/esp32-marauder-puts-a-bluetooth-wi-fi-pen-testing-toolkit-in-your-pocket-32d389f6e66f) as well as other interesting engineering projects.

## Capabilities
### Current
- Probe Request Sniff: Sniff for WiFi [probe request frames](https://mrncciew.com/2014/10/27/cwap-802-11-probe-requestresponse/) sent by wireless devices
- Beacon Sniff: Sniff [beacon frames](https://en.wikipedia.org/wiki/Beacon_frame) sent by wireless acccess points
- Beacon Spam Random: Spam hundreds of random beacon frames to wireless devices within range
- Rick Roll Beacon: Broadcast the rick roll lyrics as WiFi access points
- Bluetooth Sniffer: Sniff bluetooth devices within range
- Detect Card Skimmers: Detect bluetooth enabled credit card skimmers
- Packet Monitor: Show WiFi packet density on a given channel using a time bar graph
- Deauth Sniff: Detect deauthentication packets sent on all channels
- Draw: Just doodle on the screen or whatever
- Update Firmware: Update Marauder firmware over the air via web interface

### Developing
- Emulate Bluetooth: Emulate a bluetooth device with a specific name

# Do It Yourself

## Hardware
This project requires the following hardware in order to work:
- Any ESP32 Development Board
- 2.8" TFT Touch Screen w/ ili9341
- Jumper Wires
- Breadboard

### Connections
Make the following connections between your 2.8" TFT Screen and your ESP32 board. You may need to refer to a pinout sheet specific to the ESP32 dev board you have chosen. For more infomation about this circuit, please refer to [this schematic](https://github.com/justcallmekoko/ESP32Marauder/blob/master/schematics/Schematic_ESP32-Marauder-2_ESP32-Marauder-2-Schematic_20191007113616_png.png)

| 2.8" TFT | ESP32  |
| -------- | ------ |
| VCC      | VCC    |
| GND      | GND    |
| CS       | GPIO17 |
| RESET    | GPIO5  |
| D/C      | GPIO16 |
| MOSI     | GPIO23 |
| SCK      | GPIO18 |
| LED      | GPIO32 |
| MISO     | GPIO19 |
| T_CLK    | GPIO18 |
| T_CS     | GPIO21 |
| T_DI     | GPIO23 |
| T_DO     | GPIO19 |
| T_IRQ    | N/C    |

## Flashing Firmware
### Using Arduino IDE
1. Install the [Arduino IDE](https://www.arduino.cc/en/main/software)
2. In the Arduino IDE, go to `File`>`Preferences`
3. Add the following URL to `Additional Boards Manager URLs:`
    - https://dl.espressif.com/dl/package_esp32_index.json
4. Go to `Tools`>`Board`>`Boards Manager`, search for `esp32` and install `esp32 by Espressif Systems`
5. Install Spacehuhn's [SimpleList](https://github.com/spacehuhn/SimpleList) library in your Arduino IDE
    - Download the SimpleList repo
    - In the Arduino IDE, go to `Sketch`>`Include Library`>`Add .ZIP Library...` and add the SimpleList-master.zip you just downloaded
<!---6. Install Bodmer's [TFT_eSPI](https://github.com/Bodmer/TFT_eSPI) library in your Arduino IDE--->
6. Install my fork of Bodmer's [TFT_eSPI](https://github.com/justcallmekoko/TFT_eSPI) library in your Arduino IDE
    - Download the TFT_eSPI repo
    - In the Arduino IDE, go to `Sketch`>`Include Library`>`Add .ZIP Library...` and add the TFT-eSPI-master.zip you just downloaded
    - Make the following modifications shown in [this issue](https://github.com/justcallmekoko/ESP32Marauder/issues/2#issuecomment-555695918) to the TFT_eSPI library you just installed
7. Follow [these instructions](https://github.com/me-no-dev/arduino-esp32fs-plugin) for installing ESP32 Spiffs Tool
8. Install the [CH340 Drivers](https://github.com/justcallmekoko/ESP32Marauder/blob/master/Drivers/CH34x_Install_Windows_v3_4.EXE)
9. Download or clone this repository
10. Open `esp32_marauder.ino`
11. Plug your ESP32 into a USB port and select the COM port under `Tools`>`Port`
12. Select `LOLIN D32` under `Tools`>`Boards`
13. Click `ESP32 Sketch Data Upload` and wait for the SPIFFS upload to finish
14. Click the upload button

## Updating Firmware
There are multiple options available to update the Marauder firmware. If you have already built the project from this repo, you can just pull the latest commit and flash the firmware using the Arduino IDE (see [here](#using-arduino-ide)).  
If you own an ESP32 Marauder (v0.4.0 or later) and have not build the project, you can follow these instructions for installing the latest update over the air via Marauder's web interface.  

1. Download the [latest release](https://github.com/justcallmekoko/ESP32Marauder/releases/latest) of the Marauder firmware
2. With Marauder powered on, select the main menu option `Update Firmware`
    - Marauder will display details on screen about the status of the update
3. Connect to the MarauderOTA WiFi network from your computer
    - password: justcallmekoko
4. On your web browser, navigate to `http://192.168.4.1`
5. Enter the username and password
    - Username: admin
    - Password: admin
6. Click the `Browse` button and select the .bin file you downloaded from the releases
7. Click `Update`
    - Marauder will automatically reboot once the update has been applied
  
# Under Development
Currently the ESP32 Marauder has limited firmware capabilities. Most of the work so far has been put into designing the hardware. New firmware features will be added over time and will eventually reach a point where this project will be a fully capable hacking machine.

# Special Thanks
- [Spacehuhn](https://github.com/spacehuhn) for an easy to use linked list library [SimpleList](https://github.com/spacehuhn/SimpleList)
  - Also a well designed menu structure. I adapted it to the TFT GUI because it worked perfectly
- [Bodmer](https://github.com/Bodmer) for a comprehensive TFT touch screen library [TFT_eSPI](https://github.com/Bodmer/TFT_eSPI)
- [HyderHasnain](https://github.com/hyderhasnain) for an adaptable [line graph](https://github.com/hyderhasnain/arduino_touchscreen_controller/blob/master/Code/AccelGraph_Original.ino) to be used as the packet monitor

# For Sale Now
You can buy the ESP32 Marauder using [this link](https://www.tindie.com/products/justcallmekoko/esp32-marauder/)
