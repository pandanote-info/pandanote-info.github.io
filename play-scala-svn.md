---
title: panda大学習帳外伝
description: Play Frameworkを使って作ったWebアプリケーションのプロジェクトをSubversionのリポジトリにimportしてみた。
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}

# Play Frameworkを使って作ったWebアプリケーションのプロジェクトをSubversionのリポジトリに収容してみた。
## はじめに

Play FrameworkのチュートリアルをもとにしてリアルなWebアプリケーションを作ってみました。

Play FrameworkのアプリケーションはJavaでも書けますが、Scalaで書いてみました。

ScalaはJavaに比べると簡潔な記述ができますが、それでもリアルなWebアプリケーションを作るとなるとコードやファイルの量が増えてきて、ディレクトリ構成も複雑になってきます。
そんなときに、リファクタリングを派手に失敗したとき等には簡単に元に戻したいので、リポジトリに入れたくなってきます。

リポジトリにインポートするときには必要なファイルだけをインポートするのが基本中の基本ですが、sbtを実行すると得体の知れない中間ファイルをいろいろな場所に作ってくれるので、それらのファイルはインポートの対象から除外せねばなりません。

そこで、この記事でPlay Frameworkで作ったリアルなWebアプリケーションのプロジェクトをリポジトリにインポートする際に不要な中間ファイルを排除するための手順例について書きます。

{% include firstad.html %}

## リポジトリに入れるべきでないディレクトリの削除。

```
.bloop
.metals
logs
project/.bloop
project/project
project/target
```
EmacsでMetalsを使用している場合には、.metalsまたは.bloopという名前のディレクトリがいつの間にか作成されていることがありますので、
プロジェクトのルートディレクトリで以下のコマンドを実行して削除しておきます。

```
find . -name 
```

## いよいよインポート。

## svn:ignoreの設定。

## まとめ

{% include thirdintervalad.html %}

# リンク
[panda大学習帳のScalaのカテゴリ](https://pandanote.info/?cat=17) \| {% include pagelink.md %}

{% include fourthintervalad.html %}
