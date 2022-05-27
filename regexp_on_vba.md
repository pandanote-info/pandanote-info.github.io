---
title: 正規表現を使って文字列を変換するプログラムをVBAで書いてみた。 - panda大学習帳外伝
description: 「すぐに取り出せる場所に置いておくと便利かもしれない正規表現」について書きました。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2022/05/P_20211231_094404-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Fri May 27 11:21:17 2022 +0900
---
{% include pagelink.md %}
# 正規表現を使って文字列を変換するプログラムをVBAで書いてみた。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
最近歳のせいかExcelを使うことが多くなりました。

Excelのシートに入力されている膨大なデータの中に規則性を見出すと正規表現を使いたくなることがありますが、正規表現を用いた処理はVBAで記述する必要があります。

また、そのような処理を記述するときに限って時間が潤沢に与えられることはまずないので、すぐに取り出せる場所に書いておく必要があります。

この記事ではそんな「すぐに取り出せる場所に置いておくと便利かもしれない処理」の例として、正規表現で文字列を変換する処理をVBAのプログラムとして記述する方法について書きます。

{% include firstad.html %}

## VBObjectを使った書き方
### 問題設定
問題設定としては、

```
京急1000形1890番台(Le Ciel)
```

のような文字列を…

```
Le Ciel 京急1000形1890番台
```

のように変換(カッコ内の文字列について、当該文字列を囲んている括弧を外しつつ、文字列の先頭に移動し、移動していない文字列の間は半角スペースで区切る。)ことを考えます。

{%include secondintervalad.html %}

### プログラム例
VBObjectのみを用いて正規表現の処理を行う場合には、VBAのプログラムは以下のような感じで記述します。

<script src="https://gist.github.com/pandanote-info/3816b4b043ebaadb2bd6f9353efee4da.js"></script>

記述できたら、試しに開発環境で実行してみます。

すると、イミディエイト画面に…

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/05/regexp_on_vba_scene1.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/05/regexp_on_vba_scene1.png"/></a>

のように「Le Ciel 京急1000形1890番台」と表示されることが確認できます(上図の赤矢印)。

{%include thirdintervalad.html %}

## アドインのすゝめ
前節の処理に限らず、VBAのプログラムを処理の対象となるデータが格納されているExcelのファイルに直接書き込むと、後でいろいろと気まずい思いをすることがあります。

そんなときには、正規表現等の処理を記述するためのExcelのアドインを作っておき、そこに思いついた処理を記述するようにしておくと~~苦痛に耐えられぬ時に~~いろいろと便利です。

{%include fourthintervalad.html %}

## まとめ
この記事では正規表現を特別な設定なしに使う方法としてVBObjectを使う方法に焦点を当てて書きました。

前節で書いたアドインにExcelのセルなどで右クリックすると表示されるポップアップメニューに対して新たなメニュー項目を追加するためのプログラムを追加すると、単純作業をより楽しくすることができたりしますが、そちらの方面の話題については時間と精神的な余裕ができたときに書くつもりです。

この記事は以上です。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
