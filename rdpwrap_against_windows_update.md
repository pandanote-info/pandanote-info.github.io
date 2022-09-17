---
title: Windows Updateの実行後にRDP Wrapper Libraryの設定ファイルをデスクトップからログインせずに最新版に更新し、かつその設定を反映させる方法。 - panda大学習帳外伝
description: Windows Updateは月に1回やってくるのですが、対処方法を忘れがちなので、メモしてみました。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2022/09/restoring_rdpwrap_through_ssh_scene3.png
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sat Sep 17 11:28:39 2022 +0900
---
{% include pagelink.md %}
# Windows Updateの実行後にRDP Wrapper Libraryの設定ファイルをデスクトップからログインせずに最新版に更新し、かつその設定を反映させる方法。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
[この記事](https://pandanote.info/?p=8228)などでご紹介していたdynabook(R732/37HK、以下単に「dynabook」と書きます。)はその後特にOSもWindows 10 Homeから変更されることもなく戸棚の奥にしまい込まれつつ、ファイルサーバ兼VirtualBoxのホストマシンとして運用しています。

さらに、RDP Wrapper Libraryをインストールしてリモートデスクトップのサーバとして使えるように設定しています。

しかし、毎月恒例のWindows Updateが実行されると、RDP Wrapper Libraryが参照しているDLLファイルが変更されてしまうことが多く、DLLファイルが変更された場合にはリモートデスクトップ機能が使えなくなります。

{% include thirdintervalad.html %}

その都度、戸棚の奥からdynabookを取り出してローカルのデスクトップからログインして設定の反映が必要ということになると、サーバとしての価値が激落ちくんです。

そこで、そのあたりを改善する方法を考えることにしました。

{% include firstad.html %}

## 前提条件
改善に必要な作業を行うにあたり、dynabook側に以下のソフトウェアが
インストール及び適切に設定され、正常に使用できる状態になっているものと仮定します。

1. RDP Wrapper Library
1. Git
1. OpenSSH

{%include secondintervalad.html %}

## 作業手順
以下の手順で作業します。

<ol>
<li>リモートデスクトップの設定を行うPC(本記事の例ではdynabookになります。)にsshを使ってログインします。</li>
<li>(初回のみ実行) 以下のコマンドを実行し、INI-RDPWRAPのリポジトリをローカルにcloneします。
```
panda@pandanote.info c:\Users\pandanote\work>git clone https://github.com/affinityv/INI-RDPWRAP
Cloning into 'INI-RDPWRAP'...
remote: Enumerating objects: 341, done.
remote: Counting objects: 100% (102/102), done.
remote: Compressing objects: 100% (45/45), done.
remote: Total 341 (delta 97), reused 61 (delta 57), pack-reused 239
Receiving objects: 100% (341/341), 1.33 MiB | 8.42 MiB/s, done.
Resolving deltas: 100% (241/241), done.
```
</li>
<li>(2回目以降実行) 手順1でcloneしたリポジトリのディレクトリ(INI-RDPWRAP)があるディレクトリ上で以下のコマンドを実行します。
```
panda@pandanote.info c:\Users\pandanote\work\INI-RDPWRAP>git pull
Already up to date.
```
</li>
<li>管理者の権限でコマンドプロンプトを起動します。</li>
<li>手順1または2でダウンロードまたは更新されたrdpwrap.iniをRDP Wrapper Libraryのインストール先(dynabookでは"c:\Program Files\RDP Wrapper"としています。)にコピー(既存のrdpwrap.iniがある場合はバックアップを取ってから上書き)します。</li>
<li>以下のコマンドを実行し、PowerShellを起動します。
```
panda@pandanote.info c:\Program Files\RDP Wrapper>powershell
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

新しいクロスプラットフォームの PowerShell をお試しください https://aka.ms/pscore6
```
</li>
<li>以下のコマンドを実行し、サービスを一旦停止させます。
```
panda@pandanote.info c:\Program Files\RDP Wrapper>net stop termservice
```
サービスの停止ができない場合には、システムを再起動します。
</li>
<li>以下のコマンドを実行してサービスを開始させ、設定の変更を反映させます。
```
panda@pandanote.info c:\Program Files\RDP Wrapper>net stop termservice
```
</li>
</ol>

{%include fifthintervalad.html %}

## 動作確認
動作確認は、リモートのPCからリモートデスクトップ接続を行うことにより確認できます。

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/09/restoring_rdpwrap_through_ssh_scene1.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/09/restoring_rdpwrap_through_ssh_scene1.png"/></a>

上図の画面が表示されたら「接続」ボタンをクリックします。

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/09/restoring_rdpwrap_through_ssh_scene2.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/09/restoring_rdpwrap_through_ssh_scene2.png"/></a>

上図のような警告画面が表示された場合には、念のため内容を確認した上で「はい」ボタンをクリックします。

すると…

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/09/restoring_rdpwrap_through_ssh_scene3.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/09/restoring_rdpwrap_through_ssh_scene3.png"/></a>

設定に成功していればログイン画面が表示されます。

お疲れさまでした。
## まとめ
RDP Wrapper Libraryを使い始めた当初はリモートデスクトップ機能が使えなくなる度にDLLファイルも置き換えたりしていたために手順が煩雑で、最終的には戸棚の奥からdynabookを取り出してデスクトップにログインしないと作業を完結させることができませんでした。

INI-RDPWRAPが整備されたおかげで、INIファイルの置き換えだけでリモートデスクトップ機能が使えるようになったので、かつSSH経由で作業を完結させることができるようになりました。

また、毎月1回のWindows Updateが行われるごとに戸棚の奥からdynabookを取り出す手間が省くことができるようにもなりました。

かなりいい感じです。

この記事は以上です。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
