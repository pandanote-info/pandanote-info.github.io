---
title: VirtualBoxのゲストOSで稼働しているFedora35を効率良くFedora36にアップグレードしようとしたところ、ホストOSのWindows10/11が停止した話。 - panda大学習帳外伝
description: VirtualBoxのスナップショットは緊急事態発生時の復旧手段として割と使えるかもしれないというお話です。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2022/05/fedora36_upgrade_scene5.png
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sat May 14 16:12:06 2022 +0900
---
{% include pagelink.md %}
# VirtualBoxのゲストOSで稼働しているFedora35を効率良くFedora36にアップグレードしようとしたところ、ホストOSのWindows10/11が停止した話。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
今この記事を書いているHP Elite Dragonfly G2の購入前に使っていたdynabook R732/37HKはサーバ機として余生を送っていますが、Windows 10はまだ取っておいた方が良さそうだと思ったので、Windows10にVirtualBoxをインストールして、さらにゲストOSとしてFedora 35を複数インストールして使っています。

そして、現在この記事を書いているHP Elite Dragonfly G2にもWindows11にVirtualBoxをインストールして、ゲストOSとしてFedora 35を複数インストールして使っていました。

そして、このたびFedora 36がリリースされたとの情報を得たので、アップグレードを試みたのですが…

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr"><a href="https://twitter.com/hashtag/Windows?src=hash&amp;ref_src=twsrc%5Etfw">#Windows</a> 10/11がホストになっている <a href="https://twitter.com/hashtag/VirtualBox?src=hash&amp;ref_src=twsrc%5Etfw">#VirtualBox</a> の上で動いているFedora35のゲストOSを効率よく <a href="https://twitter.com/hashtag/Fedora36?src=hash&amp;ref_src=twsrc%5Etfw">#Fedora36</a> へアップグレードするつもりで、ゲストOSを2個起動してアップグレードを始めたところ、ホストのWindowsが停止するというミスを2度やらかしたので、ゲストOSが3個壊れたでござるがここで文字数</p>&mdash; pandanote.info (@Pandanote_info) <a href="https://twitter.com/Pandanote_info/status/1525295580733247488?ref_src=twsrc%5Etfw">May 14, 2022</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

という事態が発生しました。

壊れたゲストOSが三種三様な壊れ方をしたので、この記事ではそれらに対する対処の内容をつらつらと雑語りします。

なお、必ずしも前向きな対処策ばかりではない点については悪しからずご了承願います。

{% include firstad.html %}

## 対処内容
### 1個目: ゲストOSの起動には成功し、パッケージが途中までインストールされているが、それ以上のインストールができない。

OSの起動には成功するもの、dnf reinstall等のコマンドを駆使しても、

```
エラー:
 問題: 操作は結果的に以下の保護されたパッケージを削除します: NetworkManager, grub2-tools-minimal, systemd, systemd-udev
 (以下略)
```

と表示されて先に進めなくなってしまいました。

root権限で以下のコマンドを実行するとsystemdあたりまでは削除できないことはないのですが、systemd-udevを削除しようとしたところ、GNOMEが起動しなくなってしまいました。

このゲストOSはTezos(詳細は[こちら](https://pandanote.info/?p=7281)参照)の開発・構築環境の保管用のもので、VirtualBox上でスナップショットを取得していたため、最新の状態からの復旧は諦め、スナップショットから復旧後、再度Fedora 36へのアップグレードを行いました。

{%include secondintervalad.html %}

### 2個目: 仮想マシンの設定ファイル等が壊れてしまい、ゲストOSが「Oracle VM VirtualBox マネージャー」画面に表示されない。
今回壊れたゲストOSの中ではもっとも重要な役割を担っているものが起動しなくなってしまいました。

このゲストOSは次節のゲストOSのアップグレード作業を行う際に起動したままになっていたためにホストOSの停止時に巻き添えになる形で停止してしまったものです。

それで、ホストOSの電源をONにして再度VirtualBoxを起動してみると…

そもそも、ゲストOSが「Oracle VM VirtualBox マネージャー」画面に表示されません、また、起動ボタンも現れません。

そのかわりといってはなんですが、エラーメッセージが表示されます。

おまけにそのエラーの内容も「仮想ディスクが見つかりません。」的なエラーでして、これを見た時には…

「＼(^o^)／ｵﾜﾀ」

と思いました。

しかし、仮想ディスク(拡張子がvdiのファイル)の状況について調べてみると特になくなっていたりとか仮想ディスクのファイルサイズが0になっているとかということはなさそうだったので、仮想マシン用のVirtualBoxの設定ファイルまたはnvramファイルを作り直して、そこにもともと使っていた仮想マシンの仮想ディスクをアタッチすることにしました。

手順は新規に仮想マシンを作成する際と同様の手順ですが、以下の点には注意が必要です。

1. 「仮想マシン」の名前にはもとの仮想マシンとは異なるものを(仮に)指定します。
1. 「仮想マシンの作成」のウィンドウの「ハードディスク」のところでは「すでにある仮想ハードディスク」を選択し、プルダウンリストから今まで使っていた仮想ディスクを選択します。
<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/05/fedora36_upgrade_scene5.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/05/fedora36_upgrade_scene5.png"/></a>

上記の設定を行って新しい設定の仮想マシンを起動したところ、仮想マシンが正常に起動したため、仮想ディスク自体には問題がないことが確認できました。

そこで、以下の手順で復旧させました。

1. 新しい設定の仮想マシン用のディレクトリに仮想ディスクをコピーします。
1. 起動しなくなってしまった方の仮想マシン用のディレクトリをいったん別のディレクトリに退避します。
1. 新しい設定の仮想マシン用の設定ファイルのファイル名を変更したりするなどの方法で元の仮想マシン用の環境を(仮想ディスク以外の古い環境に係るファイルを使うことなく)復元します。
1. 復元した環境で正常に起動できることを確認します。 

その後、このゲストOSもFedora 36にアップグレードしました。

{%include thirdintervalad.html %}

### 3個目: ゲストOSが「Oracle VM VirtualBox マネージャー」画面に表示されるものの、ゲストOSの起動の途中で止まってしまう。

「Oracle VM VirtualBox マネージャー」画面の「起動」ボタンは押すことができて起動できるようには見えるものの、Fedoraの起動中に止まってしまいました。

このゲストOSは[この記事](https://pandanote.info/?p=8608)の説明用に作ったものでした。

そこで、Fedora 36のインストール用のISOイメージをダウンロードしてそこから起動してもとの仮想ディスクの中身に救出すべきファイルがないことを確認後、復旧を諦めて削除して仮想マシンごと削除しました。

{%include fifthintervalad.html %}

## まとめ
1,3個目のゲストOSでは壊れてしまったゲストOS復旧自体は諦めてしまいましたが、スナップショットを取っておいたおかげで1個目のゲストOSだけは被害を最小限に食い止めることができました。

今後ゲストOSのアップグレード作業を行う際には、以下の事項の確認は必須ですね。

1. アップグレード作業を行うゲストOSの他に動いているゲストOSがないかどうか確認し、あれば終了させる。
1. 事前にスナップショットのようなものを取得する。

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
