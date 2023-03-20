# Regenfass

> Bei diesem Projekt geht es um einen intelligenten Wassertank. Es misst den Wasserstand und sendet die Daten an einen Server. Der Server kann zur Steuerung der Wasserpumpe verwendet werden. Die Pumpe kann über ein Webinterface oder über einen Telegrammbot gesteuert werden. Es verwendet einen HC-SR04-Ultraschallsensor, um den Wasserstand zu messen. Die Daten werden über ein LoRaWAN-Gateway an TTN gesendet.

## Schnellstart

Wenn Sie bereits über die Hardware verfügen und sofort loslegen möchten,

1.  Verbinden Sie Ihr Board mit Ihrem Computer und
2.  klicken Sie auf die folgende Schaltfläche:

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

## Hardware

### Teile

Die folgenden Teile sind Empfehlungen. Sie können andere Teile verwenden, wenn Sie möchten. Möglicherweise müssen Sie jedoch den Code ändern. Folgende Teile werden empfohlen:

#### Sensoren

Um den Wasserstand zu messen, benötigen Sie einen Sensor. Es ist keine leichte Aufgabe, einen Sensor zu finden, der wasserdicht ist und in einem Wassertank verwendet werden kann. Folgende Sensoren werden unterstützt und empfohlen:

##### Anfänger

-   [HC-SR04 Ultraschallsensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Lasersensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### Fortschrittlich

-   [Wassersensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Wasserdichter Ultraschallsensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### LoRaWAN

-   LoRaWAN-Gateway

#### Mikrocontroller

Es ist offensichtlich, dass Sie ein Board benötigen, um die Software auszuführen. Sie benötigen aber auch einen LoRa-Chip, um die Daten an TTN zu senden. Folgende Boards werden unterstützt:

-   [Auf dem Weg zum Grasen](Hardware/TTGOLoRa32.md)
-   [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### Schema

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D-gedruckte Teile

-   [Wassertank](https://www.thingiverse.com/thing:2751000)
-   [Wasserpumpe](https://www.thingiverse.com/thing:2751000)

## Software

### Arduino

-   [Arduino](Software/Arduino/README.md)

### Server

-   [Server](Software/Server/README.md)

### Telegramm-Bot

-   [Telegramm-Bot](Software/TelegramBot/README.md)

## Lizenz

[Namensnennung-Nichtkommerziell-Weitergabe unter gleichen Bedingungen 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**Es steht Ihnen frei:**

-   Teilen – Kopieren und Weitergeben des Materials in jedem Medium oder Format
-   Anpassen – Material neu mischen, transformieren und darauf aufbauen

* * *

_Hergestellt mit ❤️ von[dokumentieren](https://docsify.js.org/)_
