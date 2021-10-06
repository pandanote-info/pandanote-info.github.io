---
title: if文を使わないで旬を求める。 - panda大学習帳外伝
description: 
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2021/10/P_20211001_072058b.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Thu Oct  7 07:49:25 2021 +0900
---
{% include pagelink.md %}
# if文を使わないで旬を求める。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
2021年は「令和三年東京オリンピック競技大会・東京パラリンピック競技大会特別措置法」の第32条の規定により祝日が変更されました。

しかし、この法律案が成立したのが一般的な2021年のカレンダーが販売開始された後(2020年11月27日)であったため…

<blockquote class="instagram-media" data-instgrm-captioned data-instgrm-permalink="https://www.instagram.com/p/CUeH9Y2pPRS/?utm_source=ig_embed&amp;utm_campaign=loading" data-instgrm-version="14" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:540px; min-width:326px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:16px;"> <a href="https://www.instagram.com/p/CUeH9Y2pPRS/?utm_source=ig_embed&amp;utm_campaign=loading" style=" background:#FFFFFF; line-height:0; padding:0 0; text-align:center; text-decoration:none; width:100%;" target="_blank"> <div style=" display: flex; flex-direction: row; align-items: center;"> <div style="background-color: #F4F4F4; border-radius: 50%; flex-grow: 0; height: 40px; margin-right: 14px; width: 40px;"></div> <div style="display: flex; flex-direction: column; flex-grow: 1; justify-content: center;"> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; margin-bottom: 6px; width: 100px;"></div> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; width: 60px;"></div></div></div><div style="padding: 19% 0;"></div> <div style="display:block; height:50px; margin:0 auto 12px; width:50px;"><svg width="50px" height="50px" viewBox="0 0 60 60" version="1.1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink"><g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd"><g transform="translate(-511.000000, -20.000000)" fill="#000000"><g><path d="M556.869,30.41 C554.814,30.41 553.148,32.076 553.148,34.131 C553.148,36.186 554.814,37.852 556.869,37.852 C558.924,37.852 560.59,36.186 560.59,34.131 C560.59,32.076 558.924,30.41 556.869,30.41 M541,60.657 C535.114,60.657 530.342,55.887 530.342,50 C530.342,44.114 535.114,39.342 541,39.342 C546.887,39.342 551.658,44.114 551.658,50 C551.658,55.887 546.887,60.657 541,60.657 M541,33.886 C532.1,33.886 524.886,41.1 524.886,50 C524.886,58.899 532.1,66.113 541,66.113 C549.9,66.113 557.115,58.899 557.115,50 C557.115,41.1 549.9,33.886 541,33.886 M565.378,62.101 C565.244,65.022 564.756,66.606 564.346,67.663 C563.803,69.06 563.154,70.057 562.106,71.106 C561.058,72.155 560.06,72.803 558.662,73.347 C557.607,73.757 556.021,74.244 553.102,74.378 C549.944,74.521 548.997,74.552 541,74.552 C533.003,74.552 532.056,74.521 528.898,74.378 C525.979,74.244 524.393,73.757 523.338,73.347 C521.94,72.803 520.942,72.155 519.894,71.106 C518.846,70.057 518.197,69.06 517.654,67.663 C517.244,66.606 516.755,65.022 516.623,62.101 C516.479,58.943 516.448,57.996 516.448,50 C516.448,42.003 516.479,41.056 516.623,37.899 C516.755,34.978 517.244,33.391 517.654,32.338 C518.197,30.938 518.846,29.942 519.894,28.894 C520.942,27.846 521.94,27.196 523.338,26.654 C524.393,26.244 525.979,25.756 528.898,25.623 C532.057,25.479 533.004,25.448 541,25.448 C548.997,25.448 549.943,25.479 553.102,25.623 C556.021,25.756 557.607,26.244 558.662,26.654 C560.06,27.196 561.058,27.846 562.106,28.894 C563.154,29.942 563.803,30.938 564.346,32.338 C564.756,33.391 565.244,34.978 565.378,37.899 C565.522,41.056 565.552,42.003 565.552,50 C565.552,57.996 565.522,58.943 565.378,62.101 M570.82,37.631 C570.674,34.438 570.167,32.258 569.425,30.349 C568.659,28.377 567.633,26.702 565.965,25.035 C564.297,23.368 562.623,22.342 560.652,21.575 C558.743,20.834 556.562,20.326 553.369,20.18 C550.169,20.033 549.148,20 541,20 C532.853,20 531.831,20.033 528.631,20.18 C525.438,20.326 523.257,20.834 521.349,21.575 C519.376,22.342 517.703,23.368 516.035,25.035 C514.368,26.702 513.342,28.377 512.574,30.349 C511.834,32.258 511.326,34.438 511.181,37.631 C511.035,40.831 511,41.851 511,50 C511,58.147 511.035,59.17 511.181,62.369 C511.326,65.562 511.834,67.743 512.574,69.651 C513.342,71.625 514.368,73.296 516.035,74.965 C517.703,76.634 519.376,77.658 521.349,78.425 C523.257,79.167 525.438,79.673 528.631,79.82 C531.831,79.965 532.853,80.001 541,80.001 C549.148,80.001 550.169,79.965 553.369,79.82 C556.562,79.673 558.743,79.167 560.652,78.425 C562.623,77.658 564.297,76.634 565.965,74.965 C567.633,73.296 568.659,71.625 569.425,69.651 C570.167,67.743 570.674,65.562 570.82,62.369 C570.966,59.17 571,58.147 571,50 C571,41.851 570.966,40.831 570.82,37.631"></path></g></g></g></svg></div><div style="padding-top: 8px;"> <div style=" color:#3897f0; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:550; line-height:18px;">View this post on Instagram</div></div><div style="padding: 12.5% 0;"></div> <div style="display: flex; flex-direction: row; margin-bottom: 14px; align-items: center;"><div> <div style="background-color: #F4F4F4; border-radius: 50%; height: 12.5px; width: 12.5px; transform: translateX(0px) translateY(7px);"></div> <div style="background-color: #F4F4F4; height: 12.5px; transform: rotate(-45deg) translateX(3px) translateY(1px); width: 12.5px; flex-grow: 0; margin-right: 14px; margin-left: 2px;"></div> <div style="background-color: #F4F4F4; border-radius: 50%; height: 12.5px; width: 12.5px; transform: translateX(9px) translateY(-18px);"></div></div><div style="margin-left: 8px;"> <div style=" background-color: #F4F4F4; border-radius: 50%; flex-grow: 0; height: 20px; width: 20px;"></div> <div style=" width: 0; height: 0; border-top: 2px solid transparent; border-left: 6px solid #f4f4f4; border-bottom: 2px solid transparent; transform: translateX(16px) translateY(-4px) rotate(30deg)"></div></div><div style="margin-left: auto;"> <div style=" width: 0px; border-top: 8px solid #F4F4F4; border-right: 8px solid transparent; transform: translateY(16px);"></div> <div style=" background-color: #F4F4F4; flex-grow: 0; height: 12px; width: 16px; transform: translateY(-4px);"></div> <div style=" width: 0; height: 0; border-top: 8px solid #F4F4F4; border-left: 8px solid transparent; transform: translateY(-4px) translateX(8px);"></div></div></div> <div style="display: flex; flex-direction: column; flex-grow: 1; justify-content: center; margin-bottom: 24px;"> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; margin-bottom: 6px; width: 224px;"></div> <div style=" background-color: #F4F4F4; border-radius: 4px; flex-grow: 0; height: 14px; width: 144px;"></div></div></a><p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;"><a href="https://www.instagram.com/p/CUeH9Y2pPRS/?utm_source=ig_embed&amp;utm_campaign=loading" style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none;" target="_blank">pandanote.info(@pandanote_info)がシェアした投稿</a></p></div></blockquote> <script async src="//www.instagram.com/embed.js"></script>

