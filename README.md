# Monoprice-36739-Sous-Vide-custom_firmware
Instructions, tips, and tricks for obtaining DP IDs, creating and flashing custom firmware, and working with the 1100W Strata Home by Monoprice Smart Sous Vide Precision Cooker Powered by STITCH Wireless.

## Background:
I've tried to avoid Tuya devices (and cloud-based devices in general) when making IOT product selections, but by the end of the recent holiday season, I ended up with two Tuya devices: a Sous Vide stick, and a infrared heater. (For the purpose of this project, we'll focus on the Sous Vide, and address the heater in a later project.)

I briefly tried using the HA Tuya Integrations, but both options seemed a bit clunky and limiting, and the Sous Vide completely disconnected twice. The second time this happened, I notcied that the discovery network followed the same ESP_XXXXXX common among other Espressif ESP based devices. After using the MAC address to confirm that it was indeed an Espressif Wifi module, I decided it was time to reflash the device.

I learned a bit along the way, and thought I would share my experiences, as many of existing guides and tips that I found are now out of date.

## Obtaining DP IDs and 
The first product in question is [this](https://www.monoprice.com/product?p_id=36739) Wifi-enabled 1100W Sous Vide Cooker.

Like many Tuya IOT devices, this unit has an MCU to handle the machine operation, and the Wifi MCU only handles wireless duties, communicating back and forth to the main MCU via serial. Since it uses a secondary Tuya MCU, it is important that we map out the DP IDs before disassembly or flashing.

There is a good guide here on how to obtain the DP IDs [here](https://www.zigbee2mqtt.io/advanced/support-new-devices/03_find_tuya_data_points.html).
