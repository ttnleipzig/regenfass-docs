# 雨桶

> 这个项目是关于一个智能水箱的。它测量水位并将数据发送到服务器。服务器可用于控制水泵。该泵可以通过网络界面或电报机器人进行控制。它使用 HC-SR04 超声波传感器测量水位。数据通过 LoRaWAN 网关发送到 TTN。

* * *

## 表中的内容

1.  **快速开始**
    1.  介绍
    2.  硬件
    3.  闪存软件
2.  **硬件**
    1.  传感器
    2.  电源
    3.  住房
    4.  微控制器
    5.  天线
3.  **组装**
    1.  传感器到控制器
    2.  控制器电源
    3.  Trouble shooting
4.  **设置**
    1.  TTN
        1.  创建账户
        2.  创建应用程序
        3.  配置解码器
        4.  复制凭据
    2.  设备
        1.  下载驱动程序
        2.  闪烁
        3.  配置
5.  **调试**
    1.  串行监视器
    2.  TTN控制台
    3.  MQTT客户端
    4.  Pit falls
6.  **数据工程**
    1.  节点红色
    2.  格拉法纳
    3.  Alexa 技能
    4.  蔚蓝连接

* * *

## 快速开始

### 快速介绍

快速入门专为想要立即开始的人而设计。它不是为想要了解其工作原理的人而设计的。如果你想了解它是如何工作的，你可以阅读[文档](https://ttnleipzig.github.io/regenfass-docs/).如果您想立即开始，可以按照以下步骤操作：

### 快速 - 硬件概述

您需要以下部分：

![Overview](_media/hardware/hardware-overview.png)

-   带 LoRa 芯片的微控制器
-   传感器
-   Power supply
-   住房

?> 如果您想了解更多有关零件的信息，可以阅读[硬件文档](#Hardware).

### Quick-Flash软件

1.  将您的电路板连接到您的计算机，然后
2.  单击以下按钮：

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

## 硬件

1.  传感器
2.  电源
3.  住房
4.  微控制器
5.  天线

### 传感器

要测量水位，您需要一个传感器。要找到一款既防水又能在水箱中使用的传感器并不是一件容易的事。支持并推荐以下传感器：
|部分|说明 |
\| --- \| --- \|
\|![HC-SR04](_media/hardware/sensor-hcsr04.svg)\|[HC-SR04超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)该传感器相对便宜且易于使用。它不防水。你必须把它放在防水外壳里。如果您只是想试用一下，我们推荐这款传感器。不建议长期使用。 |
\|![Laser distance sensor](_media/hardware/sensor-laser.svg)\|[激光传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)该传感器相对便宜且易于使用。与 HC-SRo4 一样，它不防水，但具有更高的精度。你必须把它放在防水外壳里。如果您只是想试用一下，我们推荐这款传感器。不建议长期使用。 |

#### 初学者

-   [HC-SR04超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [激光传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### 先进的

-   [水传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [防水超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

| 部分                                                                | 描述                                                                                                            |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/sensor-hcsr04.svg" width="244" />       | [HC-SR04超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) |
| <img src="_media/hardware/hardware-esplora.svg" width="244" />    | [去吃草](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)           |
| <img src="_media/hardware/hardware-18650.svg" width="144" />      | 18650电池                                                                                                       |
| <img src="_media/hardware/hardware-solarpanel.svg" width="244" /> | 太阳能板                                                                                                          |

### 部分

以下部分是建议。如果需要，您可以使用其他部件。但是您可能必须更改代码。推荐以下部分：

#### 罗拉万

-   LoRaWAN网关

#### 微控制器

很明显，您需要一块板来运行该软件。但是你还需要一个 LoRa 芯片来将数据发送到 TTN。支持以下板：

-   [去吃草](Hardware/TTGOLoRa32.md)
-   [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### 原理图

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D 打印部件

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
