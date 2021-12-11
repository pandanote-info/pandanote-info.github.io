---
title: GitHub Gistにアップロードしたファイルの最新版でない版をWebのページに貼り付ける方法 - panda大学習帳外伝
description: Gistにアップロードしたファイルの特定の版に依存した記事を書く時に使えそうです。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2021/12/gist_older_code_scene1.png
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sat Dec 11 21:06:18 2021 +0900
---
{% include pagelink.md %}
# GitHub Gistにアップロードしたファイルの最新版でない版をWebのページに貼り付ける方法
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
GitHub Gistにアップロードしたファイルの内容をバージョン間で比較したくなった時などに使えそうな方法です。

{% include firstad.html %}
## 貼り付け方
以下の手順で貼り付けます。

1. GitHub Gistの貼り付けたいファイルのページへアクセスします。
1. Revisionsをクリックします。
1. Revision間の差分を表示する画面に切り替わりますので、貼り付けたいバーションの右上隅にある「…」アイコン(下図の赤矢印)をクリックし、「View file」をクリックします。<img width="515" src="https://pandanote.info/wordpress/wp-content/uploads/2021/12/gist_older_code_scene1.png"/>
1. ブラウザのアドレスバーに選択したリビジョンのURLが表示されます(下図の赤矢印)ので、左クリックで選択後にCtrl-Cを押すなどの方法でクリップボードにコピーします。<img width="505" src="https://pandanote.info/wordpress/wp-content/uploads/2021/12/gist_older_code_scene2.png"/>
1. Webページ中の貼り付けたい場所に以下のscriptタグを記述します。手順4でコピーしたURLの末尾に".js"を追加したものをsrc属性の値として指定します。
    ```
<script src="手順4でクリップボードにコピーしたURL+'.js'"></script>
    ```
1. 表示を確認します。

{%include secondintervalad.html %}

## 表示例
### 最新版の表示
[この記事](https://pandanote.info/?p=8226)では[このコード](https://gist.github.com/pandanote-info/81982c96f73b3954a2226c647d682a81)の最新版を貼り付けています…、と書いても記事中のどこにあるのかがわかりにくいと思いますので、↓に再掲します。

<script src="https://gist.github.com/pandanote-info/81982c96f73b3954a2226c647d682a81.js"></script>
### 一つ前の版の表示
一方で、[この記事](https://pandanote.info/?p=8205)では[このコード](https://gist.github.com/pandanote-info/81982c96f73b3954a2226c647d682a81)の最新版の一つ前の版を貼り付けています↓

<script src="https://gist.github.com/pandanote-info/81982c96f73b3954a2226c647d682a81/a5826f744e9da88addc9aef6288c819350e43b8a.js"></script>

最新版とは12行目が相違していることが確認できます。

{%include thirdintervalad.html %}

## まとめ
同じファイル(特にプログラム)の過去の版を振り返ることはあまり一般的ではないかもしれませんが、URLの末尾に何となく".js"を付けてみたところ表示できたので、使ってみることにしました。

Gistにアップロードしたファイル(またはプログラム)の特定の版に強く依存した記事を書く時に使えそうです。

この記事は以上です。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
