# 雨樽

> このプロジェクトはスマート給水タンクに関するものです。水位を測定し、データをサーバーに送信します。サーバーを使用してウォーターポンプを制御できます。ポンプは、Web インターフェイスまたは電報ボット経由で制御できます。超音波センサーHC-SR04を使用して水位を測定します。データは LoRaWAN ゲートウェイ経由で TTN に送信されます。

?> 元の文書は次のように書かれていました。[英語](README.md)。翻訳はGoogle翻訳で行いました。エラーを見つけた場合は無視してください。ありがとう！

* * *

## 目次

1.  **クイックスタート**
    1.  導入
    2.  ハードウェア
    3.  フラッシュソフトウェア
2.  **ハードウェア**
    1.  センサー
    2.  電源
    3.  ハウジング
    4.  マイクロコントローラー
    5.  ゲートウェイ (オプション)
3.  **組み立て**
    1.  センサーからコントローラーまで
    2.  コントローラーへの電源供給
    3.  トラブルシューティング
4.  **設定**
    1.  TTN
        1.  アカウントを作成する
        2.  アプリの作成
        3.  デコーダの構成
        4.  認証情報のコピー
    2.  デバイス
        1.  ドライバーをダウンロードする
        2.  点滅
        3.  構成
5.  **デバッグ**
    1.  シリアルモニター
    2.  TTN コンソール
    3.  MQTT クライアント
    4.  落とし穴
6.  **データエンジニアリング**
    1.  ノードRED
    2.  グラファナ
    3.  アレクサスキル
    4.  Azure コネクト

* * *

## クイックスタート

### クイックスタート - はじめに

