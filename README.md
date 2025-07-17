# ESP32 OTA Data Partition Files

## Overview
The binary files mentioned below populate the OTA selection data partition at offset `0xe000`, to control which application partition the ESP32 / ESP32-Sx boots into. This is useful for [WipperSnapper](https://github.com/adafruit/Adafruit_Wippersnapper_Arduino/) and with CircuitPython 10's new single-partition layout (no second OTA partition).

## Files

### `boot_ota_app0_0xE000.bin`
- **Use for**: CircuitPython/WipperSnapper applications
- **Source**: Arduino ESP32 BSP (boot_app0.bin)
- **Effect**: Boots directly into OTA app partition 0 (your main application)

### `boot_factory_tinyuf2_0xE000.bin` 
- **Use for**: TinyUF2 bootloader as default
- **Source**: TinyUF2 releases (ota_data_initial.bin) 
- **Effect**: Boots into factory partition (TinyUF2 bootloader), all bytes 0xFF

## Installation
Flash your chosen file to offset `0xe000`:
```
esptool.py write_flash 0xe000 <filename>.bin
```
Or using the web version of esptool (supports downloading, listing, and writing partitions):

[https://tyeth.github.io/read-partitions-esptool-js/](https://tyeth.github.io/read-partitions-esptool-js/)

## Which File to Choose?
- Choose `boot_ota_app0_0xE000.bin` if you want your device to boot directly into the user app `OTA_0` (CircuitPython/WipperSnapper)
- Choose `boot_factory_tinyuf2_0xE000.bin` if you want the device to boot into the `factory` type partition (TinyUF2) by default

## More Information
- [Adafruit Learn Guide showing the partition layout and desribing the change](https://learn.adafruit.com/adafruit-esp32-s2-feather/update-tinyuf2-bootloader-for-circuitpython-10-4mb-boards-only) - ESP32 partition layout changes for CircuitPython 10
- [ESP32 OTA Documentation](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-reference/system/ota.html) - Official ESP32 OTA partition documentation explaing boot order, OTA app partitions, and the OTA selection data partition.
