---
title: GitHub GistにuploadしたPHPのget_class関数の使用例をGitHub Pagesに貼り付けてみた。 - panda大学習帳外伝
description: PHPのget_class関数の使用方法を確認するための簡単なコードをGitHub Gistにuploadし、さらにそれをこのページに貼ってみました。
image: https://pandanote.info/wordpress/wp-content/uploads/2020/03/P_20200328_093048_vHDR_On_HP.jpg
twitter:
  card: summary_large_image
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}
# GitHub GistにuploadしたPHPのget_class関数の使用例をGitHub Pagesに貼り付けてみた。
## はじめに
親クラス$C_0$にメソッドを大量に実装し、それを拡張する子クラス$C_1 \cdots C_n$では必要最低限のメソッドを実装しておいて、それらのインスタンスに対する処理を行うところで、インスタンス名のクラス名が必要なPHPのプログラムを書くと、作業効率が上がりそうな局面がやってきました。

そこで、テスト用のプログラムを書いてみることにしました。

{% include firstad.html %}
## 書いた、貼った、動かした。
以下のようなプログラムを書いて、GitHub Gistに貼ってみました。
<script src="https://gist.github.com/pandanote-info/15cfcabe7ee7c0af95e31f1c60e56ad8.js"></script>
Hogeクラスが$C_0$に、HogeHogeクラスが$C_1$に相当します。get_class関数は$C_0$側に実装します。

{%include thirdintervalad.html %}
上記のプログラムをPHPのCLIに食わせてみます。上記のプログラムの15行目で"Hoge"が、17行目で"HogeHoge"がそれぞれ出力されれば正解ですが…
```
$ php getclassexample.php 
Hoge
HogeHoge
```
無事出力されました。&#x1F600;

{%include thirdintervalad.html %}
## まとめ
GitHub GistにアップロードしたコードをGitHub Pagesのページに貼り付けてみました。

本ページのコード例のような実装はRDBMSのテーブルとの間でデータを読み書きする際などに良く現れると思いますので、そのようなコードを書かねばならない局面に出くわした場合等にご参考にしていただけると幸いです。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
