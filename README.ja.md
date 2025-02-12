# 雨バレル

> このプロジェクトは、スマートウォータータンクに関するものです。水位を測定し、データをサーバーに送信します。サーバーは、ウォーターポンプを制御するために使用できます。ポンプは、Webインターフェイスまたは電報ボットを介して制御できます。 HC-SR04超音波センサーを使用して、水位を測定します。データは、ロラワンゲートウェイを介してTTNに送信されます。

？>元のドキュメントは書かれています[英語](README.md)。翻訳はGoogle翻訳で行われました。エラーが見つかった場合は、それらを無視してください。ありがとう！

* * *

## コンテンツの表

1.  **クイックスタート**
    1.  導入
    2.  ハードウェア
    3.  フラッシュソフトウェア
2.  **ハードウェア**
    1.  センサー
    2.  電源
    3.  ハウジング
    4.  マイクロコントローラー
    5.  ゲートウェイ（オプション）
3.  **組み立て**
    1.  コントローラーへのセンサー
    2.  コントローラーへのパワー
    3.  トラブルシューティング
4.  **設定**
    1.  ttn
        1.  アカウントを作成する
        2.  アプリを作成します
        3.  デコーダーを構成します
        4.  資格情報をコピーします
    2.  デバイス
        1.  ドライバーをダウンロードします
        2.  点滅
        3.  構成
5.  **デバッグ**
    1.  シリアルモニター
    2.  TTNコンソール
    3.  MQTTクライアント
    4.  落とし穴
6.  **データエンジニアリング**
    1.  ノードレッド
    2.  こすります
    3.  Alexaスキル
    4.  Azure Connect

* * *

## クイックスタート

### クイックスタート - はじめに

