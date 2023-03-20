# barril de lluvia

> Este proyecto trata sobre un tanque de agua inteligente. Mide el nivel del agua y envía los datos a un servidor. El servidor se puede utilizar para controlar la bomba de agua. La bomba se puede controlar a través de una interfaz web o mediante un bot de Telegram. Utiliza un sensor ultrasónico HC-SR04 para medir el nivel del agua. Los datos se envían a TTN a través de una puerta de enlace LoRaWAN.

## Inicio rápido

Si ya tiene el hardware y desea comenzar de inmediato,

1.  conecte su tablero a su computadora y
2.  haga clic en el siguiente botón:

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

## Hardware

### Parts

Las siguientes partes son recomendaciones. Puedes usar otras partes si quieres. Pero puede que tenga que cambiar el código. Se recomiendan las siguientes piezas:

#### Sensores

Para medir el nivel del agua necesitas un sensor. No es una tarea fácil encontrar un sensor que sea resistente al agua y pueda usarse en un tanque de agua. Los siguientes sensores son compatibles y recomendados:

##### Beginner

-   [Sensor ultrasónico HC-SR04](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Sensor láser](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### Avanzado

-   [sensor de agua](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Sensor ultrasónico a prueba de agua](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### LoRaWAN

-   Puerta de enlace LoRaWAN

#### microcontrolador

Es obvio que necesita una placa para ejecutar el software. Pero también necesitas un chip LoRa para enviar los datos a TTN. Se admiten las siguientes placas:

-   [TTGO LoRa32](Hardware/TTGOLoRa32.md)
-   [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### Esquemático

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### Piezas impresas en 3D

-   [Depósito de agua](https://www.thingiverse.com/thing:2751000)
-   [Bomba de agua](https://www.thingiverse.com/thing:2751000)

## Software

### arduino

-   [arduino](Software/Arduino/README.md)

### Server

-   [Servidor](Software/Server/README.md)

### robot de telegramas

-   [robot de telegramas](Software/TelegramBot/README.md)

## Licencia

[Reconocimiento-NoComercial-CompartirIgual 4.0 Internacional (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**Eres libre de:**

-   Compartir — copiar y redistribuir el material en cualquier medio o formato
-   Adaptar: remezclar, transformar y construir sobre el material.

* * *

_Hecho con ❤️ por[docsificar](https://docsify.js.org/)_
