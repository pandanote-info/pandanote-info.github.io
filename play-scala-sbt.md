---
title: panda大学習帳外伝
description: Play FrameworkやScalaやsbtのメモ書き。
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}

# Play FrameworkやScalaやsbtのメモ書き。

情報が少ないのでまとめてみました。

なお、ある程度情報がまとまった部分については「panda大学習帳」に新規の記事を作った上で移転する可能性があります。

{% include firstad.html %}

## Play Framework

1. routesファイルに定義していないURLをcontrollersパッケージのコードから参照しようとすると、「controllers.routesにコントローラクラスはみつかりません。」というエラーメッセージが表示されて、コンパイルができない。よって、routesファイルへの設定が必要。
1. データベースに対するSQL文の発行はanormを使うと良い。ただ、Framework側ではSQL文のパラメータを置き換える程度の処理しかしないので、複雑なSQL文が必要になったとき(っていうか、そこそこ実用的なWebアプリケーションを作るときにはほぼ必要になります。)には良いかもです。
1. where ~ in 句のin句にパラメータを設定する際にはSeq型のデータを指定する。
1. Webアプリケーションの実行テストの際に「controllersパッケージのReverse&lt;コンロローラのクラス名&gt;のvalueが見つからない」

## Scala

1. コンパイルの際に生成される中間ファイルのパスの文字列が長くなり、Windowsのパスの文字列長の制限に引っかかることがあるので、身に覚えのないコンパイルエラーが発生した場合には、プロジェクトのファイルの置き場をドライブ直下に変えるか、いったんLinuxがインストールされているPCにプロジェクトをまるごとコピーした上でコンパイルを行うこと。

## sbt

1. sbt-1.3.0-RC1でPlay Frameworkのプロジェクトをコンパイルするとviews.htmlが見つからないといわれる。なお、sbt-1.2.8ではビルドできる。

## その他、または複合的なやつ。

TBD.

{% include thirdintervalad.html %}

# リンク
[panda大学習帳のScalaのカテゴリ](https://pandanote.info/?cat=17) \| {% include pagelink.md %}

{% include fourthintervalad.html %}


