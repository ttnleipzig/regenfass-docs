# barril de lluvia

> Este proyecto trata sobre un tanque de agua inteligente. Mide el nivel del agua y envía los datos a un servidor. El servidor se puede utilizar para controlar la bomba de agua. La bomba se puede controlar a través de una interfaz web o mediante un bot de Telegram. Utiliza un sensor ultrasónico HC-SR04 para medir el nivel del agua. Los datos se envían a TTN a través de una puerta de enlace LoRaWAN.

?> El documento original fue escrito en[Inglés](README.md). La traducción se hizo con Google Translate. Si encuentra algún error, intente ignorarlo. ¡Gracias!

* * *

## Tabla de contenidos

1.  **Inicio rápido**
    1.  Introducción
    2.  Hardware
    3.  programa flash
2.  **Hardware**
    1.  Sensores
    2.  Fuente de alimentación
    3.  Alojamiento
    4.  microcontrolador
    5.  Antena
3.  **Montaje**
    1.  Sensor a controlador
    2.  Alimentación al controlador
    3.  Solución de problemas
4.  **Configuración**
    1.  TTN
        1.  Crear una cuenta
        2.  Crear aplicación
        3.  Configurar decodificador
        4.  Copiar credenciales
    2.  Dispositivo
        1.  Descargar controlador
        2.  Brillante
        3.  Configuración
5.  **depuración**
    1.  monitor de serie
    2.  Consola TTN
    3.  Cliente MQTT
    4.  Trampas
6.  **Ingeniería de datos**
    1.  Nodo ROJO
    2.  Grafana
    3.  Habilidad de Alexa
    4.  conexión azul

* * *

## Inicio rápido

### Inicio rápido - Introducción