クイックスタートは、Arudino Framework を使用して IoT についての深い知識を持ち、すぐに始めたい人向けに作成されています。それがどのように機能するかを理解したい場合は、を読むことができます[ドキュメンテーション](#hardware)。

### クイックスタート - ハードウェアの概要

次の部品が必要です。

![Overview](_media/hardware/hardware-overview.png ":size=200")

-   LoRaチップを搭載したマイクロコントローラー
-   センサー
-   電源
-   ハウジング

?> パーツについて詳しく知りたい場合は、[ハードウェアのドキュメント](#Hardware)。

### クイックスタート - Flash ソフトウェア

1.  ボードをコンピュータに接続し、
2.  次のボタンをクリックします。

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

?> フラッシュ プロセスについて詳しく知りたい場合は、次のドキュメントを参照してください。[セットアップドキュメント](#Setup)。

## ハードウェア

1.  [センサー](#Sensors)
2.  [電源](#Power-supply)
3.  [ハウジング](#Housing)
4.  [マイクロコントローラー](#Microcontroller)
5.  [ゲートウェイ](#Gateway)

### センサー

水位を測定するにはセンサーが必要です。防水で水槽内で使用できるセンサーを見つけるのは簡単ではありません。次のセンサーがサポートされており、推奨されます。

#### 初心者

初心者の場合は、安価なセンサーを使用して最初のプロトタイプを作成することをお勧めします。次のセンサーがサポートされており、推奨されます。

| 一部                                                  | 説明                                                                                                                                                                                                                                                                                                                                                                                           |
| --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![HC-S04 sensor](_media/hardware/sensor-hcsr04.svg) | [HC-SR04 超音波センサー](https://amzn.to/3MHNrbJ)センサーは比較的安価で使いやすいです。防水ではありません。防水ケースに入れる必要があります。ただ試してみたい場合には、このセンサーをお勧めします。長期間の使用はお勧めできません。の**HC-SR04**センサーは距離測定に使用される超音波センサーです。高周波音波を放射し、音波が物体に衝突してから反射するまでの時間を検出します。この時間は、センサーと物体の間の距離を計算するために使用されます。最大 4 メートルの範囲があり、Arduino、Raspberry Pi などのマイクロコントローラーと接続できます。HC-SR04 は、ロボティクス、オートメーション、セキュリティ システム、および正確で信頼性の高い距離感知を必要とするその他のアプリケーションでよく使用されます。 |
| ![](_media/hardware/sensor-vl6180x.svg)             | [BL6180X](https://amzn.to/3zVEFPM)飛行時間センサーは比較的安価で使いやすいです。 VL6180X レーザー距離モジュールは、レーザーを使用してセンサーと物体間の距離を測定するセンサーです。これは飛行時間型 (ToF) センサーであり、レーザー光が物体で反射してセンサーに戻るまでの時間を測定します。センサーは防水ではありませんが、精度は高くなります。防水ケースに入れる必要があります。ただ試してみたい場合には、このセンサーをお勧めします。長期間の使用はお勧めできません。                                                                                                                                 |

#### 高度な

そのプロジェクトを長期間使用したい場合は、より高価なセンサーを使用することをお勧めします。次のセンサーがサポートされており、推奨されます。

| 一部                                                                     | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![CQRobot](_media/hardware/sensor-water-CQRobot.svg)                   | [接触水位センサー](https://amzn.to/41sKAaL)このセンサーは光学原理を利用して液位を検出するもので、光電式水液位センサーとして知られています。このタイプのセンサーの大きな利点の 1 つは、感度が優れていることと、機械部品がないため、校正の頻度が少なくて済むことです。センサープローブ自体が小型で設置方向に柔軟に対応できるため、溶液の流出、乾燥、水平レベルなどのさまざまな状態を検出できます。さらに、このセンサーはリマインダーおよびアラームシステムとしても機能します。発光ダイオードとフォトトランジスタを内蔵しており、帯電部分は管理液体から完全に隔離されており、安全性を確保しています。                                                                                                                                                                                                                     |
| ![Water proof Ultrasonic Sensor](_media/hardware/sensor-JSN-SR04T.svg) | [防水超音波センサー](https://amzn.to/3MNk4F2)JSN-SR04Tは、ソナー技術を利用して物体の距離を検出する超音波センサーモジュールです。このコンパクトで使いやすいモジュールは、高い精度と信頼性を備えており、ロボティクス、オートメーション、セキュリティ システムなどの幅広いアプリケーションに最適です。センサーの検出範囲は最大 5 メートルで、15 度以内の角度内の物体を検出できます。周波数 40 kHz で動作し、分解能は 1 cm です。このモジュールには温度補償機能も組み込まれており、さまざまな温度条件下でも安定した正確な読み取り値を保証します。**JSN-SR04T**モジュールは防水性と防塵性を備えた筐体で設計されており、過酷な環境での使用に適しています。インストールが簡単で、シンプルな 3 ピン インターフェイスを通じて、Arduino や Raspberry Pi などの幅広いマイクロコントローラーとシームレスに統合できます。全体として、JSN-SR04T 超音波センサー モジュールは、プロジェクトに信頼性が高く正確な距離測定ソリューションを探している人にとって優れた選択肢です。 |

### 電源

マイクロコントローラーに電力を供給するには、電源が必要です。 18650 バッテリーが最良の選択肢です。安いしソーラーパネルで充電できる。ただし、モバイルバッテリーや USB 電源を使用することもできます。

| 一部                                                      | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![18650 battery](_media/hardware/hardware-18650.svg)    | 電池にはたくさんの種類があります。最も一般的なものは、リチウムイオン、リチウムポリマー、リン酸鉄リチウムです。の**18650バッテリー**リチウムイオン電池です。それがこのプロジェクトにとって最良の選択肢です。安いしソーラーパネルで充電できる。リチウムイオン素材を採用しており、最大500回の充電が可能です。 18650 バッテリーの電圧は 3.7V で、容量は約 2200mAh です。ソーラーパネルの電圧は5V、出力は2Wです。ソーラーパネルは3時間でバッテリーを充電できます。私たちのセンサーには 5V と 100mA が必要です。マイクロコントローラーには 5V と 100mA が必要です。したがって、5Vを得るには2つの18650バッテリーと電圧レギュレーターが必要です。バッテリーは防水ではありません。防水ケースに入れる必要があります。高温にも注意してください。バッテリーが熱すぎると爆発する可能性があります。長く使いたい場合はこちらのバッテリーをおすすめします。 |
| ![Solar panel](_media/hardware/hardware-solarpanel.svg) | **ソーラーパネル：**庭にあるのでソーラーパネルが使えます。防水加工が施されており、雨の中でも使用可能です。多結晶シリコン製で、出力は2Wです。ソーラーパネルを購入する場合は、少なくとも 400mA の 5V 出力を備えていることを確認する必要があります。バッテリーを充電するには、充電コントローラーが必要です。幸いなことに、マイクロコントローラーには充電コントローラーが組み込まれているので、ソーラーパネルを直接使用できます。                                                                                                                                                                                                                                  |

### ハウジング

センサーとマイクロコントローラーを保護するには、ハウジングが必要です。ハウジングは防水性があり、高温や紫外線に対して多少の耐性がある必要があります。
使用**PETG**プロトタイプに適しています。防水ではないため、紫外線により劣化する可能性があります。使用**PETG**長期使用に。防水性と耐紫外線性があります。も使用できます**ABS**。防水性と耐紫外線性があります。

平**タッパーウェア**良い選択肢です。防水性と耐紫外線性があります。

### マイクロコントローラー

マイクロコントローラーはシステムの頭脳です。水位を測定し、データをサーバーに送信する役割を果たします。次のマイクロコントローラーがサポートされており、推奨されます。

| 一部                                                                  | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![Seamuing SX1262 LoRa Modul](_media/hardware/hardware-esplora.svg) | の[Seamuing SX1262 LoRa モジュール 868](https://amzn.to/3UFRGq5)LoRaモジュールを搭載したマイクロコントローラーです。安価で使いやすい SX1262 は、さまざまな無線通信アプリケーションで使用するために設計された、高度に統合された低電力、長距離トランシーバーです。超低消費電力モードを備えているため、長いバッテリ寿命を必要とするバッテリ駆動のアプリケーションに最適です。 SX1262 は、最小限の電力消費で長距離通信を可能にする LoRa 変調技術を利用しています。 SX1262 は、見通し内条件で最大 15 km、都市環境で最大 2 km の通信範囲を備えており、長距離無線通信アプリケーションに最適です。トランシーバーは 860 ～ 930 MHz の周波数範囲で動作するため、幅広い地域の規制要件に適合します。また、-148dBmの高感度を実現し、騒音や電波の弱い環境でも安定した通信が可能です。 SX1262 は、高度に構成可能なインターフェイスを備えて設計されているため、幅広いアプリケーションに簡単に統合できます。また、トランシーバーが使用されていないときの電力消費を削減する低電力スタンバイモードも備えています。全体として、SX1262 は汎用性が高く信頼性の高いトランシーバー ソリューションであり、IoT、スマート メーター、産業オートメーションなどの幅広い無線通信アプリケーションに最適です。**防水ではありません。**防水ケースに入れる必要があります。ただ試してみたい場合には、このマイコンをお勧めします。長期間の使用はお勧めできません。 |

### ゲートウェイ

TTN マップをチェックして、近くにゲートウェイがあるかどうかを確認してください。近くにゲートウェイがない場合は、ゲートウェイを購入できますが、インターネット接続が必要です。ゲートウェイは、マイクロコントローラーと TTN サーバー間のブリッジです。次のゲートウェイがサポートされており、推奨されています。

| 一部                                                   | 説明                                                                                                                                                                                                                                                                                                                                                                                                             |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![TTN gateway](_media/hardware/hardware-gateway.svg) | [TTN 屋内ゲートウェイ](https://amzn.to/3L1x1JN)ゲートウェイは、安全なデバイスのアクティベーション、グローバル カバレッジ、簡単なデバイス管理などのさまざまな機能を提供する The Things Network v3 とシームレスに連携するように設計されています。また、Bluetooth Low Energy (BLE) と Wi-Fi のサポートも組み込まれているため、スマートフォンやコンピューターを使用して簡単に設定および管理できます。全体として、Things Indoor LoRaWAN 屋内ゲートウェイ TTNv3 は、LoRaWAN ネットワーク用の信頼性が高く使いやすいゲートウェイを探している人にとって優れた選択肢です。手頃な価格でエネルギー効率が高く、商用および産業用 IoT アプリケーションの両方にとって理想的な選択肢となる機能が満載です。 |

## 3. 組み立て

1.  [センサーからコントローラーまで](#sensor-to-controller)
2.  [コントローラーへの電源供給](#power-to-controller)
3.  [トラブルシューティング](#trouble-shooting)

### センサーからコントローラーまで

この例では、HC-SR04 センサーをマイクロコントローラーに組み立てる方法を示します。センサーは 4 ピン ケーブルでマイクロコントローラーに接続されています。黄色のケーブルはトリガーケーブルです。青いケーブルはエコー ケーブルです。赤いケーブルは5Vケーブルです。黒いケーブルはアースケーブルです。

![Schema for ultra sonic sensor](_media/schema/schema-regenfass-ultrasonic.png)

### コントローラーへの電源供給

### トラブルシューティング

* * *

#### LoRaWAN

-   LoRaWAN ゲートウェイ

#### マイクロコントローラー

ソフトウェアを実行するにはボードが必要であることは明らかです。ただし、データを TTN に送信するには LoRa チップも必要です。次のボードがサポートされています。

-   [ラアへ向かう](Hardware/TTGOLoRa32.md)
-   [ヘルテック LoRa32](Hardware/HeltecLoRa32.md)

### 回路図

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3D プリント部品

## ソフトウェア

### Arduino

-   [Arduino](Software/Arduino/README.md)

### サーバ

-   [サーバ](Software/Server/README.md)

### 電報ボット

-   [電報ボット](Software/TelegramBot/README.md)

## 貢献する

-   [ｈっｔｐｓ：／／ぎてゅｂ。こｍ／っｔんぇいｐじｇ／れげんふぁっｓーｈｃーｓｒ０４／](https://github.com/ttnleipzig/regenfass-hc-sr04/)
-

## ライセンス

[表示 - 非営利 - 継承 4.0 インターナショナル (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**次のことを自由に行うことができます。**

-   共有 — マテリアルを任意の媒体または形式でコピーして再配布します
-   適応 — 素材をリミックス、変換し、構築します

* * *

_❤️で作りました[文書化する](https://docsify.js.org/)_