QuickStartは、Arudinoフレームワークを使用してIoTについてすぐに始めたい人のために作られています。それがどのように機能するかを理解したい場合は、[ドキュメント](#hardware).

### クイックスタート - ハードウェアの概要

次の部分が必要です。

![Overview](_media/hardware/hardware-overview.png ":size=200")

-   ロラチップ付きマイクロコントローラー
-   センサー
-   電源
-   ハウジング

？>部品についてもっと知りたい場合は、[ハードウェアのドキュメント](#Hardware).

### クイックスタート - フラッシュソフトウェア

1.  ボードをコンピューターに接続します
2.  次のボタンをクリックします。

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

？>点滅プロセスについてもっと知りたい場合は、[ドキュメントのセットアップ](#Setup).

## ハードウェア

1.  [センサー](#Sensors)
2.  [電源](#Power-supply)
3.  [ハウジング](#Housing)
4.  [マイクロコントローラー](#Microcontroller)
5.  [ゲートウェイ](#Gateway)

### センサー

水位を測定するには、センサーが必要です。防水性で水タンクで使用できるセンサーを見つけるのは簡単なことではありません。次のセンサーがサポートされ、推奨されています。

#### 初心者

初心者の場合は、安価なセンサーを使用して最初のプロトタイプを構築することをお勧めします。次のセンサーがサポートされ、推奨されています。

| 一部                                                  | 説明                                                                                                                                                                                                                                                                                                                                                                                                      |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![HC-S04 sensor](_media/hardware/sensor-hcsr04.svg) | [HC-SR04超音波センサー](https://amzn.to/3MHNrbJ)センサーは相対的に安価で使いやすいです。防水ではありません。防水ハウジングに入れなければなりません。試してみたい場合は、このセンサーをお勧めします。長期的な使用にはお勧めしません。**HC-SR04**センサーは、距離測定に使用される超音波センサーです。それは高周波の音波を放出し、波がオブジェクトを押した後に跳ね返るのにかかる時間を検出します。この時間は、センサーとオブジェクト間の距離を計算するために使用されます。最大4メートルの範囲があり、Arduino、Raspberry Piなどのマイクロコントローラーをインターフェースできます。HC-SR04は、正確で信頼できる距離センシングを必要とするロボット工学、自動化、セキュリティシステム、およびその他のアプリケーションで一般的に使用されます。 |
| ![](_media/hardware/sensor-vl6180x.svg)             | [VL6180X](https://amzn.to/3zVEFPM)飛行センサーの時間は、相対的に安価で使いやすいです。 VL6180Xレーザー距離モジュールは、レーザーを使用してセンサーとオブジェクト間の距離を測定するセンサーです。これは飛行時間（TOF）センサーです。つまり、レーザーライトがオブジェクトから跳ね返り、センサーに戻るのにかかる時間を測定することを意味します。センサーは防水ではありませんが、より高い鋭敏性があります。防水ハウジングに入れなければなりません。試してみたい場合は、このセンサーをお勧めします。長期的な使用にはお勧めしません。                                                                                                                  |

#### 高度な

そのプロジェクトを長い間使用したい場合は、より高価なセンサーを使用することをお勧めします。次のセンサーがサポートされ、推奨されています。

| 一部                                                                     | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![CQRobot](_media/hardware/sensor-water-CQRobot.svg)                   | [水位センサーに連絡します](https://amzn.to/41sKAaL)このセンサーは、光学原理を利用して液体レベルを検出し、光電気水液レベルセンサーとして知られています。このタイプのセンサーの主な利点の1つは、その優れた感度と機械的部分の欠如であり、頻度が低下することです。センサープローブ自体は、配置方向の点で小さく柔軟であるため、溶液の流出、乾燥、水平レベルなどのさまざまな条件を検出できます。さらに、このセンサーはリマインダーおよびアラームシステムとして機能できます。このデバイスは、内蔵の発光ダイオードとフォトトランスリスターを備えており、充電された部分が制御された液体から完全に分離され、安全性が確保されています。                                                                                                                                                                                                               |
| ![Water proof Ultrasonic Sensor](_media/hardware/sensor-JSN-SR04T.svg) | [防水超音波センサー](https://amzn.to/3MNk4F2)JSN-SR04Tは、ソナーテクノロジーを利用してオブジェクトの距離を検出する超音波センサーモジュールです。このコンパクトで使いやすいモジュールは、高い精度と信頼性を備えているため、ロボット工学、自動化、セキュリティシステムなどの幅広いアプリケーションに理想的な選択肢となります。センサーの検出範囲は最大5メートルで、15度の角度内でオブジェクトを検出できます。 40 kHzの周波数で動作し、分解能が1 cmです。モジュールには、温度補償機能が組み込まれているため、さまざまな温度条件でも安定した正確な測定値が確保されます。**JSN-SR04T**モジュールは、防水性と防塵性のあるケーシングで設計されており、過酷な環境での使用に適しています。 ArduinoやRaspberry Piなどの幅広いマイクロコントローラーとシンプルな3ピンインターフェイスを通じて、シームレスにインストールして統合するのは簡単です。全体として、JSN-SR04T超音波センサーモジュールは、プロジェクトに信頼性の高い正確な距離測定ソリューションを探している人にとっては優れた選択肢です。 |

### 電源

マイクロコントローラーに電源を入れるには、電源が必要です。 18650バッテリーが最良のオプションです。安く、ソーラーパネルで充電できます。ただし、パワーバンクまたはUSB電源を使用することもできます。

| 一部                                                      | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![18650 battery](_media/hardware/hardware-18650.svg)    | バッテリーには多くの種類があります。最も一般的なのは、リチウムイオン、リチウムポリマー、リチウム鉄リン酸リチウムです。**18650バッテリー**リチウムイオンバッテリーです。これはこのプロジェクトに最適なオプションです。安く、ソーラーパネルで充電できます。リチウムイオンで作られており、最大500回充電できます。 18650バッテリーの電圧は3.7Vで、Araound 2200MAHの容量を持つことができます。ソーラーパネルの電圧は5Vと2Wの出力です。ソーラーパネルは3時間でバッテリーを充電できます。センサーには5Vと100MAが必要です。マイクロコントローラーには5Vおよび100MAが必要です。したがって、5Vを取得するには、2つの18650バッテリーとA電圧レギュレーターが必要です。バッテリーは防水ではありません。防水ハウジングに入れなければなりません。また、高温にも注意してください。暑すぎると、バッテリーが爆発する可能性があります。長い間使用したい場合は、このバッテリーをお勧めします。 |
| ![Solar panel](_media/hardware/hardware-solarpanel.svg) | **ソーラーパネル：**私たちは庭にいるので、ソーラーパネルを使用できます。防水で、雨の中で使用できます。多結晶シリコンで作られており、2Wの出力を持っています。ソーラーパネルを購入する場合、少なくとも400mAの5V出力があることをShureにする必要があります。バッテリーを充電するには、充電コントローラーが必要です。幸いなことに、マイクロコントローラーには充電コントローラーが組み込まれています。そのため、ソーラーパネルを直接使用できます。                                                                                                                                                                                                                                       |

### ハウジング

センサーとマイクロコントローラーを保護するには、ハウジングが必要です。住宅は防水性があり、高温や紫外線に少し耐性がある必要があります。
使用**PETG**プロトタイプに適しています。防水ではなく、紫外線で破壊することができます。使用**PETG**長期使用のため。防水性と紫外線耐性です。使用することもできます**腹筋**。防水性と紫外線耐性です。

平**タッパーウェア**良いオプションです。防水性と紫外線耐性です。

### マイクロコントローラー

マイクロコントローラーはシステムの脳です。水位を測定し、データをサーバーに送信する責任があります。次のマイクロコントローラーがサポートされ、推奨されています。

| 一部                                                                  | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Seamuing SX1262 LoRa Modul](_media/hardware/hardware-esplora.svg) | [SX1262 LORAモジュール868を縫います](https://amzn.to/3UFRGq5)LORAモジュールを備えたマイクロコントローラーです。安価で使いやすいです。SX1262は、さまざまなワイヤレス通信アプリケーションで使用するために設計された高度に統合された低電力の長距離トランシーバーです。超低電力消費モードを備えているため、バッテリー寿命が長いバッテリー駆動のアプリケーションに最適です。 SX1262は、LORA変調技術を利用して、最小限の消費電力との長距離通信を可能にします。視線の範囲が最大15 kmで、都市環境では最大2 kmの範囲で、SX1262は長距離ワイヤレス通信アプリケーションに最適です。トランシーバーは860-930 MHz周波数範囲で動作し、幅広い地域の規制要件と互換性があります。また、-148 dBMの高感度を備えており、ノイズの多い信号環境でも信頼できるコミュニケーションを可能にします。 SX1262は、高度に構成可能なインターフェイスで設計されているため、幅広いアプリケーションに簡単に統合できます。また、低電力スタンバイモードも備えており、トランシーバーが使用されていないときに消費電力を削減します。全体として、SX1262は非常に用途が広く信頼性の高いトランシーバーソリューションであり、IoT、スマートメーター、産業の自動化など、幅広いワイヤレス通信アプリケーションに最適です。**防水ではありません。**防水ハウジングに入れなければなりません。試してみたい場合は、このマイクロコントローラーをお勧めします。長期的な使用にはお勧めしません。 |

### ゲートウェイ

TTNマップを確認して、お近くにゲートウェイがあるかどうかを確認してください。近くにゲートウェイがない場合は、ゲートウェイを購入できますが、インターネット接続が必要です。ゲートウェイは、マイクロコントローラーとTTNサーバーの間のブリッジです。次のゲートウェイがサポートされ、推奨されています。

| 一部                                                   | 説明                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![TTN gateway](_media/hardware/hardware-gateway.svg) | [TTN屋内ゲートウェイ](https://amzn.to/3L1x1JN)ゲートウェイは、セキュアなデバイスのアクティベーション、グローバルカバレッジ、簡単なデバイス管理など、さまざまな機能を提供するThings Network V3とシームレスに動作するように設計されています。また、Bluetooth Low Energy（BLE）とWi-Fiの組み込みサポートを備えており、スマートフォンまたはコンピューターを使用して簡単な構成と管理を可能にします。全体として、屋内ロラワン屋内ゲートウェイTTNV3は、ロラワンネットワークの信頼できる使いやすいゲートウェイを探している人に最適です。手頃な価格でエネルギー効率が高く、商業用および産業用IoTアプリケーションの両方に理想的な選択肢となる機能が詰め込まれています。 |

## 3。アセンブリング

1.  [コントローラーへのセンサー](#sensor-to-controller)
2.  [コントローラーへのパワー](#power-to-controller)
3.  [トラブルシューティング](#trouble-shooting)

### コントローラーへのセンサー

この例は、HC-SR04センサーをマイクロコントローラーに組み立てる方法を示しています。センサーは、4ピンケーブルを使用してマイクロコントローラーに接続されています。黄色のケーブルはトリガーケーブルです。青いケーブルはエコーケーブルです。赤いケーブルは5Vケーブルです。黒いケーブルは接地ケーブルです。

![Schema for ultra sonic sensor](_media/schema/schema-regenfass-ultrasonic.png)

### コントローラーへのパワー

### トラブルシューティング

* * *

#### ロラワン

-   ロラワンゲートウェイ

#### マイクロコントローラー

ソフトウェアを実行するためにボードが必要であることは明らかです。ただし、データをTTNに送信するには、LORAチップも必要です。次のボードがサポートされています。

-   [tto lora32](Hardware/TTGOLoRa32.md)
-   [Heltec lora32](Hardware/HeltecLoRa32.md)

### 回路図

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3Dプリント部品

## ソフトウェア

### Arduino

-   [Arduino](Software/Arduino/README.md)

### サーバ

-   [サーバ](Software/Server/README.md)

### 電報ボット

-   [電報ボット](Software/TelegramBot/README.md)

## 貢献する

-   <https://github.com/ttnleipzig/regenfass-hc-sr04/>
-

## ライセンス

[アトリビューション - コマーシャル - 恥ずかしさ4.0 International（CC BY-NC-SA 4.0）](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**あなたは自由にできます：**

-   共有 - 媒体または形式で素材をコピーして再配布する
-   適応 - リミックス、変革、および素材の上に構築します

* * *

_byで作られています[docsify](https://docsify.js.org/)_
