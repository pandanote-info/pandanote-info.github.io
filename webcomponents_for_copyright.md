---
title: Web Componentsを使ってCopyright表示の年号を制御するカスタムHTML要素を作成する。 - panda大学習帳外伝
description: 年が変わってもCopyrightの年を追従させる方法について書いています。
mathjax: true
image: https://ipfs.io/ipns/k51qzi5uqu5dgl9vqr7048dee9fnf1fhqq3zywm2rpq5ekh3kwegd22r2flijf/copyright_webcomponents_scene1.png
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Fri Jan 13 11:51:19 2023 +0900
---
{% include pagelink.md %}
# WebComponentsを使ってCopyright表示の年号を制御するカスタムHTML要素を作成する。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
新年になった途端に気になるのが、Webサイト下部のCopyright表示の年号の更新作業です。

地味に面倒です。

更新対象となる箇所が1箇所とか2箇所のレベルであれば、直接その部分を編集ということでも何とかなるかもしれませんし、今までは実際にその方針で対応してきました。

しかし、1年に一度の作業ということで忘れがちな上に、<a href="https://vsse.pandanote.info/">このWebサイト</a>のように更新の対象となる箇所が徐々に増えてくるタイプのWebサイトを構築してしまったりすると、年を追うごとに工数が増えていくこと請け合いです。

そこで、この状況を打開すべく、Web Componentsを使ってCopyright表示の年号を制御するだけのカスタムHTML要素をやっつけで作ることにしました。

{% include firstad.html %}
## 簡単に仕様決め。
以下の仕様とします。

1. 要素名は pandanote-copyright とする。
2. 属性名は established とする。
   1. established属性が指定された場合の挙動は以下の通りとする。
	  1. 属性値としてページがアクセスされた年よりも前の年が指定された場合には "Copyright &lt;established属性で指定された年&gt;-&lt;ページがアクセスされた年&gt; by pandanote.info" と表示する。
	  2. 属性値としてページがアクセスされた年と同じ年が指定された場合には "Copyright &lt;established属性で指定された年&gt; by pandanote.info" と表示する。
	  3. この属性が指定された場合で、かつ属性値に前項または前々項以外の値(数字以外の文字列または空文字が指定された場合も含む。)が指定された場合には"Copyright 2020-&lt;ページがアクセスされた年&gt; by pandanote.info" と表示する。
   2. established属性が指定されていない場合には"Copyright 2020-&lt;ページがアクセスされた年&gt; by pandanote.info" と表示する。 

{%include secondintervalad.html %}

## Web Componentsのプログラム
Web Componentsのプログラムを以下のように書いて、Webサーバがアクセスできる場所に置きました。

<script src="https://gist.github.com/pandanote-info/75fcd3afa3cf2ed23f8833b682a0a10e.js"></script>

一般に簡単な処理を行うWeb ComponentsのプログラムではconntectedCallbackメソッドにカスタムHTML要素がドキュメントに追加されたときに行うべき処理を記述しますが、その方法だとestablished属性の属性値を取得することができなかったため、attributeChangedCallbackメソッドが呼び出されたときにestablished属性の属性値を取り出してCopyright表示に埋め込む処理を記述しています。

また、上記のコードの2-4行目でattributeChangedCallbackメソッドを呼び出す対象となる属性を記述しています。

なお、呼び出す対象となる属性が1種類であるため、attributeChangedCallbackメソッド内で属性名を確認する処理は省略しています。

上記のファイルをWebサーバがアクセスできる場所に置きます。

{%include secondintervalad.html %}

ここからは、本記事では上記のファイルを

```
https://vsse.pandanote.info/pandanotelink.js
```

に置いたものとして設定等を記述します。
## 設定例
### headタグ側の設定
まず、通常のJavaScriptファイルと同様の方法でHTMLのheadタグの内側にscriptタグを挿入します。

```
<head>
   <script src="https://vsse.pandanote.info/pandanotelink.js"></script>
</head>
```
### footerタグ側の設定
次に、footerタグの内側に以下のように記述します。

```
<footer>
   <pandanote-copyright established="2022"></pandanote-copyright>
</footer>
```
## 表示例
表示例です。

<a href="https://ipfs.io/ipns/k51qzi5uqu5dgl9vqr7048dee9fnf1fhqq3zywm2rpq5ekh3kwegd22r2flijf/copyright_webcomponents_scene1.png"><img width="540" src="https://ipfs.io/ipns/k51qzi5uqu5dgl9vqr7048dee9fnf1fhqq3zywm2rpq5ekh3kwegd22r2flijf/copyright_webcomponents_scene1.png"/></a>

## まとめ
やっつけで作成したこともあり、

* 要素名や属性名の命名センスがいまいちだったり、
* Copyrightのメッセージの文言がWebサイト間で異なる場合にはどう対応するのか、

とかいったようなちょっと気になる点はありますが、当面の間はこれで運用してみることにします。

これで年が変わってもHTMLファイルをこまめに編集することはなくなりそうです。

この記事は以上です。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
