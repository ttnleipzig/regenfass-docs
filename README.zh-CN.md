# 雨桶

> 这个项目是关于一个智能水箱的。它测量水位并将数据发送到服务器。服务器可用于控制水泵。该泵可以通过网络界面或电报机器人进行控制。它使用 HC-SR04 超声波传感器测量水位。数据通过 LoRaWAN 网关发送到 TTN。

## 快速开始

如果您已经拥有硬件并想立即开始，

1.  将您的电路板连接到您的计算机，然后
2.  单击以下按钮：

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

## 硬件

### 部分

以下部分是建议。如果需要，您可以使用其他部件。但是您可能必须更改代码。推荐以下部分：

#### 传感器

要测量水位，您需要一个传感器。要找到一款既防水又能在水箱中使用的传感器并不是一件容易的事。支持并推荐以下传感器：

##### 初学者

-   [HC-SR04超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [Lasersensor](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### 先进的

-   [水传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [防水超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### 罗拉万

-   LoRaWAN网关

#### 微控制器

很明显，您需要一块板来运行该软件。但是你还需要一个 LoRa 芯片来将数据发送到 TTN。支持以下板：

-   [去吃草](Hardware/TTGOLoRa32.md)
-   [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### Schematic

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D 打印零件

-   [水箱](https://www.thingiverse.com/thing:2751000)
-   [水泵](https://www.thingiverse.com/thing:2751000)

## 软件

### 阿杜诺

-   [阿杜诺](Software/Arduino/README.md)

### 服务器

-   [服务器](Software/Server/README.md)

### 电报机器人

-   [电报机器人](Software/TelegramBot/README.md)

## 执照

[署名-非商业性使用-相同方式共享 4.0 国际 (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**您可以自由地：**

-   分享——以任何媒介或格式复制和重新分发材料
-   Adapt——重新混合、转换和构建材料

* * *

_由 ❤️ 制作[文件化](https://docsify.js.org/)_
