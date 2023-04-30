---
title: GitHub Gistにアップロードしたシェルスクリプトのファイルをgit cloneして使ってみた。 - panda大学習帳外伝
description: 
mathjax: true
image: 
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sun Apr 30 16:00:53 2023 +0900
---
{% include pagelink.md %}
# GitHub Gistにアップロードしたシェルスクリプトのファイルをgit cloneして使ってみた。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに

Fedora 38へのアップグレードを何とか完了させたところですが、アップグレードの実行時に最近気になっているのが…

nginxが使用するディレクトリでownerがapacheやrootになっているものをnginxユーザに変更する手順の説明方法です。

実はFedora 37へのアップグレード作業までは以下のシェルスクリプトを直接使用することはせず、かわりにシェルスクリプト内に書いたコマンドを一個ずつコマンドプロンプトから入力しながら実行していました。

<script src="https://gist.github.com/pandanote-info/6d5abf29e0b21fcf12bfec25fea0831b.js"></script>

アップグレードの対象となるPCが1台であるうちはそれでも良かったのですが、Fedora 38へのアップグレードの作業開始の時点ではアップグレードの対象となるPCが3台と増えており、それなりに手間がかかります。

そこで、今回のFedora 38へのアップグレードからは上記のシェルスクリプトを直接使ってディレクトリのownerを変更することにしました。

{% include firstad.html %}

## シェルスクリプトを使ったownerの変更
### ダウンロード

GitHub Gistにアップロードしたシェルスクリプトは以下の手順でダウンロードします。

1. 

### 実行

### ownerが変わったことの確認



{%include secondintervalad.html %}
## まとめ

ダウンロード後のディレクトリ名が固定でかつ16進表現のハッシュ値っぽい文字列になってしまう点が短所と言えば短所ですが、シェルスクリプトが利用できることが確認できました。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
