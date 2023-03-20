# Regenfass

> This project is about a smart water tank. It measures the water level and sends the data to a server. The server can be used to control the water pump. The pump can be controlled via a web interface or via a telegram bot. It uses a  HC-SR04 ultrasonic sensor to measure the water level. The data is sent to TTN via a LoRaWAN gateway.

## Quick start

If you already have the hardware and want to start right away,

1. connect your board to your computer and
2. click on the following button:


<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

## Hardware

### Parts

The following parts are recomnondations. You can use other parts if you want. But you may have to change the code. The following parts are recommended:

#### Sensors

To messure the water level you need a sensor.  It is not an easy task to find a sensor that is waterproof and can be used in a water tank. The following sensors are supported and recommended:

##### Beginner

* [HC-SR04 Ultrasonic Sensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
* [Lasersensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### Advanced

* [Water Sensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
* [Water proof Ultrasonic Sensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### LoRaWAN

* LoRaWAN Gateway

#### Micro controller

It is ovious that you need a board to run the software. But you also need a LoRa chip to send the data to TTN. The following boards are supported:

* [TTGO LoRa32](Hardware/TTGOLoRa32.md)
* [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### Schematic

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D-Printed Parts

* [Water Tank](https://www.thingiverse.com/thing:2751000)
* [Water Pump](https://www.thingiverse.com/thing:2751000)

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