El inicio rápido está diseñado para personas que desean comenzar de inmediato y tener un conocimiento profundo sobre IoT con Arudino Framework. Si quieres entender cómo funciona, puedes leer el[documentación](#hardware).

### Inicio rápido: descripción general del hardware

Necesitas las siguientes piezas:

![Overview](_media/hardware/hardware-overview.png)

-   Microcontrolador con chip LoRa
-   Sensor
-   Fuente de alimentación
-   Alojamiento

?> Si quieres saber más sobre las partes, puedes leer el[documentación de hardware](#Hardware).

### Inicio rápido: software flash

1.  Conecte su tablero a su computadora y
2.  Haga clic en el siguiente botón:

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

?> Si quieres saber más sobre el proceso de flasheo, puedes leer el[documentación de configuración](#Setup).

## Hardware

1.  [Sensores](#Sensors)
2.  [Fuente de alimentación](#Power-supply)
3.  [Alojamiento](#Housing)
4.  [microcontrolador](#Microcontroller)
5.  [Antena](#Antenna)

### Sensores

Para medir el nivel del agua necesitas un sensor. No es una tarea fácil encontrar un sensor que sea resistente al agua y pueda usarse en un tanque de agua. Los siguientes sensores son compatibles y recomendados:

| Parte                                                                | Descripción                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/sensor-hcsr04.svg" alt="HC-S$04 sensor" /> | [Sensor ultrasónico HC-SR04](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)El sensor es relativamente barato y fácil de usar. No es resistente al agua. Tienes que ponerlo en una carcasa impermeable. Recomendamos este sensor si solo quieres probarlo. No se recomienda para uso a largo plazo.                                           |
| <img src="_media/hardware/sensor-hcsr04.svg">                        | [Sensor láser](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)El sensor es relativamente barato y fácil de usar. Al igual que el HC-SRo4, no es resistente al agua pero tiene una mayor precisión. Tienes que ponerlo en una carcasa impermeable. Recomendamos este sensor si solo quieres probarlo. No se recomienda para uso a largo plazo. |

#### Principiante

-   [Sensor ultrasónico HC-SR04](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Sensor láser](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### Avanzado

-   [sensor de agua](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Sensor ultrasónico a prueba de agua](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

### Fuente de alimentación

Para alimentar el microcontrolador necesita una fuente de alimentación. La batería 18650 es la mejor opción. Es barato y puedes cargarlo con un panel solar. Pero también puedes usar un banco de energía o una fuente de alimentación USB.

| Parte                                                 | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/hardware-18650.svg" />      | Hay muchos tipos de baterías. Los más comunes son el Ion de Litio, el Polímero de Litio y el Fosfato de Hierro y Litio. El**18650 batería**es una batería de iones de litio. Es la mejor opción para este proyecto. Es barato y puedes cargarlo con un panel solar. Está hecho de iones de litio y se puede cargar hasta 500 veces. La batería 18650 tiene un voltaje de 3,7 V y puede tener una capacidad de alrededor de 2200 mAh. El panel solar tiene un voltaje de 5V y una potencia de 2W. El panel solar puede cargar la batería en 3 horas. Nuestro sensor necesita 5V y 100mA. El microcontrolador necesita 5V y 100mA. Entonces necesitamos dos baterías 18650 y un regulador de voltaje para obtener 5V. La batería no es resistente al agua. Tienes que ponerlo en una carcasa impermeable. También tenga cuidado con las altas temperaturas. La batería puede explotar si está demasiado caliente. Recomendamos esta batería si desea usarla durante mucho tiempo. |
| <img src="_media/hardware/hardware-solarpanel.png" /> | **Panel solar:**Dado que los artículos están en nuestro jardín, podemos usar un panel solar. Es resistente al agua y se puede utilizar bajo la lluvia. Está fabricado en silicio policristalino y tiene una potencia de 2W. Si compra un panel solar, debe asegurarse de que tenga una salida de 5V con al menos 400mA. Para cargar nuestras baterías, necesitamos un controlador de carga. Afortunadamente, el microcontrolador tiene un controlador de carga incorporado. Así que podemos usar el panel solar directamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### Alojamiento

Para proteger el sensor y el microcontrolador necesita una carcasa. La carcasa tiene que ser impermeable y un poco resistente a las altas temperaturas y la radiación UV.
Use PLA solo para prototipos. No es resistente al agua y puede ser destruido por la radiación UV. Use ABS para uso a largo plazo. Es impermeable y resistente a los rayos UV. También puedes usar PETG. Es impermeable y resistente a los rayos UV. Pero no es tan fuerte como el ABS.

Incluso tupperware es una buena opción. Es impermeable y resistente a los rayos UV.

### microcontrolador

El microcontrolador es el cerebro del sistema. Se encarga de medir el nivel del agua y enviar los datos al servidor. Los siguientes microcontroladores son compatibles y recomendados:

| Parte                                              | Descripción                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/hardware-esplora.svg" /> | **tienden a patrocinar:**El TTGO LoRa32 es un microcontrolador con un módulo LoRa. Es barato y fácil de usar. No es resistente al agua. Tienes que ponerlo en una carcasa impermeable. Recomendamos este microcontrolador si solo quiere probarlo. No se recomienda para uso a largo plazo. |

* * *

| Parte                                                             | Descripción                                                                                                                |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/sensor-hcsr04.svg" width="244" />       | [Sensor ultrasónico HC-SR04](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) |
| <img src="_media/hardware/hardware-esplora.svg" width="244" />    | [Rumbo a pastar](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)             |
| <img src="_media/hardware/hardware-18650.svg" width="144" />      | 18650 batería                                                                                                              |
| <img src="_media/hardware/hardware-solarpanel.svg" width="244" /> | Panel solar                                                                                                                |

Las siguientes partes son recomendaciones. Puedes usar otras partes si quieres. Pero puede que tenga que cambiar el código. Se recomiendan las siguientes piezas:

#### LoRaWAN

-   Puerta de enlace LoRaWAN

#### microcontrolador

Es obvio que necesita una placa para ejecutar el software. Pero también necesitas un chip LoRa para enviar los datos a TTN. Se admiten las siguientes placas:

-   [Rumbo a pastar](Hardware/TTGOLoRa32.md)
-   [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### Esquemático

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### Piezas impresas en 3D

## Software

### arduino

-   [arduino](Software/Arduino/README.md)

### Servidor

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
