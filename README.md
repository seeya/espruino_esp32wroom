# espruino_esp32wroom
Setting up esp32_wroom with espruino on a mac osx

# Installing the drivers for OSX 
https://github.com/adrianmihalko/ch340g-ch34g-ch34x-mac-os-x-driver


# Installing esptool.py
`pip install esptool`

# Download the firmware
Download the file `espruino_2v00.133_esp32.tgz` at http://www.espruino.com/binaries/travis/master/ the version you like of course.
Then extract it. It should contain `bootloader.bin`, `partitions_espruino.bin` and `espruino_esp32.bin`.

# Flashing the esp32
```
esptool.py    \
        --chip esp32                                \
        --port /dev/tty.SLAB_USBtoUART  			\
        --baud 921600                               \
        --after hard_reset write_flash              \
        -z                                          \
        --flash_mode dio                            \
        --flash_freq 40m                            \
        --flash_size detect                         \
        0x1000 bootloader.bin                       \
        0x8000 partitions_espruino.bin              \
        0x10000 espruino_esp32.bin
 ```

# Installing the Web IDE
https://chrome.google.com/webstore/detail/espruino-web-ide/bleoifhkdalbjfbobjackfdifdneehpo/related

# Setting correct baudrate
In the Web IDE, click on settings (top right cog icon). Go to `connection` and update the baudrate to `115200`.


# References
https://techtutorialsx.com/2017/10/15/esp32-javascript-getting-started-with-espruino/
https://github.com/adrianmihalko/ch340g-ch34g-ch34x-mac-os-x-driver
https://chrome.google.com/webstore/detail/espruino-web-ide/bleoifhkdalbjfbobjackfdifdneehpo/related
https://www.espruino.com/ESP32
https://www.youtube.com/watch?v=IStuUv9eAmE


# ESP8266 NodeMCU
It goes the same for esp8266.

```
esptool.py --port /dev/tty.SLAB_USBtoUART --baud 115200 erase_flash

esptool.py --port /dev/tty.SLAB_USBtoUART --baud 460800 write_flash \
  --flash_freq 80m --flash_mode qio --flash_size 4MB-c1 \
  0x0000 "boot_v1.6.bin" 0x1000 espruino_esp8266_user1.bin \
  0x3FC000  esp_init_data_default.bin 0x3FE000 blank.bin
```

# ESP8266 WeMOS

```
esptool.py --port /dev/tty.wchusbserial1420 --baud 115200 erase_flash
  esptool.py --port /dev/tty.wchusbserial1420 --baud 460800 write_flash \
  --flash_freq 80m --flash_mode qio --flash_size 4MB-c1 \
  0x0000 "boot_v1.6.bin" 0x1000 espruino_esp8266_user1.bin \
  0x3FC000  esp_init_data_default.bin 0x3FE000 blank.bin
```