のような、通常の年であれば何の変哲も問題もない(はずの)カレンダーの写真でも…

<a href="https://pandanote.info/?attachment_id=7987"><img src="https://pandanote.info/wordpress/wp-content/uploads/2021/10/P_20211001_072058b.jpg"></a>

というような注意喚起が必要になったりします。

ところで、月を上旬、中旬または下旬に3分割する場合、

人間なら例えば、

「15日は上旬、中旬、下旬のうちどの旬に属しますか?」

という質問に比較的瞬時に「中旬である。」答えることができます。

しかし、コンピュータに上記の問題を解かせるにはどのようにしたら良いでしょうか?

if文を使う手もなくはないですが、人間は上記の質問の答えを考えるにあたって、if文またはif文的なものを思い浮かべつつ考えるということはなさそうですので、もう少し賢く解く手がありそうです。

そこで、この記事では日付からif文を使わずに対応する旬を求める方法を考えることにします。

{% include firstad.html %}

## やりたいこと
そんなわけで、日付からif文を使わずに対応する旬を求めるために、

* 1以上10以下の整数には0を、
* 11以上20以下の整数には1を、
* 21以上31以下の整数には2を、

それぞれ出力として与える関数$f(x)$が作れないか考えてみます。

{%include secondintervalad.html %}

