[![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]
[![Ahoy Build][release-action-badge]][release-action-link] [![Ahoy Dev Build][dev-action-badge]][dev-action-link]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: https://creativecommons.org/licenses/by-nc-sa/4.0/deed.de
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg

[release-action-badge]: https://github.com/lumapu/ahoy/actions/workflows/compile_release.yml/badge.svg
[release-action-link]: https://github.com/lumapu/ahoy/actions/workflows/compile_release.yml

[dev-action-badge]: https://github.com/lumapu/ahoy/actions/workflows/compile_development.yml/badge.svg
[dev-action-link]: https://github.com/lumapu/ahoy/actions/workflows/compile_development.yml

# This Fork adds some information about building AhoyDTU with ESP32-S3-WROOM-1 and E49-900M20S

- Tested with version 0.8.112 from branch 'development03'
- Use environment 'opendtufusion' or 'opendtufusion-de'
- One can use the build in USB for [flashing](https://docs.espressif.com/projects/esp-idf/en/stable/esp32s3/get-started/establish-serial-connection.html#:~:text=Flash%20Using%20USB&text=The%20USB%20on%20the%20ESP32,that%20release%20the%20BOOT%20button.)
  - The USB on the ESP32-S3 uses the GPIO20 for D+ and GPIO19 for D-. If you are flashing for the first time, you need to get the ESP32-S3 into the download mode manually.
  - To do so, press and hold the BOOT button and then press the RESET button once. After that release the BOOT button.
  - That is: Connect the BOOT pin with GND. Then connect EN pin with GND. Release EN pin and after that release the BOOT pin. 

![schematic](https://github.com/plybrd/ahoy-ESP32-S3-WROOM/blob/development03/doc/Wiring_ESP32_S3-CMT2300A.png) 
(My [assembly](https://github.com/plybrd/ahoy-ESP32-S3-WROOM/blob/development03/doc/Aufbau_ESP32_S3-CMT2300A.png))

Restart ESP32-S3 after flashing. The setup works as usual. In `Settings` disable nRF24L01+ and enable CMT2300A. The pin settings are

| Signal |Pin |
|---|---|
|SCLK| GPIO12|
|SDIO| GPIO13 (MISO)|
|CSB | GPIO10 (CS)|
|FCSB| GPIO48|
|IRQ | GPIO21 |

We use SPI2 main interface (Group 5e) for fast SPI (FSPI) connection.
See [ESP32-S3 datasheet](https://www.espressif.com/sites/default/files/documentation/esp32-s3_datasheet_en.pdf) (p. 17).


# 🖐 Ahoy!
![Logo](https://github.com/lumapu/ahoy/blob/main/doc/logo1_small.png?raw=true)

This repository provides hardware and software solutions for communicating with Hoymiles inverters via radio. Our system allows you to easily obtain real-time values, such as power, current, and daily energy, as well as set parameters like the power limit of your inverter to achieve zero export. You can access these functionalities through our user-friendly web interface, MQTT, or JSON. Our solutions simplify the process of monitoring and fine-tuning your solar panel system to help you achieve your goals.

## Changelog
[latest Release](https://github.com/lumapu/ahoy/blob/main/src/CHANGES.md)
[Development Version](https://github.com/lumapu/ahoy/blob/development03/src/CHANGES.md)


Table of approaches:

| Board  | MI | HM | HMS/HMT | comment | HowTo start |
| ------ | -- | -- | ------- | ------- | ---------- |
| [ESP8266/ESP32, C++](manual/Getting_Started.md) | ✔️ | ✔️ | ✔️ |  👈 the most effort is spent here | [create your own DTU](https://ahoydtu.de/getting_started/) |
| [Arduino Nano, C++](tools/nano/NRF24_SendRcv/) | ❌ | ✔️ | ❌ | |
| [Raspberry Pi, Python](tools/rpi/) | ❌ | ✔️ | ❌ | |
| [Others, C/C++](tools/nano/NRF24_SendRcv/) | ❌ | ✔️ | ❌ |  |

⚠️ **Warning: HMS-XXXXW-2T WiFi inverters are not supported. They have a 'W' in their name and a DTU serial number on its sticker**

## Getting Started
1. [Guide how to start with a ESP module](manual/Getting_Started.md)

2. [ESP Webinstaller (Edge / Chrome Browser only)](https://ahoydtu.de/web_install)

3. [Ahoy Configuration ](manual/ahoy_config.md)

## Our Website
[https://ahoydtu.de](https://ahoydtu.de)

## Success Stories
- [Getting the data into influxDB and visualize them in a Grafana Dashboard](https://grafana.com/grafana/dashboards/16850-pv-power-ahoy/) (thx @Carl)

## Support, Feedback, Information and Discussion
- [Discord Server (~ 7.300 Users)](https://discord.gg/WzhxEY62mB)
- [The root of development](https://www.mikrocontroller.net/topic/525778)

### Development
If you encounter any problems, use the issue tracker on Github. Provide a detailed description of the issue and consider if it is related to our software. This will help us provide effective solutions.

**Contributors are always welcome!**

### Related Projects
- [OpenDTU](https://github.com/tbnobody/OpenDTU)
  <- Our sister project ✨ for Hoymiles HM- and HMS-/HMT-series (for ESP32 only!)
- [hms-mqtt-publisher](https://github.com/DennisOSRM/hms-mqtt-publisher)
  <- a project which can handle WiFi inverters like HMS-XXXXW-2T
