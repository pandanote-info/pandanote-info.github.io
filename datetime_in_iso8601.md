---
title: Python3で現在のローカル時刻をISO8601フォーマットで表示させるプログラムのメモ。 - panda大学習帳外伝
description: 時々使おうとして思い出せないことがあるので、メモすることにしました。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2022/08/datetime_scene1.png
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sun Aug 28 22:47:36 2022 +0900
---
{% include pagelink.md %}
# Python3で現在のローカル時刻をISO8601フォーマットで表示させるプログラムのメモ。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
[この記事](https://vsse.pandanote.info/xtzyieldcalc.html)といいますか、グラフ生成用のプログラムの機能強化をした際に、現在のローカル時刻を取得する必要が生じたのですが、なんか時刻を取得するためのコードって毎度Google先生に質問しているような気がしてきました。

そこで、現在のローカル時刻を取得するためのコードをまとめることにしました。

{% include firstad.html %}
## Python3のコード例
### その1
Python3で時刻を扱うためにはdatetimeモジュールを使い、以下のように記述します。

<script src="https://gist.github.com/pandanote-info/455e8185f2574f028aab62919b613a09.js"></script>

上記のプログラムを実行すると、以下の結果が得られます。

```
C:\Users\pandanote\Documents\sandbox>python datetime_in_isoformat_part1.py
2022-08-28T20:32:26.074491+09:00
```

{%include secondintervalad.html %}

### その2
その1のプログラムだと"datetime.datetime"のように書くのが冗長に感じられるかもしれません。

そこで、モジュール名のdatetimeの記載を省略すべく、以下のように記述します。

<script src="https://gist.github.com/pandanote-info/8476402230fcebbe9cd85cb5dbb3117b.js"></script>

上記のプログラムを実行すると、以下の結果が得られます。

```
C:\Users\pandanote\Documents\sandbox>python datetime_in_isoformat_part2.py
2022-08-28T20:40:00.198453+09:00
```

{%include thirdintervalad.html %}

## おまけ: Emacs Lispのコード例
Emacs Lispで現在のローカル時刻を取得してISO8601フォーマットで表示するには、以下のように記述します。

```
(concat (format-time-string "%Y-%m-%dT%H:%M:%S.%6N%z"))
```

%6Nのところを%Nとすると、ナノ秒単位で表示できるようです。

…が、手元の環境(Windows11上のEmacs 27.2)ではミリ秒以下は"000"と表示されたため、%6Nと設定することによって表示をミリ秒までに制限しています。

上記のコードをバッファに入力して評価すると…

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/08/datetime_scene1.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/08/datetime_scene1.png"/></a>

のようにミニバッファに出力されます。
## まとめ
Python3やEmacs Lispに限らず、現在のローカル時刻を表示させるコードが必要になるときに限って書き方を忘れてしまっていて、都度Google先生に質問していることが多いように感じるので、本Webサイトにキャッシュすることにしました。

何かの参考にしていただけると幸いです。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
