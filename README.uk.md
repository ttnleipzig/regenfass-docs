# дощова бочка

> Цей проект про розумний резервуар для води. Він вимірює рівень води та надсилає дані на сервер. Сервер можна використовувати для управління водяним насосом. Керувати насосом можна через веб-інтерфейс або через телеграм-бот. Для вимірювання рівня води використовується ультразвуковий датчик HC-SR04. Дані надсилаються до TTN через шлюз LoRaWAN.

\|[англійська](README.md)\|[Німецький](de-de/README.md)\|

## Обладнання

### Запчастини

Наступні частини є рекомендаціями. Ви можете використовувати інші частини, якщо хочете. Але, можливо, вам доведеться змінити код. Рекомендуються такі частини:

#### Датчики

Для вимірювання рівня води потрібен датчик. Це непросте завдання знайти водонепроникний датчик, який можна використовувати в резервуарі для води. Підтримуються та рекомендуються такі датчики:

##### Початківець

-   [Ультразвуковий датчик HC-SR04](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Лазерний датчик](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### Просунутий

-   [Датчик води](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Водонепроникний ультразвуковий датчик](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### LoRaWAN

-   Шлюз LoRaWAN

#### Мікро контролер

Очевидно, що вам потрібна плата для запуску програмного забезпечення. Але вам також потрібен чіп LoRa, щоб надсилати дані на TTN. Підтримуються такі дошки:

-   [Заголовок на випас](Hardware/TTGOLoRa32.md)
-   [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### Схематичний

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D-друковані частини

-   [Бак для води](https://www.thingiverse.com/thing:2751000)
-   [Водяний насос](https://www.thingiverse.com/thing:2751000)

## програмне забезпечення

### Arduino

-   [Arduino](Software/Arduino/README.md)

### Сервер

-   [Сервер](Software/Server/README.md)

### Telegram бот

-   [Telegram бот](Software/TelegramBot/README.md)

## Ліцензія

[Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**Ви можете:**

-   Поділіться — копіюйте та розповсюджуйте матеріал у будь-якому носії чи форматі
-   Адаптуйте — створюйте ремікси, трансформуйте та надбудовуйте матеріал

* * *

_Зроблено за допомогою ❤️[документувати](https://docsify.js.org/)_
