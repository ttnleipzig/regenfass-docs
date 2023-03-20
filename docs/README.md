# Regenfass

> This project is about a smart water tank. It measures the water level and sends the data to a server. The server can be used to control the water pump. The pump can be controlled via a web interface or via a telegram bot. It uses a  HC-SR04 ultrasonic sensor to measure the water level. The data is sent to TTN via a LoRaWAN gateway.

| [English](README.md) | [Deutsch](de-de/README.md) |

## Table of Contents

* [Table of Contents](#table-of-contents)
* [Hardware](#hardware)
  + [Parts](#parts)
  + [Schematic](#schematic)
  + [3D-Printed Parts](#3d-printed-parts)
* [Software](#software)
    - [Arduino](#arduino)
    - [Server](#server)
    - [Telegram Bot](#telegram-bot)
* [License](#license)

## Hardware

### Parts

* HC-SR04 Ultrasonic Sensor
* LoRaWAN Gateway

#### Boards

* [ESP32](Hardware/ESP32.md)

### Schematic

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

---
*Made with ❤️ by [docsify](https://docsify.js.org/)*
