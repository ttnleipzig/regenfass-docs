# 雨桶

> 这个项目是关于智能水箱的。它测量水位并将数据发送到服务器。服务器可用于控制水泵。可以通过Web界面或电报机器人控制泵。它使用HC-SR04超声波传感器来测量水位。数据通过Lorawan网关发送到TTN。

？>原始文件写在[英语](README.md)。该翻译是用Google翻译进行的。如果发现任何错误，请尝试忽略它们。谢谢你！

* * *

## 内容表

1.  **Quickstart**
    1.  介绍
    2.  硬件
    3.  闪存软件
2.  **硬件**
    1.  传感器
    2.  电源
    3.  住房
    4.  微控制器
    5.  网关（可选）
3.  **组装**
    1.  传感器到控制器
    2.  控制器的电源
    3.  故障射击
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
    4.  陷阱
6.  **数据工程**
    1.  节点红色
    2.  刮
    3.  Alexa技能
    4.  Azure Connect

* * *

## 快速开始

### 快速开始 - 简介

Quickstart是针对想要立即开始使用Arudino框架对物联网的深刻了解的人们进行的。如果您想了解其工作原理，可以阅读[文档](#hardware).

### 快速启动 - 硬件概述

您需要以下部分：

![Overview](_media/hardware/hardware-overview.png ":size=200")

-   与洛拉芯片的微控制器
-   传感器
-   电源
-   住房

？>如果您想了解更多有关零件的信息，则可以阅读[硬件文档](#Hardware).

### 快速启动 - 闪存软件

1.  将板连接到计算机，
2.  单击以下按钮：

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

？>如果您想了解更多有关闪烁过程的信息，则可以阅读[设置文档](#Setup).

## 硬件

1.  [传感器](#Sensors)
2.  [电源](#Power-supply)
3.  [住房](#Housing)
4.  [微控制器](#Microcontroller)
5.  [网关](#Gateway)

### 传感器

要测量水位，您需要一个传感器。找到防水并可以在水箱中使用的传感器并不是一件容易的事。支持并推荐以下传感器：

#### 初学者

如果您是初学者，我们建议使用便宜的传感器来构建您的第一个原型。支持并推荐以下传感器：

| 部分                                                  | 描述                                                                                                                                                                                                                                                                         |
| --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![HC-S04 sensor](_media/hardware/sensor-hcsr04.svg) | [HC-SR04超声传感器](https://amzn.to/3MHNrbJ)传感器相对便宜且易于使用。它不防水。您必须将其放在防水外壳中。如果您只想尝试一下，我们会建议使用该传感器。不建议长期使用。这**HC-SR04**传感器是用于距离测量的超声传感器。它发出高频声波并检测到击中对象后向后反弹所需的时间。然后，使用此时间来计算传感器和对象之间的距离。它具有多达4米的范围，可以与Arduino，Raspberry Pi等微控制器连接。HC-SR04通常用于机器人技术，自动化，安全系统和其他需要准确且可靠的距离感测的应用程序。 |
| ![](_media/hardware/sensor-vl6180x.svg)             | [VL6180X](https://amzn.to/3zVEFPM)飞行传感器的时间相对便宜且易于使用。 VL6180X激光距离模块是使用激光来测量传感器和对象之间的距离的传感器。这是一个飞行时间（TOF）传感器，这意味着它可以测量激光灯从物体弹起并返回传感器所需的时间。该传感器不是防水的，但具有更高的外观。您必须将其放在防水外壳中。如果您只想尝试一下，我们会建议使用该传感器。不建议长期使用。                                                                     |

#### 先进的

如果您想长时间使用该项目，我们建议使用更昂贵的传感器。支持并推荐以下传感器：

| 部分                                                                     | 描述                                                                                                                                                                                                                                                                                                                                                                          |
| ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![CQRobot](_media/hardware/sensor-water-CQRobot.svg)                   | [接触水位传感器](https://amzn.to/41sKAaL)该传感器利用光学原理检测液位，被称为光电水液位传感器。这种类型的传感器的主要优点是其出色的灵敏度和缺乏机械零件，从而导致校准较少。传感器探针本身在放置方向方面又柔软且灵活，从而可以检测到各种条件，例如溶液溢出，干燥和水平水平。此外，该传感器可以用作提醒和警报系统。该设备具有内置的发射二极管和光晶体管，带电部分完全与受控液体隔离，以确保安全。                                                                                                                                                               |
| ![Water proof Ultrasonic Sensor](_media/hardware/sensor-JSN-SR04T.svg) | [防水超声传感器](https://amzn.to/3MNk4F2)JSN-SR04T是一种超声传感器模块，它利用声纳技术检测物体的距离。这个紧凑且易于使用的模块具有高精度和可靠性，使其成为包括机器人技术，自动化和安全系统在内的广泛应用程序的理想选择。传感器的检测范围高达5米，可以在15度角度检测对象。它以40 kHz的频率运行，分辨率为1 cm。该模块还包括内置温度补偿功能，即使在不同的温度条件下，也可以确保稳定且准确的读数。**JSN-SR04T**模块的设计具有防水和防尘外壳，使其适合在恶劣的环境中使用。通过其简单的三针界面，与广泛的微控制器（例如Arduino和Raspberry Pi）无缝安装和集成。总体而言，JSN-SR04T超声传感器模块是任何寻求为其项目提供可靠且准确的距离测量解决方案的人的绝佳选择。 |

### 电源

要为微控制器供电，您需要电源。 18650电池是最好的选择。它很便宜，您可以用太阳能电池板充电。但是您也可以使用电力库或USB电源。

| 部分                                                      | 描述                                                                                                                                                                                                                                                                                          |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![18650 battery](_media/hardware/hardware-18650.svg)    | 电池有很多类型。最常见的是锂离子，锂聚合物和磷酸锂。这**18650电池**是锂离子电池。这是该项目的最佳选择。它很便宜，您可以用太阳能电池板充电。它是由锂离子制成的，可充电高达500次。 18650电池电压为3.7V，可容纳2200mAh。太阳能电池板的电压为5V，功率为2W。太阳能电池板可以在3小时内为电池充电。我们的传感器需要5V和100mA。微控制器需要5V和100mA。因此，我们需要两个18650电池一个电压调节器才能获得5V。电池不防水。您必须将其放在防水外壳中。还要注意高温。如果电池太热，电池可能会爆炸。如果您想长时间使用它，我们建议使用此电池。 |
| ![Solar panel](_media/hardware/hardware-solarpanel.svg) | **太阳能电池板：**由于我们在花园里，我们可以使用太阳能电池板。它是防水的，可在雨中使用。它由多晶硅制成，功率为2W。如果您购买太阳能电池板，则必须使其具有至少400mA的5V输出。要为电池充电，我们需要一个充电控制器。幸运的是，MicroController具有充电控制器的构建。因此，我们可以直接使用太阳能电池板。                                                                                                                            |

### 住房

为了保护传感器和微控制器，您需要住房。外壳必须防水，并且对高温和紫外线辐射具有抗性。
使用**Petg**对原型有益。它不是防水的，可以被紫外线辐射摧毁。使用**Petg**用于长期使用。它具有防水性和耐紫外线。您也可以使用**腹肌**。它具有防水性和耐紫外线。

甚至**特百惠**是一个不错的选择。它具有防水性和耐紫外线。

### 微控制器

微控制器是系统的大脑。它负责测量水位并将数据发送到服务器。支持并推荐以下微控制器：

| 部分                                                                  | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Seamuing SX1262 LoRa Modul](_media/hardware/hardware-esplora.svg) | 这[Seamuing SX1262 Lora模块868](https://amzn.to/3UFRGq5)是带有LORA模块的微控制器。它便宜且易于使用。SX1262是一款高度集成的低功率，远程收发器，旨在用于各种无线通信应用程序。它具有超低功耗模式，非常适合需要较长电池寿命的电池供电应用。 SX1262利用了Lora调制技术，该技术可以通过最少的功耗来实现远程通信。 SX1262在视线条件下的范围高达15公里，在城市环境中最多可达2公里，是长期无线通信应用程序的绝佳选择。收发器在860-930 MHz频率范围内运行，使其与广泛的区域监管要求兼容。它还具有-148 dbm的高灵敏度，即使在嘈杂或弱信号环境中也可以实现可靠的通信。 SX1262的设计具有高度可配置的接口，使其易于集成到广泛的应用程序中。它还具有低功率待机模式，当不使用收发器时，它会降低功耗。总体而言，SX1262是一种通用和可靠的收发器解决方案，非常适合各种无线通信应用，包括物联网，智能计量和工业自动化。**它不防水。**您必须将其放在防水外壳中。如果您只想尝试一下，我们建议使用此微控制器。不建议长期使用。 |

### 网关

检查TTN地图，以查看您附近是否有网关。如果您附近没有门户，则可以购买网关，但需要互联网连接。网关是微控制器和TTN服务器之间的桥梁。支持并推荐以下网关：

| 部分                                                   | 描述                                                                                                                                                                                                                                       |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![TTN gateway](_media/hardware/hardware-gateway.svg) | [TTN室内门户](https://amzn.to/3L1x1JN)该网关旨在与Things Network V3无缝合作，该网络V3提供了一系列功能，例如安全设备激活，全局覆盖范围和简单的设备管理。它还具有对蓝牙低能（BLE）和Wi-Fi的内置支持，可以使用智能手机或计算机轻松配置和管理。总体而言，对于任何寻求可靠，易于使用的网关的人来说，室内室内室内网关TTNV3都是一个绝佳的选择。它负担得起，能源效率，并带有功能，使其成为商业和工业物联网应用的理想选择。 |

## 3。组装

1.  [传感器到控制器](#sensor-to-controller)
2.  [控制器的电源](#power-to-controller)
3.  [故障射击](#trouble-shooting)

### 传感器到控制器

此示例说明了如何将HC-SR04传感器组装到微控制器上。传感器用4针电缆连接到微控制器。黄色电缆是扳机电缆。蓝色电缆是回声电缆。红色电缆是5V电缆。黑色电缆是接地电缆。

![Schema for ultra sonic sensor](_media/schema/schema-regenfass-ultrasonic.png)

### 控制器的电源

### 故障射击

* * *

#### 洛万

-   Lorawan Gateway

#### 微控制器

很明显，您需要一个董事会来运行该软件。但是您还需要一个Lora芯片将数据发送到TTN。支持以下董事会：

-   [ttgo lora32](Hardware/TTGOLoRa32.md)
-   [Heltec Lora32](Hardware/HeltecLoRa32.md)

### 示意图

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D打印零件

## 软件

### Arduino

-   [Arduino](Software/Arduino/README.md)

### 服务器

-   [服务器](Software/Server/README.md)

### 电报机器人

-   [电报机器人](Software/TelegramBot/README.md)

## 贡献

-   <https://github.com/ttnleipzig/regenfass-hc-sr04/>
-

## 执照

[归因非商业共享4.0国际（CC BY-NC-SA 4.0）](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**您可以自由：**

-   分享 - 以任何媒介或格式复制并重新分配材料
-   适应 - 混音，转换和建立在材料上

* * *

_由❤️制成[文档](https://docsify.js.org/)_
