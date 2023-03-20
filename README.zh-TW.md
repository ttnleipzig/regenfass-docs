# 雨桶

> 這個項目是關於一個智能水箱的。它測量水位並將數據發送到服務器。服務器可用於控制水泵。該泵可以通過網絡界面或電報機器人進行控制。它使用 HC-SR04 超聲波傳感器測量水位。數據通過 LoRaWAN 網關發送到 TTN。

\|[英語](README.md)\|[德語](de-de/README.md)\|

## 硬件

### 部分

以下部分是建議。如果需要，您可以使用其他部件。但是您可能必須更改代碼。推薦以下部分：

#### 傳感器

要測量水位，您需要一個傳感器。要找到一款既防水又能在水箱中使用的傳感器並不是一件容易的事。支持並推薦以下傳感器：

##### 初學者

-   [HC-SR04超聲波傳感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Lasersensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### 先進的

-   [水傳感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [防水超聲波傳感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### 羅拉萬

-   LoRaWAN網關

#### 董事會

很明顯，您需要一塊板來運行該軟件。但是你還需要一個 LoRa 芯片來將數據發送到 TTN。支持以下板：

-   [去吃草](Hardware/TTGOLoRa32.md)
-   [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### 原理圖

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D 打印部件

-   [水箱](https://www.thingiverse.com/thing:2751000)
-   [水泵](https://www.thingiverse.com/thing:2751000)

## 軟件

### 阿杜諾

-   [阿杜諾](Software/Arduino/README.md)

### 服務器

-   [服務器](Software/Server/README.md)

### 電報機器人

-   [電報機器人](Software/TelegramBot/README.md)

## 執照

[署名-非商業性使用-相同方式共享 4.0 國際 (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**您可以自由地：**

-   分享——以任何媒介或格式複制和重新分發材料
-   Adapt——重新混合、轉換和構建材料

* * *

_由 ❤️ 製作[文件化](https://docsify.js.org/)_
