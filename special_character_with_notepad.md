---
title: Wordがなければメモ帳でも入力できる特殊文字 - panda大学習帳外伝
description: Twitter改めXのロゴっぽい文字をメモ帳上のUnicode変換を駆使して表示させる方法を書きました。
mathjax: true
image: https://ipfs.io/ipns/pandanote.info/QmSbHsZN3VEpgTgs4X53UD78sfoRN1TxFpbZAe3qY9Pw8R
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sat Jul 29 00:03:00 2023 +0900
---
{% include pagelink.md %}
# Wordがなければメモ帳でも入力できる特殊文字
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## 長めの前置き

2023年7月にTwitterが「X」にリブランドされることになったことは周知の事実かと思います。

その「X」のロゴがなんというか、その…

昔懐かしのX Window Systemのロゴに割とよく似ていたりするわけです。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">なお、参考画像。<br>xlogoって <a href="https://twitter.com/hashtag/Fedora38?src=hash&amp;ref_src=twsrc%5Etfw">#Fedora38</a> に単品でインストールできるんですね。<a href="https://twitter.com/hashtag/lifeinyokohama?src=hash&amp;ref_src=twsrc%5Etfw">#lifeinyokohama</a> <a href="https://t.co/TpTUxxqYC4">pic.twitter.com/TpTUxxqYC4</a></p>&mdash; pandanote.info (@Pandanote_info) <a href="https://twitter.com/Pandanote_info/status/1684940937808719872?ref_src=twsrc%5Etfw">July 28, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

さらに調べてみると…

Unicodeにもそこそこ似ている文字があるようです。

これはTwitter…じゃなかった、Ｘに投稿するときに是非ともこの文字を使いたくなります。

ところが、個人で使っているPC(HP DragonFly G2)にはこの記事を最初に書いた時点ではWordがインストールされていません。

いろいろと調べてみるとWordがインストールされていると特殊文字を変換する方法があるようですが、WordがインストールされていないのではWordを利用する方法を使うことはできません。

ここで、「Microsoft謹製のソフトウェアなら文字入力の変換方法って大体同じなんじゃね?」と考えたので、メモ帳を使ってUnicode変換を試みたところ特殊文字を得ることができましたので、この記事では変換の方法を書きます。

{% include firstad.html %}

## 入力の方法

前置きが長くなりすぎたので結論を先に書きますと、Windows11のメモ帳でのUnicode入力による変換の方法はWordにおけるそれとほぼ同じで、以下の手順となります。

1. メモ帳を起動します。
1. 編集画面に"U+..."と入力します。
<a href="https://ipfs.io/ipns/pandanote.info/special_character_with_notepad_scene1.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/special_character_with_notepad_scene1.png"/></a>
1. 入力した"U+..."の文字列をマウスでドラッグして選択状態にします。
<a href="https://ipfs.io/ipns/pandanote.info/special_character_with_notepad_scene2.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/special_character_with_notepad_scene2.png"/></a>
1. 選択状態としたまま、Alt+Xを押します。
1. メモ帳に変換結果が表示されます。
<a href="https://ipfs.io/ipns/pandanote.info/special_character_with_notepad_scene3.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/special_character_with_notepad_scene3.png"/></a>

{%include secondintervalad.html %}

## コピー&ペースト例

メモ帳に表示された&Xopf;をTwitter改めXの入力ウィンドウにコピーします。

すると…

<a href="https://ipfs.io/ipns/pandanote.info/special_character_with_notepad_scene4.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/special_character_with_notepad_scene4.png"/></a>

無事コピー&ペーストされました。

{%include thirdintervalad.html %}

## まとめ

HTMLだと数値文字参照で入力できる特殊文字ですが、Twitter改めX等のSNSでの投稿では入力に少し手間がかかります。

ただ、Wordがなくても入力できることがわかったので、今後はUnicode変換ライフを満喫できるのではないかと思います。(｀・ω・´)

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