## 関数を作ります。
なんとなく適当な実数$a$を考え、$f(x)=\displaystyle\frac{x}{a}$と(とりあえず)置いてみます。

前節の条件を満たすためには、

\begin{align}
10/a&\lt 1, 11/a \ge 1 \label{eq:conditionone} \cr
20/a&\lt 2, 21/a \ge 2 \label{eq:conditiontwo} \cr
31/a&\lt 3  \label{eq:conditionthree}
\end{align}

が成り立てば良さそうです。

条件式(\ref{eq:conditionone})から条件式(\ref{eq:conditionthree})に向かうに連れて条件が厳しくなり、$a$の取りうる値の範囲を少しずつ狭くしてくれます。

上記の条件をすべて満たす$a$の範囲は

\begin{align}
31/3 &\lt a \le 21/2 \label{eq:solution}
\end{align}

になりますので、例えば $a = \displaystyle\frac{27}{5} (=10.4)$とおいて

\begin{align}
f(x) &= \left\lfloor \displaystyle\frac{5}{27}x \right\rfloor \label{eq:function}
\end{align}

という関数を考えると、$1 \le x \le 31$の範囲の整数$x$について$f(x)$が所望の値を出力してくれそうです。

試してみます。

## 何それおいしいの?
if文を使わないと何がありがたいのかというと、SQL文にそのまま入れることができたりします。

特に「SQL文を使いたいけど、種々の理由によりストアドプロシージャは作りたくない or あまり増やしたくない。」という場面で威力を発揮しそうです。
## 動作確認。
### データの準備
まず、以下のようなSQL文(今回のテストにはSQLite3を使用しています。)でテスト用の日付を格納するテーブルを作ります。

```
sqlite> create table decade_test ( day integer );
```

次に、上記のテーブルにテスト用の日付をinsertします。

```
sqlite> insert into decade_test(day) values(1),(2),(3),(4),(5),(6),(7),(8),(9),(10),(11),(12),(13),(14),(15),(16),(17),(18),(19),(20),(21),(22),(23),(24),(25),(26),(27),(28),(29),(30),(31);
```
### ケース1
$a = 10.4$の場合です。上旬は0、中旬は1、下旬は2と正しく分類できていることが確認できます。
```
sqlite> select day,cast(day/10.4 as int) from decade_test;
1|0
2|0
3|0
4|0
5|0
6|0
7|0
8|0
9|0
10|0
11|1
12|1
13|1
14|1
15|1
16|1
17|1
18|1
19|1
20|1
21|2
22|2
23|2
24|2
25|2
26|2
27|2
28|2
29|2
30|2
31|2
```
### ケース2
$a = 10.5$の場合です。このケースでも上旬は0、中旬は1、下旬は2と正しく分類できていることが確認できます。
```
sqlite> select day,cast(day/10.5 as int) from decade_test;
1|0
2|0
3|0
4|0
5|0
6|0
7|0
8|0
9|0
10|0
11|1
12|1
13|1
14|1
15|1
16|1
17|1
18|1
19|1
20|1
21|2
22|2
23|2
24|2
25|2
26|2
27|2
28|2
29|2
30|2
31|2
```
### ケース3
$a = 10.2$の場合です。このケースは$a$の値が(\ref{eq:solution})式の範囲外になりますが、31日の分類に失敗していることがわかります。
```
sqlite> select day,cast(day/10.2 as int) from decade_test;
1|0
2|0
3|0
4|0
5|0
6|0
7|0
8|0
9|0
10|0
11|1
12|1
13|1
14|1
15|1
16|1
17|1
18|1
19|1
20|1
21|2
22|2
23|2
24|2
25|2
26|2
27|2
28|2
29|2
30|2
31|3
```

{%include thirdintervalad.html %}

## まとめ
「Numerical Recipes in C」に3月1日からの経過日数(2月末日までは前の年の3月1日からの経過日数)を入力として、対応する月を出力するようなプログラムの例が掲載されています。

この記事の例よりも複雑な例((\ref{eq:conditionone})式から(\ref{eq:conditionthree})式に相当する部分の式の数が増えます。)になりますが、この部分の解説が一切ないのでなんでそうなるのかはあまり検討されないままコーディングされて使われている予感がします…

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
