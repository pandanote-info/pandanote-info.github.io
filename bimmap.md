---
title: Bidirectional mapのプロトタイプをScalaだけで作ってみた。 - panda大学習帳外伝
description: みんな大好き双方向マップをScalaだけで作ってみました。
mathjax: true
image: https://cloudflare-ipfs.com/ipns/k51qzi5uqu5dgl9vqr7048dee9fnf1fhqq3zywm2rpq5ekh3kwegd22r2flijf/bimmap_scene1.png
twitter:
  card: summary_large_image
encoding: UTF-8
update: Sat Feb  5 23:15:31 2022 +0900
---
{% include pagelink.md %}
# Bidirectional mapのプロトタイプをScalaだけで作ってみた。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
やんごとなき作業のすきま作業(*1)でScalaでプログラムを書いていたのですが、

「bidirectional mapが必要かも。」

と思ったので書いてみたところ、当初の想定よりもシンプルに書けました。

{% include firstad.html %}
## 本編
### プログラム
プログラムはテストコードなど込みで、GitHubに置きました。
### ネーミング
BidirectionalなMapでMutableなMapを拡張して作ったものなので、パッケージ名及びクラス名は「BiMMap」としました。

そのまんまな感じのネーミングです。

{%include secondintervalad.html %}

## 作り方
BiMMapはクラスはscala.collection.mutable.Mapを拡張して作りますが、traitを拡張するので、インスタンスを別途定義する必要があります。

そこで、publicとするMapの子クラスとしてHelperクラス(BiMMap_クラス)を定義し、HelperクラスにMutableなMapのコンストラクタを引数として渡しています。

「Mapはtraitのはずなのになんでコンストラクタが実行できるのか?」というツッコミがあるかもしれませんが、Mapの親traitのコンパニオンオブジェクト(MapFactory)には子クラス(Delegate)がいて、そこにはapplyメソッドが待ち構えています。このメソッドがコンストラクタを実行すると起動されるようです。

{%include thirdintervalad.html %}

## 使用例
当面の間はテストコードをご参照ください。

## プログラミング後記
BiMMapは本来予定していたすきま作業(*1)では使用されない見込みです。

そうは言ってもコード的にはいい感じのものが作れたので、参照用としてGitHubに置くことにしました。

Scalaのソースコードを紐解いてみると、Map.scalaにAbstractMapなるクラスがいて、それを拡張するとGitHubに置いたコードと似たようなことができそうにも見えましたが、iteratorを定義するための実装のハードルが高かったため、AbstractMapクラスを拡張する方から攻めるアプローチは断念しました。

value側からのkeyの検索時にkeyとvalueを転置したMapを作っているため、データ量が多くなってくると処理コストがデータ量に比例して増えるかもなので、時々value側からの検索を行いたい時にしか役に立たないかもしれませんが、何かの機会のご参考にしていただけると幸いです。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
