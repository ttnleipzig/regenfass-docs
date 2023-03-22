# レインバレル

> このプロジェクトは、スマートな水タンクに関するものです。水位を測定し、データをサーバーに送信します。サーバーを使用してウォーターポンプを制御できます。ポンプは、Web インターフェイスまたは電報ボットを介して制御できます。 HC-SR04超音波センサーを使用して水位を測定します。データは LoRaWAN ゲートウェイ経由で TTN に送信されます。

* * *

## 目次

1.  **クイックスタート**
    1.  序章
    2.  ハードウェア
    3.  フラッシュソフトウェア
2.  **ハードウェア**
    1.  センサー
    2.  電源
    3.  ハウジング
    4.  マイクロコントローラ
    5.  アンテナ
3.  **組み立て**
    1.  センサーからコントローラー
    2.  コントローラへの電源
    3.  トラブルシューティング
4.  **設定**
    1.  TTN
        1.  アカウントを作成する
        2.  アプリの作成
        3.  デコーダーの構成
        4.  資格証明のコピー
    2.  デバイス
        1.  ドライバをダウンロード
        2.  点滅
        3.  構成
5.  **デバッグ**
    1.  シリアルモニター
    2.  TTN コンソール
    3.  MQTT クライアント
    4.  落とし穴
6.  **データエンジニアリング**
    1.  ノードレッド
    2.  グラファーナ
    3.  アレクサスキル
    4.  アズール コネクト

* * *

## クイックスタート

### クイック - はじめに

クイックスタートは、すぐに始めたい人向けです。それがどのように機能するかを理解したい人のために作られていません.それがどのように機能するかを理解したい場合は、[ドキュメンテーション](https://ttnleipzig.github.io/regenfass-docs/).すぐに始めたい場合は、次の手順に従ってください。

### クイック - ハードウェアの概要

次の部品が必要です。

![Overview](_media/hardware/hardware-overview.png)

-   LoRa チップを搭載したマイクロコントローラ
-   センサー
-   電源
-   ハウジング

?> パーツについて詳しく知りたい場合は、[ハードウェアのドキュメント](#Hardware)。

### クイック - フラッシュ ソフトウェア

1.  ボードをコンピュータに接続し、
2.  次のボタンをクリックします。

<esp-web-install-button manifest="/static/firmware_build/manifest.json"></esp-web-install-button>

## ハードウェア

1.  Sensors
2.  電源
3.  ハウジング
4.  マイクロコントローラ
5.  アンテナ

### センサー

水位を測るにはセンサーが必要です。防水で水槽内で使用できるセンサーを見つけるのは簡単なことではありません。次のセンサーがサポートされており、推奨されています。
| |パート |説明 |
\| \| --- \| --- \|
\| \|![HC-SR04](_media/hardware/sensor-hcsr04.svg)｜[HC-SR04 超音波センサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)センサーは比較的安価で使いやすいです。防水ではありません。防水ケースに入れる必要があります。試してみたいだけなら、このセンサーをお勧めします。長期間の使用はお勧めできません。 | |  
｜![Laser distance sensor](_media/hardware/sensor-hcsr04.svg)｜[レーザーセンサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)センサーは比較的安価で使いやすいです。 HC-SRo4 と同様、防水ではありませんが精度が向上しています。防水ケースに入れる必要があります。試してみたいだけなら、このセンサーをお勧めします。長期間の使用はお勧めできません。 | |

#### 初心者

-   [HC-SR04 超音波センサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [レーザーセンサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

#### 高度

-   [水センサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)
-   [防水超音波センサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)

| 部                                                                 | 説明                                                                                                              |
| ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| <img src="_media/hardware/sensor-hcsr04.svg" width="244" />       | [HC-SR04 超音波センサー](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1) |
| <img src="_media/hardware/hardware-esplora.svg" width="244" />    | [放牧に向かう](https://www.amazon.de/gp/product/B07B4J8QZK/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)          |
| <img src="_media/hardware/hardware-18650.svg" width="144" />      | 18650 バッテリー                                                                                                     |
| <img src="_media/hardware/hardware-solarpanel.svg" width="244" /> | ソーラーパネル                                                                                                         |

### 部品

次の部分は推奨事項です。必要に応じて、他のパーツを使用できます。ただし、コードを変更する必要がある場合があります。以下の部品が推奨されます。

#### ロラワン

-   LoRaWAN ゲートウェイ

#### マイクロコントローラ

ソフトウェアを実行するにはボードが必要であることは明らかです。ただし、データを TTN に送信するには LoRa チップも必要です。次のボードがサポートされています。

-   [放牧に向かう](Hardware/TTGOLoRa32.md)
-   [ヘルテック LoRa32](Hardware/HeltecLoRa32.md)

### 回路図

![Schematic](https://raw.githubusercontent.com/Regenfass/Regenfass/master/Hardware/Schematic.png)

### 3Dプリント部品

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
