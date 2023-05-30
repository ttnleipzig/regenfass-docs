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
    5.  Puerta de enlace (opcional)
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

![Overview](_media/hardware/hardware-overview.png ":size=200")

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
5.  [Puerta](#Gateway)

### Sensores

Para medir el nivel del agua necesitas un sensor. No es una tarea fácil encontrar un sensor que sea resistente al agua y pueda usarse en un tanque de agua. Los siguientes sensores son compatibles y recomendados:

#### Principiante

Si eres principiante, te recomendamos usar sensores baratos para construir tu primer prototipo. Los siguientes sensores son compatibles y recomendados:

| Parte                                               | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![HC-S04 sensor](_media/hardware/sensor-hcsr04.svg) | [Sensor ultrasónico HC-SR04](https://amzn.to/3MHNrbJ)El sensor es relativamente barato y fácil de usar. No es resistente al agua. Tienes que ponerlo en una carcasa impermeable. Recomendamos este sensor si solo quieres probarlo. No se recomienda para uso a largo plazo. El**HC-SR04**El sensor es un sensor ultrasónico utilizado para medir distancias. Emite ondas de sonido de alta frecuencia y detecta el tiempo que tardan las ondas en rebotar después de golpear un objeto. Este tiempo se usa para calcular la distancia entre el sensor y el objeto. Tiene un alcance de hasta 4 metros y se puede interconectar con microcontroladores como Arduino, Raspberry Pi, etc. El HC-SR04 se usa comúnmente en robótica, automatización, sistemas de seguridad y otras aplicaciones que requieren detección de distancia precisa y confiable. |
| ![](_media/hardware/sensor-vl6180x.svg)             | [BL6180X](https://amzn.to/3zVEFPM)El sensor de tiempo de vuelo es relativamente barato y fácil de usar. El módulo de distancia láser VL6180X es un sensor que utiliza un láser para medir la distancia entre el sensor y un objeto. Es un sensor de tiempo de vuelo (ToF), lo que significa que mide el tiempo que tarda la luz láser en rebotar en un objeto y regresar al sensor. El sensor no es resistente al agua, pero tiene una mayor precisión. Tienes que ponerlo en una carcasa impermeable. Recomendamos este sensor si solo quieres probarlo. No se recomienda para uso a largo plazo.                                                                                                                                                                                                                                                     |

#### Avanzado

Si desea utilizar ese proyecto durante mucho tiempo, le recomendamos que utilice sensores más caros. Los siguientes sensores son compatibles y recomendados:

| Parte                                                                  | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![CQRobot](_media/hardware/sensor-water-CQRobot.svg)                   | [sensor de nivel de agua de contacto](https://amzn.to/41sKAaL)Este sensor utiliza principios ópticos para detectar niveles de líquido y se conoce como sensor de nivel de líquido de agua fotoeléctrico. Una de las principales ventajas de este tipo de sensor es su excelente sensibilidad y la falta de piezas mecánicas, lo que conduce a una calibración menos frecuente. La sonda del sensor en sí es pequeña y flexible en términos de orientación de ubicación, lo que le permite detectar una variedad de condiciones, como derrames de solución, sequedad y nivel horizontal. Además, este sensor puede funcionar como un sistema de recordatorio y alarma. El dispositivo cuenta con un diodo emisor y un fototransistor integrados, con la parte cargada completamente aislada del líquido controlado, lo que garantiza la seguridad.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ![Water proof Ultrasonic Sensor](_media/hardware/sensor-JSN-SR04T.svg) | [Sensor ultrasónico a prueba de agua](https://amzn.to/3MNk4F2)El JSN-SR04T es un módulo de sensor ultrasónico que utiliza tecnología de sonda para detectar la distancia de los objetos. Este módulo compacto y fácil de usar presenta una alta precisión y confiabilidad, lo que lo convierte en una opción ideal para una amplia gama de aplicaciones que incluyen robótica, automatización y sistemas de seguridad. El sensor tiene un rango de detección de hasta 5 metros y puede detectar objetos dentro de un ángulo de 15 grados. Opera a una frecuencia de 40 kHz y tiene una resolución de 1 cm. El módulo también incluye una función de compensación de temperatura incorporada, lo que garantiza lecturas estables y precisas incluso en condiciones de temperatura variables.**El JSN-SR04T**El módulo está diseñado con una carcasa resistente al agua y al polvo, lo que lo hace adecuado para su uso en entornos hostiles. Es fácil de instalar y se integra a la perfección con una amplia gama de microcontroladores, como Arduino y Raspberry Pi, a través de su sencilla interfaz de tres pines. En general, el módulo de sensor ultrasónico JSN-SR04T es una excelente opción para cualquiera que busque una solución de medición de distancia confiable y precisa para sus proyectos. |

### Fuente de alimentación

Para alimentar el microcontrolador necesita una fuente de alimentación. La batería 18650 es la mejor opción. Es barato y puedes cargarlo con un panel solar. Pero también puedes usar un banco de energía o una fuente de alimentación USB.

| Parte                                                   | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![18650 battery](_media/hardware/hardware-18650.svg)    | Hay muchos tipos de baterías. Los más comunes son el Ion de Litio, el Polímero de Litio y el Fosfato de Hierro y Litio. El**18650 batería**es una batería de iones de litio. Es la mejor opción para este proyecto. Es barato y puedes cargarlo con un panel solar. Está hecho de iones de litio y se puede cargar hasta 500 veces. La batería 18650 tiene un voltaje de 3,7 V y puede tener una capacidad de alrededor de 2200 mAh. El panel solar tiene un voltaje de 5V y una potencia de 2W. El panel solar puede cargar la batería en 3 horas. Nuestro sensor necesita 5V y 100mA. El microcontrolador necesita 5V y 100mA. Entonces necesitamos dos baterías 18650 y un regulador de voltaje para obtener 5V. La batería no es resistente al agua. Tienes que ponerlo en una carcasa impermeable. También tenga cuidado con las altas temperaturas. La batería puede explotar si está demasiado caliente. Recomendamos esta batería si desea usarla durante mucho tiempo. |
| ![Solar panel](_media/hardware/hardware-solarpanel.svg) | **Panel solar:**Ya que estamos en nuestro jardín, podemos usar un panel solar. Es resistente al agua y se puede utilizar bajo la lluvia. Está fabricado en silicio policristalino y tiene una potencia de 2W. Si compra un panel solar, debe asegurarse de que tenga una salida de 5V con al menos 400mA. Para cargar nuestras baterías, necesitamos un controlador de carga. Afortunadamente, el microcontrolador tiene un controlador de carga incorporado. Así que podemos usar el panel solar directamente.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |

### Alojamiento

Para proteger el sensor y el microcontrolador necesita una carcasa. La carcasa tiene que ser impermeable y un poco resistente a las altas temperaturas y la radiación UV.
Usar**PETG**es bueno para los prototipos. No es resistente al agua y puede ser destruido por la radiación UV. Usar**PETG**para uso a largo plazo. Es impermeable y resistente a los rayos UV. También puedes usar**abdominales**. Es impermeable y resistente a los rayos UV.

Incluso**tupperware**es una buena opción Es impermeable y resistente a los rayos UV.

### microcontrolador

El microcontrolador es el cerebro del sistema. Se encarga de medir el nivel del agua y enviar los datos al servidor. Los siguientes microcontroladores son compatibles y recomendados:

| Parte                                                               | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Seamuing SX1262 LoRa Modul](_media/hardware/hardware-esplora.svg) | El[Seamuing SX1262 Módulo LoRa 868](https://amzn.to/3UFRGq5)es un microcontrolador con un módulo LoRa. Es económico y fácil de usar. El SX1262 es un transceptor de largo alcance y baja potencia altamente integrado diseñado para usarse en una variedad de aplicaciones de comunicación inalámbrica. Cuenta con un modo de consumo de energía ultrabajo, lo que lo hace ideal para aplicaciones alimentadas por batería que requieren una batería de larga duración. El SX1262 utiliza la técnica de modulación LoRa, que permite la comunicación de largo alcance con un consumo mínimo de energía. Con un alcance de hasta 15 km en condiciones de visibilidad directa y hasta 2 km en entornos urbanos, el SX1262 es una excelente opción para aplicaciones de comunicación inalámbrica de largo alcance. El transceptor opera en el rango de frecuencia de 860-930 MHz, lo que lo hace compatible con una amplia gama de requisitos regulatorios regionales. También presenta una alta sensibilidad de -148 dBm, lo que permite una comunicación confiable incluso en entornos ruidosos o con señal débil. El SX1262 está diseñado con una interfaz altamente configurable, lo que facilita su integración en una amplia gama de aplicaciones. También cuenta con un modo de espera de bajo consumo, que reduce el consumo de energía cuando el transceptor no está en uso. En general, el SX1262 es una solución de transceptor altamente versátil y confiable que es ideal para una amplia gama de aplicaciones de comunicación inalámbrica, que incluyen IoT, medición inteligente y automatización industrial.**No es resistente al agua.**Tienes que ponerlo en una carcasa impermeable. Recomendamos este microcontrolador si solo quiere probarlo. No se recomienda para uso a largo plazo. |

### Puerta

Consulte el mapa TTN para ver si hay una puerta de enlace cerca de usted. Si no hay una puerta de enlace cerca de usted, puede comprar una puerta de enlace, pero necesita una conexión a Internet. La puerta de enlace es el puente entre el microcontrolador y el servidor TTN. Las siguientes puertas de enlace son compatibles y recomendadas:

| Parte                                                | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![TTN gateway](_media/hardware/hardware-gateway.svg) | [Puerta de enlace interior TTN](https://amzn.to/3L1x1JN)La puerta de enlace está diseñada para funcionar a la perfección con The Things Network v3, que ofrece una variedad de funciones, como activación segura de dispositivos, cobertura global y fácil administración de dispositivos. También cuenta con soporte incorporado para Bluetooth Low Energy (BLE) y Wi-Fi, lo que permite una fácil configuración y administración usando un teléfono inteligente o una computadora. En general, Things Indoor LoRaWAN Indoor Gateway TTNv3 es una excelente opción para cualquiera que busque una puerta de enlace confiable y fácil de usar para su red LoRaWAN. Es asequible, ahorra energía y está repleto de características que lo convierten en una opción ideal para aplicaciones de IoT tanto comerciales como industriales. |

## 3. Montaje

1.  [Sensor a controlador](#sensor-to-controller)
2.  [Alimentación al controlador](#power-to-controller)
3.  [Solución de problemas](#trouble-shooting)

### Sensor a controlador

Este ejemplo ilustra cómo ensamblar el sensor HC-SR04 al microcontrolador. El sensor está conectado al microcontrolador con un cable de 4 pines. El cable amarillo es el cable del gatillo. El cable azul es el cable de eco. El cable rojo es el cable de 5V. El cable negro es el cable de tierra.

![Schema for ultra sonic sensor](_media/schema/schema-regenfass-ultrasonic.png)

### Alimentación al controlador

### Solución de problemas

* * *

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

## Contribuir

-   <https://github.com/ttnleipzig/regenfass-hc-sr04/>
-

## Licencia

[Reconocimiento-NoComercial-CompartirIgual 4.0 Internacional (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**Eres libre de:**

-   Compartir — copiar y redistribuir el material en cualquier medio o formato
-   Adaptar: remezclar, transformar y construir sobre el material.

* * *

_Hecho con ❤️ por[docsificar](https://docsify.js.org/)_
