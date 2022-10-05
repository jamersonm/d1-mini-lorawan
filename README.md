# D1-mini-LoRaWAN
Wesmos D1 Mini Pro + RFM95w LoRaWAN

# TTNHelloWorld - Guide

## Menu

1. [Hardware](#ttn-configurations)  
  1.1 [Wesmos D1 mini pro](#wesmos-d1-mini)  
  1.2 [RFM95w](#rfm95w)  
  1.3 [Schematic](#schematic)  
2. [Software](#software)  
  2.1 [End devices key configuration](#end-devices-key-configuration)  
  2.2 [LMIC library](#lmic-library)  
  2.3 [Pinmap](#pinmap)
3. [TTN Configurations](#ttn-configurations)   
4. [Other issues](#other-issues)  
5. [Credits](#credits)  

## Hardware
#### Wesmos D1 mini
The borad used was Wesmos D1 mini.  
![Wesmos D1 mini](https://www.wemos.cc/en/latest/_images/d1_mini_v4.0.0_5_16x9.png)  
To program by Arduino IDE is necessary add the address http://arduino.esp8266.com/stable/package_esp8266com_index.json on **File > Preferences > Additional Boards Manager URL**  
![Arduino preferences](https://user-images.githubusercontent.com/276504/50922035-c31aea80-1449-11e9-862e-57945f6f8b6a.png)  

#### RFM95w
RFM95w is a LoRa Module.  
![RFM95w](https://5.imimg.com/data5/SELLER/Default/2022/1/NN/XT/WO/1833510/tap-sensor-module-for-arduino-500x500.JPG)    
Its pinmap depends of connections with a microcontroller.

#### Schematic
The pinmap for this board is
```
    .nss = 18,
    .rxtx = LMIC_UNUSED_PIN,
    .rst = 14, 
    .dio = {26, 35, 34},
```

## Software

#### End devices key configuration  
On **`main.ino`**, select the end device activation mode by commenting/uncommenting the option.  
```
#define USE_OTAA
//#define USE_ABP
```
Copy and paste the end device keys on the reserverd variables (lines 13-15 to ABP or lines 22-26 to OTAA)  
In case of OTAA configuration the keys AppEUI and DevEUI must be in lsb format.  
  - You can copy alredy formatted directly by the end device page on TTN. **<>** *Toggle array formatting*, <- -> *Switch byte order*

#### LMIC library
Import [mcci_catena/arduino-lmic](https://github.com/mcci-catena/arduino-lmic) library into your project    
On `/project_config/lmic_project_config.h` comment the line **`#define CFG_us915 1`** and uncomment the line **`//#define CFG_au915 1`**  
This file should be:  
```
// project-specific definitions
//#define CFG_eu868 1
//#define CFG_us915 1
#define CFG_au915 1
//#define CFG_as923 1
// #define LMIC_COUNTRY_CODE LMIC_COUNTRY_CODE_JP      /* for as923-JP; also define CFG_as923 */
//#define CFG_kr920 1
//#define CFG_in866 1
#define CFG_sx1276_radio 1
//#define LMIC_USE_INTERRUPTS
```

#### Pinmap
Set LoRa pins on struct
```
const lmic_pinmap lmic_pins = {
    .nss =  ,
    .rxtx = ,
    .rst =  , 
    .dio = { , , },
};
```

## TTN configurations
For TTN configurations, just follow the guide [TTN Hello World](https://github.com/jamersonm/TTNHelloWorld).

## Other issues
#### hal/hal.h hal_init()
In my tests, I had some issues with the function `hal_init()` on `/arduino-lmic/src/hal/hal.cpp` because duplicity with another function alredy setted on Heltec Lora v2 board to Arduino IDE. So I just change the name of this function and everythings worked fine.



## Credits
