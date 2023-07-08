---
title: GIMPで文字の縁取りができないときに確認すべきこと1選 - panda大学習帳外伝
description: 解決までにかなり時間を要したので、メモっておくことにしました。
mathjax: true
image: https://ipfs.io/ipns/pandanote.info/border_with_gimp_scene3.png
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sun Jul  9 00:10:24 2023 +0900
---
{% include pagelink.md %}
# GIMPで文字の縁取りができないときに確認すべきこと1選
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
写真や動画で「ココ!!→」とか書きたいときには、単純に文字を追加しただけでは文字が写真や動画の背景に埋もれてしまって文字を見やすく追加できるということはありません。

文字を見やすくするための一般的な方法としては「文字列に縁取りを追加する。」という方法があり、動画ではAviUtlに文字を縁取りする機能があるため、それを使用しています。
一方、写真に文字を追加する方法として一番簡単な方法として思いつくのが「GIMPで文字列に縁取りを追加する方法」です。

この方法自体はぐぐると解説サイトがいくつかあり、基本的には解説サイトの記載の通りに操作すれば文字列に縁取りができます。

しかし、<a href="https://pandanote.info/?p=10741">この記事</a>を書くときになぜかこれが設定密に気づかずにハマってしまったので、確認すべきポイントをメモすることにしました。

{% include firstad.html %}

## 確認すべきこと1選
確認すべきことは以下の一点です。

選択範囲を拡大した後にレイヤーを追加するときに、「新しいレイヤー」のポップアップウィンドウの設定項目のうち、不透明度が「0.0」になっていないことを確認します。

<a href="https://ipfs.io/ipns/pandanote.info/border_with_gimp_scene1.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/border_with_gimp_scene1.png"/></a>

「縁取りを行う」ためには不透明度は「100.0」になっていることが望ましいですが、背景となる写真を活かしたいのであれば必ずしも「100.0」でなくても良いかもしれません。

ただ、「0.0」のままレイヤーを作成すると、「背景色での塗りつぶし」を行っても画像上には反映されません。

{%include secondintervalad.html %}

## 動作確認
「新しいレイヤー」のポップアップウィンドウにおいて、不透明度は「100.0」に変更してから「OK」ボタンを押して設定の変更を反映してから、動作を確認してみます。

<a href="https://ipfs.io/ipns/pandanote.info/border_with_gimp_scene2.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/border_with_gimp_scene2.png"/></a>

「新しいレイヤー」は縁取りをしたいレイヤーのすぐ下のレイヤーに移動しておきます。

GIMPのメニューバーから「編集」→「背景色で塗りつぶす」を選択すると…

<a href="https://ipfs.io/ipns/pandanote.info/border_with_gimp_scene3.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/border_with_gimp_scene3.png"/></a>

縁取りができました。

{%include thirdintervalad.html %}

## まとめ
操作法などをGoogle先生などにお伺いを立てつつ調べると、最近では一見うまくいきそうに見える方法を記載したページなどにたどり着くことが多く、それはそれで大変に助かります。

しかし、何らかの理由で前提条件が違っていたために、ページに記載の操作法の通りに操作したのに期待したような結果にならないという状況に遭遇し、解決に時間を要してしまったため、メモ書きを作成することにしました。

何らかの参考にしていただければ幸いです。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
