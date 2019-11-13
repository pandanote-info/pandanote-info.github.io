---
title: Play FrameworkやScalaやsbtのメモ書き。 - panda大学習帳外伝
description: Play FrameworkやScalaやsbtのメモ書き。
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}

# Play FrameworkやScalaやsbtのメモ書き。

[Play Framework](https://amzn.to/2olnVQt)や[Scala](https://amzn.to/2olnVQt)や[sbt](https://amzn.to/2nG5WE9)については情報が少ないので、ハマったところから順番にまとめてみました。

なお、ある程度情報がまとまった部分については「[panda大学習帳](https://pandanote.info/)」に新規の記事を作った上で移転する可能性があります。

{% include firstad.html %}

## Play Framework

### バージョンについて
本節の記述はVersion 2.7を前提とした記述としています。

Version 2.6以降でAPIの仕様が比較的大幅に変更されているので、注意が必要です。
### 本編のメモ書き。

1. routesファイルに定義していないURLをcontrollersパッケージのコードから参照しようとすると、「controllers.routesにコントローラクラスは見つかりません。」というエラーメッセージが表示されて、コンパイルができない。よって、routesファイルへの設定が必要。
1. データベースに対するSQL文の発行はanormまたはSlickを使うと良い。ただ、Framework側ではSQL文のパラメータを置き換える程度の処理しかしないので、複雑なSQL文が必要になったとき(っていうか、そこそこ実用的なWebアプリケーションを作るときにはほぼ必要になります。)にはSlickだと厳しいかもしれないので、anormの方が無難かもです。
1. where ~ in 句のin句にパラメータを設定する際にはSeq型のデータを指定する。
1. Webアプリケーションの実行テストの際に「controllersパッケージのReverse&lt;コントローラのクラス名&gt;のvalueが見つからない」というエラーページが表示される場合にはroutesファイルへの設定が行われていないので、設定を確認する。
1. テンプレートでif文を書くときに、"@if"の後ろにはスペースを入れないこと。また、波括弧は省略しないこと。
1. エラーハンドラ以外のところでエラーを発生させ、かつ自前のエラーページを作成するとき等のためにステータスコードを取得するには、RequestHeaderクラスのstatusメソッドを実行すると取得できる。
1. MessagesRequestHandlerやMessageRequestはかなりの高確率でMessageRequestHandlerとかMessageRequestと書きがちですので、よくわからないエラーが発生したときには、最初に確認すべきところかも。
1. 実行環境でアプリケーションを終了させたときに、RUNNING_PIDという名前のファイルが消去されないときがある。このファイルが削除されずに残っているとアプリケーションが起動出来ないので、起動できないときにはRUNNING_PIDという名前のファイルがないかどうか確認し、あった場合には削除すること。

## Scala

1. コンパイルの際に生成される中間ファイルのパスの文字列が長くなり、Windowsのパスの文字列長の制限に引っかかることがあるので、身に覚えのないコンパイルエラーが発生した場合には、プロジェクトのファイルの置き場をドライブ直下に変えるか、いったんLinuxがインストールされているPCにプロジェクトをまるごとコピーした上でコンパイルを行うこと。
1. mainメソッドが引数としてとる変数argsはjarファイルの直後の引数が0番目である。
1. Scalaには三項演算子がない。ないだけならまだしも、エディタにおける文法チェック時に一見原因がわかりにくいコンパイルエラーを発生させることがあるので、以下のようなif文で書くことを習慣づけること(以下の例のようにコードブロックを示す波括弧は省略できる場合がある)。
```
val x = if (a > 0) 1 else -1
```
以下のような感じにも書くことができる。
```
println("x="+(if(y.equals("")){null}else{"'"+y+"'"}))
```
1. Listに直接要素を追加するとListを作り直してしまうため、巨大なListを扱うの場合にはパフォーマンスが低下する懸念がある(JavaにおけるStringオブジェクトと似た感じの問題)。そこで、Listに繰り返し要素を追加する処理を行う場合には、ListBufferとして以下のように定義すると良い。emptyメソッドにはListに格納するオブジェクトのクラス名を指定する。
```
val l = ListBuffer.empty[ExampleClass]
```
1. キーと値の組み合わせでデータを格納する場合に、キーの順序にソートしてデータを格納することが必要になることがある。そのような場合にはListMapを使用するとキーの順序にソートしてデータを格納することができる。
1. 英語の大文字小文字及び数字でランダムな文字列を作成するには以下のように記述すればよい(10文字の文字列を作成する場合)。以下の記述例では2行に分割しているが、(かなり横長にはなるものの)1行で書くこともできる。
```
val s = new scala.util.Random(new java.security.SecureRandom).
        alphanumeric.take(10).mkString
```
また、英語の大文字小文字のみでランダムな文字列を作成する場合にはちょっと工夫が必要で、以下のように記述する(10文字の文字列を作成する場合)。
```
val s = new scala.util.Random(new java.security.SecureRandom).
        alphanumeric.filterNot(c => c >= '0' && c <= '9').take(10).
        mkString
```
alphanumericメソッドはStreamインスタンスを返すが、StreamインスタンスでもfilterNotメソッドが利用可能であることに留意すること。
1. テキストファイルからの読み込みの際にはscala.io.Sourceクラスを使うと簡単に読めます。また、java.nio.file.Filesを使うとファイルへの書き出しを簡単に行うことができます。

{% include secondintervalad.html %}

## sbt

1. sbt-1.3.0-RC1でPlay Frameworkのプロジェクトをコンパイルするとviews.htmlが見つからないといわれる。なお、sbt-1.2.8及び1.3.3ではビルドできる。
1. sbt.bat自体はバッチプログラムなので、ビルド関連のコマンドを自動化する等の目的で別のバッチファイルからsbtを呼び出す場合には"call sbt &lt;command&gt;"のように記述すること。

## その他、または複合的なやつ。

1. DB Browser for SQLiteでデータの中身を確認しながらWebアプリケーションを実行していると、"SQLITE_BUSY"というエラーが発生することがある(データベースのデータをupdate文などで変更すると発生するようである)。そんなときには、DB Browser for SQLiteのメニューバーから「File」→「Close Database」と選択して変更を保存しつつデータベースの接続を終了すると、Webアプリケーション側のエラーが解消される。
1. セッションに保持されているデータは、sbtによるビルドを実行すると破棄されてしまうようなので、セッションのデータがなくても実行できる状態(例:ログイン前)からやり直すこと。
1. ScalaのプロジェクトのディレクトリをEmacsのミニバッファからタイプするのは少々面倒なので、Emacsの設定ファイル(init.el等)に以下の設定を追加する("your scala directory"の部分は適当に置き換えること。)と、F9キーを押すとneotreeのバッファが起動された際に設定したディレクトリを表示させることができるようになる。
```
(global-set-key [f9] 'open-scala-workspace)
(defun open-scala-workspace ()
  "Open scala workspace"
  (interactive)
  (neo-global--open-dir "your scala directory")
  (neo-global--select-window))
```
1. ネットに接続されていないPCにPlay frameworkの実行環境をインストールすると起動に時間がかかるかもしれないので、play.http.secret.keyはapplication.confなどの設定ファイルに設定すること。play.http.secret.keyキーに設定される文字列は適当な文字列で良いが、あまり長さの短いものを設定すると「キーの文字列長が短過ぎる。」と怒られるので、Linuxで以下のコマンドを実行するなどして長めのものを設定する。
```
$ head -c 32 /dev/urandom | base64
NUWoceVNSiwbPA1+PgY8GT0yGhEBk41oKP3dKedkQKI=
```

{% include thirdintervalad.html %}

# リンク
[Play Frameworkを使って作ったWebアプリケーションのプロジェクトをSubversionのリポジトリにimportしてみた。](https://sidestory.pandanote.info/play-scala-svn.html) \| [panda大学習帳のScalaのカテゴリ](https://pandanote.info/?cat=17) \| {% include pagelink.md %}

{% include fourthintervalad.html %}
