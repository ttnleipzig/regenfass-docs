# Regenfass

> This project is about a smart water tank. It measures the water level and sends the data to a server. The server can be used to control the water pump. The pump can be controlled via a web interface or via a telegram bot. It uses a  HC-SR04 ultrasonic sensor to measure the water level. The data is sent to TTN via a LoRaWAN gateway.

---

## Table Of Content

1. **Quickstart**
   1. Introduction
   2. Hardware
   3. Flash software
2. **Hardware**
   1. Sensors
   2. Power supply
   3. Housing
   4. Microcontroller
   5. Antenna
3. **Assembeling**
   1. Sensor to controller
   2. Power to controller
   3. Trouble shooting
4. **Setup**
   1. TTN
      1. Create Account
      2. Create App
      3. Configure Devoder
      4. Copy Credentials
   2. Device
      1. Download driver
      2. Flashing
      3. Configuration
5. **Debugging**
   1. Serial Monitor
   2. TTN Console
   3. MQTT Client
   4. Pit falls
6. **Data Engineering**
   1. Node RED
   2. Grafana
   3. Alexa Skill
   4. Azure Connect

---

## Quick start

### Quick - Introduction

The quickstart is made for people who want to start right away. It is not made for people who want to understand how it works. If you want to understand how it works, you can read the [documentation](https://ttnleipzig.github.io/regenfass-docs/). If you want to start right away, you can follow the following steps:

### Quick - Hardware overview

You need the following parts:

![Overview](_media/hardware/hardware-overview.png)

* Microcontroller with LoRa chip
* Sensor
* Power supply
* Housing

?> If you want to know more about the parts, you can read the [hardware documentation](#Hardware).

### Quick - Flash software

1. Connect your board to your computer and
2. Click on the following button:

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

## Hardware

   1. Sensors
   2. Power supply
   3. Housing
   4. Microcontroller
   5. Antenna
  
### Sensors

To messure the water level you need a sensor.  It is not an easy task to find a sensor that is waterproof and can be used in a water tank. The following sensors are supported and recommended:
| Part | Description |
| --- | --- |
|  ![HC-SR04](_media/hardware/sensor-hcsr04.svg)| [HC-SR04 Ultrasonic Sensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) The sensor is relativly cheap and easy to use. It is not waterproof. You have to put it in a waterproof housing. We recoment this sensor if you just want to try it out. It is not recommended for long term use. | 
|  ![Laser distance sensor](_media/hardware/sensor-laser.svg) | [Lasersensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) The sensor is relativly cheap and easy to use. As like the HC-SRo4 it is not waterproof but has a higher acuracy. You have to put it in a waterproof housing. We recoment this sensor if you just want to try it out. It is not recommended for long term use. |

#### Beginner

* [HC-SR04 Ultrasonic Sensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
* [Lasersensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### Advanced

* [Water Sensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
* [Water proof Ultrasonic Sensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

| Part | Description |
| --- | --- |
|  <img src="_media/hardware/sensor-hcsr04.svg" width="244" /> | [HC-SR04 Ultrasonic Sensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) |
|  <img src="_media/hardware/hardware-esplora.svg" width="244" /> | [TTGO LoRa32](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) |
|  <img src="_media/hardware/hardware-18650.svg" width="144" /> | 18650 battery |
|  <img src="_media/hardware/hardware-solarpanel.svg" width="244" /> | Solar panel |

### Parts

The following parts are recomnondations. You can use other parts if you want. But you may have to change the code. The following parts are recommended:

#### LoRaWAN

* LoRaWAN Gateway

#### Micro controller

It is ovious that you need a board to run the software. But you also need a LoRa chip to send the data to TTN. The following boards are supported:

* [TTGO LoRa32](Hardware/TTGOLoRa32.md)
* [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### Schematic

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D-Printed Parts


## Software

### Arduino

* [Arduino](Software/Arduino/README.md)

### Server

* [Server](Software/Server/README.md)

### Telegram Bot

* [Telegram Bot](Software/TelegramBot/README.md)

## License

[Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**You are free to:**

* Share — copy and redistribute the material in any medium or format
* Adapt — remix, transform, and build upon the material

---
*Made with ❤️ by [docsify](https://docsify.js.org/)*
