# Monoprice-36739-Sous-Vide-custom_firmware

Instructions, tips, and information about DP IDs, ESPHome firmware, and integrating the 1100W Strata Home by Monoprice Smart Sous Vide Precision Cooker Powered by STITCH Wireless with Home Assistant.

DPs and ESPHome yaml below. See the [Wiki](/wiki) for more info and full wrietup.

If you would like a deeper dive on how to obtain DP IDs (or other Tuya-related information), or how to set up ESPHome, check out the Wiki in my similar [heater repository](https://github.com/Ninja1283/HS-1500-WIFI_Heat_Storm_Phoenix-1500-Watt_Smart_Wall_Mounted_Heater/wiki).

## Background

I've tried to avoid Tuya devices (and cloud-based devices in general) when making IOT product selections, but by the end of the recent holiday season, I ended up with two Tuya devices: a Sous Vide stick, and a infrared heater. (For the purpose of this project, we'll focus on the Sous Vide. I have a separate repository for the Heater [here](https://github.com/Ninja1283/HS-1500-WIFI_Heat_Storm_Phoenix-1500-Watt_Smart_Wall_Mounted_Heater))

I briefly tried using the HA Tuya Integrations, but both options seemed a bit clunky and limiting, and the Sous Vide completely disconnected twice. The second time this happened, I notcied that the discovery network followed the same ESP_XXXXXX common among other Espressif ESP based devices. After using the MAC address to confirm that it was indeed an Espressif compatible (TYWE1S) Wifi module, I decided it was time to reflash the device.

I learned a bit along the way, and thought I would share my experiences, as many of existing guides and tips that I found are now out of date.

## Product Infomation

The product in question is [this](https://www.monoprice.com/product?p_id=36739) WiFi-enabled 1100W Sous Vide stick. Product manual can be found [here](https://downloads.monoprice.com/files/manuals/36739_Manual_190422.pdf).

## DP IDs

|Description|DP Code|Data Type|DP ID|Values|
|:-|:-|:-|:-|:-|
|Power|poweronoff|Boolean|101|0=off, 1=on|
|Status|workstatus|Enum|102|0=off, 1=working, 2=keepwarm|
|Set Temperature|tempset|Integer|103|Int range (200-950)\*|
|Current Temperature|tempshow|Integer|104|Int range (200-950)\*|
|Set Time|settime|Integer|105|Int range (0-5999)\*\*|
|Remaining Time|remainingtime|Integer|106|Int range (0-5999)\*\*|
|Fault|fault|Bitmap|107|0x00=clear, 0x01=fault|
|Set Temperature Units|tempchanger|Boolean|108|0=°F, 1=°C|
|Recipe|recipe|Integer|109|Int range (1-999)\*\*\*|

*Raw temperature values are 10x actual temperature. The Tuya MCU divides by ten to get the appropriate decimal values.

**Raw time values are in minutes. You can create a helper entity in HA if you want them reported in an easier to read HH:MM format.

***I will be customizing my own "recipes", and will skip the factory recipes for the sake of simplicity.

## ESPHome yaml

[sousvide.yaml](/docs/sousvide.yaml)

## Acknowledgements

@ssieb for their insight on using the climate component in ESPHome

@blakadder for their information about DP IDs
