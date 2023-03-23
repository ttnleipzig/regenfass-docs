# 雨桶

> 这个项目是关于一个智能水箱的。它测量水位并将数据发送到服务器。服务器可用于控制水泵。该泵可以通过网络界面或电报机器人进行控制。它使用 HC-SR04 超声波传感器测量水位。数据通过 LoRaWAN 网关发送到 TTN。

?> 原始文件写于[英语](README.md).翻译是用谷歌翻译完成的。如果您发现任何错误，请尽量忽略它们。谢谢你！

* * *

## 表中的内容

1.  **[快速开始](#Quickstart)**
    1.  [介绍](#Quickstart-Introduction)
    2.  [硬件](#Quickstart-Hardware)
    3.  [闪存软件](#Quickstart-Flash-software)
2.  **[硬件](#Hardware)**
    1.  [传感器](#Sensors)
    2.  [电源](#Power-supply)
    3.  [住房](#Housing)
    4.  [微控制器](#Microcontroller)
    5.  [天线](#Antenna)
3.  **组装**
    1.  传感器到控制器
    2.  控制器电源
    3.  故障排除
4.  **设置**
    1.  TTN
        1.  创建账户
        2.  创建应用程序
        3.  Configure Devoder
        4.  复制凭据
    2.  设备
        1.  下载驱动程序
        2.  闪烁
        3.  配置
5.  **调试**
    1.  串行监视器
    2.  TTN控制台
    3.  MQTT客户端
    4.  陷阱
6.  **数据工程**
    1.  节点红色
    2.  格拉法纳
    3.  Alexa 技能
    4.  蔚蓝连接

* * *

## 快速开始

### 快速入门 - 简介

本快速入门专为希望立即开始使用 Arudino 框架深入了解物联网的人员而设计。如果你想了解它是如何工作的，你可以阅读[文档](#hardware).

### 快速入门 - 硬件概述

您需要以下部分：

![Overview](_media/hardware/hardware-overview.png)

-   带 LoRa 芯片的微控制器
-   传感器
-   电源
-   住房

?> 如果您想了解更多有关零件的信息，可以阅读[硬件文档](#Hardware).

### 快速入门 - Flash 软件

1.  将您的电路板连接到您的计算机，然后
2.  单击以下按钮：

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

?> 如果您想了解更多关于刷机过程，您可以阅读[安装文件](#Setup).

## 硬件

1.  [传感器](#Sensors)
2.  [电源](#Power-supply)
3.  [住房](#Housing)
4.  [微控制器](#Microcontroller)
5.  [天线](#Antenna)

### 传感器

要测量水位，您需要一个传感器。要找到一款既防水又能在水箱中使用的传感器并不是一件容易的事。支持并推荐以下传感器：

| 部分                                                                   | 描述                                                                                                                                                                                       |
| -------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/sensor-hcsr04.svg" alt="HC-S$04 sensor" /> | [HC-SR04超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)该传感器相对便宜且易于使用。它不防水。你必须把它放在防水外壳里。如果您只是想试用一下，我们推荐这款传感器。不建议长期使用。               |
| <img src="_media/hardware/sensor-hcsr04.svg">                        | [激光传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)该传感器相对便宜且易于使用。与 HC-SRo4 一样，它不防水，但具有更高的精度。你必须把它放在防水外壳里。如果您只是想试用一下，我们推荐这款传感器。不建议长期使用。 |

#### 初学者

-   [HC-SR04超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [激光传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### 先进的

-   [水传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [防水超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

### 电源

要为微控制器供电，您需要一个电源。 18650电池是最好的选择。它很便宜，你可以用太阳能电池板给它充电。但您也可以使用移动电源或 USB 电源。

| 部分                                                    | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/hardware-18650.svg" />      | **18650电池：** The 18650 battery is the best option. It is cheap and you can charge it with a solar panel. It is made of Lithium Ion and can be charged up to 500 times. 18650 battery has a voltage of 3.7V and can have a capacity of araound 2200mAh. The solar panel has a voltage of 5V and a power of 2W. The solar panel can charge the battery in 3 hours. Our sensor needs 5V and 100mA. The microcontroller needs 5V and 100mA. So we need two 18650 batteries an a voltage regulator to get 5V. The battery is not waterproof. You have to put it in a waterproof housing. Also take care about high temperatures. The battery can explode if it is too hot. We recommend this battery if you want to use it for a long time. |
| <img src="_media/hardware/hardware-solarpanel.png" /> | **太阳能板：**太阳能电池板不是必需的，但与电池一起使用是最佳选择。太阳能电池板是防水的，可以在雨中使用。它由多晶硅制成，功率为2W。如果您购买太阳能电池板，则必须确保它具有至少 400mA 的 5V 输出。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |

### 住房

为了保护传感器和微控制器，您需要一个外壳。外壳必须是防水的，并且能够抵抗高温和紫外线辐射。
仅将 PLA 用于原型。它不防水，会被紫外线辐射破坏。长期使用ABS。它防水且抗紫外线。您也可以使用 PETG。它防水且抗紫外线。但它没有 ABS 强。

甚至特百惠也是一个不错的选择。它防水且抗紫外线。

### 微控制器

微控制器是系统的大脑。它负责测量水位并将数据发送到服务器。支持并推荐以下微控制器：

| 部分                                                 | 描述                                                                                                 |
| -------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/hardware-esplora.svg" /> | **倾向于光顾：**TTGO LoRa32 是一款带有 LoRa 模块的微控制器。它便宜且易于使用。它不防水。你必须把它放在防水外壳里。如果您只是想尝试一下，我们推荐这款微控制器。不建议长期使用。 |

* * *

| 部分                                                                | 描述                                                                                                            |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/sensor-hcsr04.svg" width="244" />       | [HC-SR04超声波传感器](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) |
| <img src="_media/hardware/hardware-esplora.svg" width="244" />    | [去吃草](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)           |
| <img src="_media/hardware/hardware-18650.svg" width="144" />      | 18650电池                                                                                                       |
| <img src="_media/hardware/hardware-solarpanel.svg" width="244" /> | 太阳能板                                                                                                          |

以下部分是建议。如果需要，您可以使用其他部件。但是您可能必须更改代码。推荐以下部分：

#### 罗拉万

-   LoRaWAN Gateway

#### 微控制器

很明显，您需要一块板来运行该软件。但是你还需要一个 LoRa 芯片来将数据发送到 TTN。支持以下板：

-   [去吃草](Hardware/TTGOLoRa32.md)
-   [Heltec LoRa32](Hardware/HeltecLoRa32.md)

### 原理图

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D 打印零件

## 软件

### Arduino

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
