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

ScalaはJavaに比べると簡潔な記述ができますが、それでもリアルなWebアプリケーションを作るとなるとコードやファイルの量が増えてきて、ディレクトリ構成も複雑になってきますので、コーディングを派手に失敗したときの

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

## いよいよインポート。

## svn:ignoreの設定。

## まとめ

{% include thirdintervalad.html %}

# リンク
[panda大学習帳のScalaのカテゴリ](https://pandanote.info/?cat=17) \| {% include pagelink.md %}

{% include fourthintervalad.html %}
