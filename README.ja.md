# レインバレル

> このプロジェクトは、スマートな水タンクに関するものです。水位を測定し、データをサーバーに送信します。サーバーを使用してウォーターポンプを制御できます。ポンプは、Web インターフェイスまたは電報ボットを介して制御できます。 HC-SR04超音波センサーを使用して水位を測定します。データは LoRaWAN ゲートウェイ経由で TTN に送信されます。

｜[英語](README.md)｜[ドイツ人](de-de/README.md)｜

## ハードウェア

### 部品

次の部分は推奨事項です。必要に応じて、他のパーツを使用できます。ただし、コードを変更する必要がある場合があります。以下の部品が推奨されます。

#### センサー

水位を測るにはセンサーが必要です。防水で水槽内で使用できるセンサーを見つけるのは簡単なことではありません。次のセンサーがサポートされており、推奨されています。

##### 初心者

-   [HC-SR04 超音波センサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [レーザーセンサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### 高度

-   [水センサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [防水超音波センサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### ロラワン

-   LoRaWAN ゲートウェイ

#### ボード

ソフトウェアを実行するにはボードが必要であることは明らかです。ただし、データを TTN に送信するには LoRa チップも必要です。次のボードがサポートされています。

-   [放牧に向かう](Hardware/TTGOLoRa32.md)
-   [ヘルテック LoRa32](Hardware/HeltecLoRa32.md)

### 回路図

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3Dプリント部品

-   [水槽](https://www.thingiverse.com/thing:2751000)
-   [ウォーターポンプ](https://www.thingiverse.com/thing:2751000)

## ソフトウェア

### アルドゥイーノ

-   [アルドゥイーノ](Software/Arduino/README.md)

### サーバ

-   [サーバ](Software/Server/README.md)

### 電報ボット

-   [電報ボット](Software/TelegramBot/README.md)

## ライセンス

[表示-非営利-継承 4.0 国際 (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**あなたは自由にできます：**

-   共有 — 任意の媒体または形式で資料をコピーおよび再配布します
-   適応 — 素材をリミックス、変換、構築する

* * *

_❤️で作られました[文書化する](https://docsify.js.org/)_
