---
title: Play Frameworkを使って作ったWebアプリケーションのプロジェクトをSubversionのリポジトリにimportしてみた。 - panda大学習帳外伝
description: Play Frameworkを使って作ったWebアプリケーションのプロジェクトをSubversionのリポジトリにimportしてみた。
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}

# Play Frameworkを使って作ったWebアプリケーションのプロジェクトをSubversionのリポジトリに収容してみた。
## はじめに
[Play Framework](https://amzn.to/2olnVQt)のチュートリアルをもとにしてリアルなWebアプリケーションを作ってみました。

Play FrameworkのアプリケーションはJavaでも書けますが、新しもの好きな本サイトの管理人たるpandaは[Scala](https://amzn.to/2olnVQt)で書いてみました。

ScalaはJavaに比べると簡潔な記述ができますが、それでもリアルなWebアプリケーションを作るとなるとコードやファイルの量が増えてきて、それらを収容するプロジェクト内部のディレクトリ構成も複雑になってきます。そこで、それらの修正履歴の管理を行うためにSubversionなどのリポジトリにプロジェクトごとインポートすることにしました。

リポジトリにインポートするときには必要なファイルだけをインポートするのが基本中の基本ですが、sbtコマンドを実行すると(それが"sbt clean"コマンドであったとしても、)得体の知れないファイルをいろいろな場所に作ってくれますので、それらのファイルやディレクトリを探し出して、インポートの対象から除外せねばなりません。

そこで、この記事でPlay Frameworkで作ったリアルなWebアプリケーションのプロジェクト(以下、単に「プロジェクト」と書きます。)をリポジトリにインポートする際に不要なファイルをリポジトリへのインポートの対象外とするための手順例について書きます。

なお、この記事ではSubversionのクライアントの使い方についての詳細な説明は省略します。
{% include firstad.html %}

## リポジトリに入れるべきでないディレクトリの削除。
sbtコマンドを実行すると以下のディレクトリが作成され、そのディレクトリの下に得体の知れないファイルが作成されます。

なお、logsはlogbackを使用していて、かつログファイルをlogsの下に出力するようにlogback.xmlにおいて設定している場合に限り作成される場合があるものです。
```
logs
project/project
project/target
target
```
また、ScalaのコードはEmacsのコードを使って書いていて、コード補完などのためにMetalsを使用しています(Metalsインストール時の顛末は[こちら](https://pandanote.info/?p=5265)参照。)ので、以下のディレクトリも作成されている場合があります。
```
.bloop
.metals
```
ここまでのディレクトリについてはSubversionリポジトリへのインポート前に削除します。
```
> rm -rf logs project/project project/target target .bloop .metals
```
EmacsでMetalsを使用している場合には、.metalsまたは.bloopという名前のディレクトリがいつの間にか作成されていることがありますので、
プロジェクトのルートディレクトリで以下のコマンドを実行して削除しておきます。

```
> find . \( -name .metals -a -name .bloop \) -a type d -prune -exec rm -rf '{}' \; 
```
## いよいよインポート。
不要と思われるディレクトリが削除できたら、Subversionのリポジトリにインポートします。
## svn:ignoreの設定。
Subverionのリポジトリにインポートができたら、リポジトリからプロジェクトをチェックアウトします。

その後、sbtコマンドを実行したり、Emacsでソースコード等を開いたりすると、削除したはずのディレクトリが次々と作成されますので、発見次第片っ端からignore listに登録します。
## まとめ
Subversionのリポジトリへのインポート前に不要と思われるファイルを削除するのはそれほど難しくない反面、svn:ignoreの設定は忘れがちで、かつ設定を忘れてしまったディレクトリやファイルをcommit時などに誤ってリポジトリに追加してしまいがちです。

しかし、それらのファイルやディレクトリを誤ってリポジトリに追加してしまうとインポート時に削除を行ってインポートの対象外とした意味がなくなってしまいますので、できるだけ早めにsvn:ignoreの設定を行っておくと良いと思います。

この記事は以上です。

{% include thirdintervalad.html %}

# リンク
[Play FrameworkやScalaやsbtのメモ書き。](https://sidestory.pandanote.info/play-scala-sbt.html) \| [panda大学習帳のScalaのカテゴリ](https://pandanote.info/?cat=17) \| {% include pagelink.md %}

{% include fourthintervalad.html %}
