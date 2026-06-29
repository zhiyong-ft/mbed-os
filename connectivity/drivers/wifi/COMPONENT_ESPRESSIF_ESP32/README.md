# The ESP32 WiFi driver for Mbed OS
The Mbed OS driver for the ESP32 WiFi module.

## Firmware version
The following ESP32 modules and firmware versions have been tested working: ESP32-WROOM-32-AT-V3.4.0.0, ESP32-S2-MINI_AT_Bin_V2.1.0.0, ESP32-S2-MINI-AT-V3.4.0.0, ESP32-S2-MINI-AT-V4.1.1.0, ESP32-S2-MINI-AT-V4.2.0.0, ESP32-C5-AT-v5.0.0.0, ESP32-C5-AT-v5.0.1.0 

## Mbed OS BLE stack using ESP32
You can use the Mbed OS BLE stack with ESP32 by using [esp32-at-ble-stack.lib](https://github.com/d-kato/esp32-at-ble-stack).

## Restrictions
- Setting up an UDP server is not possible

## Note:
Please consider increasing the size of RX buffer of BufferedSerial class that underpins this driver if one of the following use cases are involved:
- ESP32 is used to download large files
- HTTPS is used
- Concurrent HTTP/HTTPS and other network requests such as WS/WSS
- Other thread(s) with higher priority may hog CPU for longer time than it takes to fillup RX buffer
The default RX buffer is limited at 256. Data might be lost while your system is busy handling other tasks. This may even make system unstable. To increase the RX buffer size of BufferedSerial class, please add the following entry into the `target_overrides` section of `mbed_app.json5`, either globally or a particular target.
```
"drivers.uart-serial-rxbuf-size": 2048,
```
