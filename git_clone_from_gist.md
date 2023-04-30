---
title: GitHub Gistにアップロードしたシェルスクリプトのファイルをgit cloneして使ってみた。 - panda大学習帳外伝
description: 今まで使っていなかったシェルスクリプトを実行してみました。
mathjax: true
image: 
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sun Apr 30 17:40:03 2023 +0900
---
{% include pagelink.md %}
# GitHub Gistにアップロードしたシェルスクリプトのファイルをgit cloneして使ってみた。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに

Fedora 38へのアップグレードを何とか完了させたところです。今回はあまり大きな問題なくアップグレードが実行できて良かったです。

さて、アップグレードの実行時に最近気になっているのが…

nginxが使用するディレクトリでownerがapacheやrootになっているものをnginxユーザに変更する手順の説明方法です。

実はFedora 37へのアップグレード作業までは以下のシェルスクリプトを直接使用することはせず、かわりにシェルスクリプト内に書いたコマンドを一個ずつシェルのプロンプトから入力して実行していました。

<script src="https://gist.github.com/pandanote-info/6d5abf29e0b21fcf12bfec25fea0831b.js"></script>

アップグレードの対象となるPCが1台であるうちはそれでも良かったのですが、Fedora 38へのアップグレードの作業開始の時点ではアップグレードの対象となるPCで、かつnginxを稼働させているものが3台と増えており、それなりに手間がかかります。

前置きが長くなりましたが、Fedora 38へのアップグレードからは上記のシェルスクリプトを直接使ってディレクトリのownerを変更することにしました。

{% include firstad.html %}

## シェルスクリプトを使ったownerの変更
### ダウンロード

GitHub Gistにアップロードしたシェルスクリプトは以下の手順でダウンロードします。

1. ファイル名(下図の赤矢印)をクリックする。
<a href="https://ipfs.io/ipns/pandanote.info/git_clone_from_gist_scene1a.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/git_clone_from_gist_scene1a.png"/></a>
1. ブラウザのアドレスバーのURLを確認する(下図の赤矢印)。
<a href="https://ipfs.io/ipns/pandanote.info/git_clone_from_gist_scene2a.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/git_clone_from_gist_scene2a.png"/></a>
1. シェルスクリプトを実行するPCにログインする。
1. 手順2で確認したURLのうち、"#"よりも前の文字列を使ってgit cloneコマンドを実行する。以下のコマンドを実行すると、最後のスラッシュ以降の文字列をディレクトリ名とするディレクトリが生成されて、ダウンロードされたファイルはその下のディレクトリに格納される。
```
$ git clone https://gist.github.com/pandanote-info/6d5abf29e0b21fcf12bfec25fea0831b
```
1. 以下のコマンドを実行して、シェルスクリプトがダウンロードされていることを確認する。
```
$ cd 6d5abf29e0b21fcf12bfec25fea0831b
$ ls -l
合計 4
-rw-r--r--. 1 panda panda 291  4月 29 17:57 adjust_config_sample.sh
```
### 実行

前節の手順に続けて、シェルのプロンプトで以下のコマンドを実行します。

```
$ sudo sh ./adjust_config_sample.sh
```

### ownerが変わったことの確認

前節の手順に続けて、シェルのプロンプトで以下のコマンドを実行します。

```
$ ls -l /var/lib/php
合計 0
drwxrwx---. 2 nginx apache  6  4月 12 09:00 opcache
drwxr-xr-x. 2 root  root   80  4月 29 18:22 peclxml
drwxrwx---. 2 nginx apache 96  4月 12 09:00 session
drwxrwx---. 2 nginx apache  6  4月 12 09:00 wsdlcache
```

シェルスクリプトの実行前はopcache, session, wsdlcacheの各ディレクトリのownerはapacheだったのですが、ownerがnginxに変更されていることが確認できます。

{%include secondintervalad.html %}

## おまけ: git cloneしたリポジトリにファイルを追加してみる。
git cloneしたリポジトリにファイル(README.txt)を追加してみます。

以下のコマンドを実行して追加します。
```
$ git add README.txt
$ git commit -m 'Append README.txt.'
[master 334244d] Append README.txt.
 1 file changed, 1 insertion(+)
 create mode 100644 README.txt
$ git push
(ユーザ名とパスワードを入力)
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 440 bytes | 440.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://gist.github.com/pandanote-info/6d5abf29e0b21fcf12bfec25fea0831b
   3f43df4..334244d  master -> master
```
リモート側のリポジトリがどのように変化しているか、確認してみます。

下図(再掲)の赤矢印をクリックしてみます。

<a href="https://ipfs.io/ipns/pandanote.info/git_clone_from_gist_scene1a.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/git_clone_from_gist_scene1a.png"/></a>

すると…

<a href="https://ipfs.io/ipns/pandanote.info/git_clone_from_gist_scene3a.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/git_clone_from_gist_scene3a.png"/></a>

追加したファイル(README.txt)も見ることができます。

しかし、追加したファイルも元からあったファイルの貼り付け先の記事から見えてしまうので、削除します。

```
$ git rm README.txt
$ git commit -m 'Remove README.txt.'
[master 801e675] Remove README.txt.
 1 file changed, 1 deletion(-)
 delete mode 100644 README.txt
$ git push
(ユーザ名とパスワードを入力)
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 257 bytes | 257.00 KiB/s, done.
Total 2 (delta 0), reused 1 (delta 0), pack-reused 0
To https://gist.github.com/pandanote-info/6d5abf29e0b21fcf12bfec25fea0831b
   334244d..801e675  master -> master
```

以上、おまけでした。

{%include thirdintervalad.html %}

## まとめ

ダウンロード後のディレクトリ名が固定でかつ16進表現のハッシュ値っぽい文字列になってしまう点が短所と言えば短所ですが、リポジトリをcloneすることができて、そのリポジトリにあるシェルスクリプトを実行することができました。

Fedora 39以降のFedoraのアップグレードではいい感じにスッキリと解説することができそうです。

この記事は以上です。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
