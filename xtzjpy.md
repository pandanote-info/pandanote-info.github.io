---
title: Web APIを使ってXTZ(Tezos)とJPYの参考レートを表示するPython3のプログラムを作ってみた。 - panda大学習帳外伝
description: XTZUSDを取得するAPIとUSDJPYを取得するWeb APIを使って計算で求めてます。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2021/03/P_20210225_190838_vHDR_On_HP-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sat Mar 13 13:19:40 2021 +0900
---
{% include pagelink.md %}
# Web APIを使ってXTZとJPYの参考レートを表示するPython3のプログラムを作ってみた。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
日本国内でTezosが購入(または売却)できる取引所は数えるほどしかない(※この記事を最初に書いた時点(2021年3月)の情報です。)上に、購入(または売却)時のスプレッドがかなり大きかったり、XTZの在庫がなかったりした場合に、提示される交換レートの最新の状況への追従が遅れる場合があるかもしれなそうな予感がします。

そこで、XTZUSDの交換レートとUSDJPYの交換レートを返してくれるWeb APIにアクセスして交換レートを取得後にそれらを使ってXTZJPYの参考レートを計算し、その結果を出力するPython3のプログラムを書いてみることにしました。

{% include firstad.html %}

## いきなりプログラム例
プログラム例は以下のような感じになります。

なお、以下のプログラム及びプログラムを実行した得られた結果については全くの無保証です。

<script src="https://gist-it.appspot.com/https://github.com/pandanote-info/xtzjpy/blob/main/xtzjpy.py"></script>

XTZUSD及びUSDJPYの値は以下のWeb APIにアクセスして取得しています。

* XTZUSD: TzStatsのWeb API(上記プログラムの30行目,下記参照)
<script src="https://gist-it.appspot.com/https://github.com/pandanote-info/xtzjpy/blob/main/xtzjpy.py?slice=29"></script>
* USDJPY: Foreign exchange rates API(上記プログラムの45行目,下記参照)
<script src="https://gist-it.appspot.com/https://github.com/pandanote-info/xtzjpy/blob/main/xtzjpy.py?slice=44"></script>

Foreign exchange rates APIの値は1日に1回しか更新されませんので、法定通貨間の為替レートに急激な変動にはすぐには追従できないかもしれません。

{%include secondintervalad.html %}

## 実行例
### 単純にレートを表示する。
引数をつけずに実行すると、XTZUSD、USDJPY及びXTZJPYの参考レートを表示します。
```
>python3 xtzjpy_sample.py
XTZUSD=3.920614,USDJPY=106.900565,XTZJPY=419.115868
```
### 評価額を表示する。
第1引数に-aオプションを、Tezosの量を第2引数にそれぞれ指定して実行すると、XTZ、USD及びJPYでの評価額を表示します。
```
>python3 xtzjpy_sample.py -a 10
XTZUSD=3.963506,USDJPY=106.900565,XTZJPY=423.701061
Estimated amount of mine: 10.000000 XTZ, 39.635063 USD, 4237.010613 JPY
```
また、
```JSON
{ "amount":
  {"XTZ":314.15}
}
```
のようなJSONのファイルを用意して(仮にamount_sample.jsonというファイル名で保存したとします。)、xtzjpy_sample.pyの第1引数に-iオプションを、第2引数に上記JSONデータが書き込まれているファイル名を指定して実行すると…
```
>python3 xtzjpy_sample.py -i amount_sample.json
XTZUSD=3.983602,USDJPY=106.900565,XTZJPY=425.849299
Estimated amount of mine: 314.150000 XTZ, 1251.448547 USD, 133780.557214 JPY
```
のようにJSONファイルからTezosの量が読み込まれて、XTZ、USD及びJPYでの評価額が表示されます。

自分が保有してるTezosの量に対応する評価額を知ってニヤニヤしたいが、Tezosの量の入力をいちいち行うのが面倒な方向けのコマンドラインオプションです。

{%include thirdintervalad.html %}

## まとめ
「Tezosって何ですか?」という方や暗号資産にはまったく興味がないという方でもPython3を使ってAPIにアクセスするためのプログラムとしては参考になるかもしれませんので、何かの際に思い出していただけると幸いです。

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
