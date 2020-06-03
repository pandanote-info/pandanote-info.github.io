---
title: Windows10のEmacsのフォントをHackGenNerdに変更してみた(おまけつき)。 - panda大学習帳外伝
description: Windows10のEmacsのフォントをHackGenNerdに変更する方法です。
image: https://pandanote.info/wordpress/wp-content/uploads/2020/06/ricty_from_scratch_scene6.png
twitter:
  card: summary_large_image
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}
# Windows10のEmacsのフォントをHackGenNerdに変更してみた。
## ちょっと長めの前置き
WindowsにEmacsをインストールすると、おそらく…

<a href="https://pandanote.info/?attachment_id=6331"><img src="https://pandanote.info/wordpress/wp-content/uploads/2020/06/ricty_from_scratch_scene4.png"/></a>

のようにデフォルトのフォントとしてCourier Newが使われ、(上図には登場しませんが、)日本語のフォントはビットマップフォント的な感じのフォントが使われるのではないかと思います。

Windows版のEmacsは特に日本語関連の動作において仕様なのかバグなのかいまいちわかりにくい挙動を示すことがあり、とてもフォントの見てくれまでは手が回らないところではあります。

{% include firstad.html %}

ただ、文字はきれいに表示された方がなにかとやる気が出るような気がしてきたので、まず、Diminishedじゃない方のRictyフォントを作成後、インストールして設定を行ってみたのですが…

<a href="https://pandanote.info/?attachment_id=6332"><img src="https://pandanote.info/wordpress/wp-content/uploads/2020/06/ricty_from_scratch_scene5.png"/></a>

なんか日本語の表示が怪しい感じがします。

拡大してみると…

<a href="https://pandanote.info/?attachment_id=6333"><img src="https://pandanote.info/wordpress/wp-content/uploads/2020/06/ricty_from_scratch_scene5a.png"/></a>

日本語の文字がソーシャルディスタンスを保っているようにも見えます。なお、この現象はWindows10のEmacsでのみ発生し、Fedora32のEmacsでは発生しません。

{%include secondintervalad.html %}

日本語の文字についてはソーシャルディスタンスは不要だと思いますので、(正常に表示されることがわかっている)Ricty Diminishedフォントを使う選択肢もありますが…

ここは、「前進あるのみ!!」であります。&#x1f43c;

新しいフォントはないものかと適当にググってみたところ、「HakuGenフォント」なるものを発見したので、そのフォントの中でも(本記事を最初に書いた2020年6月時点では)最新のHakuGenNerdフォントを使ってみることにしました。

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">Windows10の <a href="https://twitter.com/hashtag/Emacs?src=hash&amp;ref_src=twsrc%5Etfw">#Emacs</a> で使用している日本語フォントをDiminishedじゃない方の <a href="https://twitter.com/hashtag/ricty?src=hash&amp;ref_src=twsrc%5Etfw">#ricty</a> にするべく設定したところ、<br><br>ど う し て こ う な っ た<br><br>的な感じの表示(1枚目)になったので、ついかっとなって<a href="https://twitter.com/hashtag/HackGenNerd?src=hash&amp;ref_src=twsrc%5Etfw">#HackGenNerd</a> をインストールしてみた。<br>作業効率が上がりそうです。😎<a href="https://twitter.com/hashtag/lifeinyokohama?src=hash&amp;ref_src=twsrc%5Etfw">#lifeinyokohama</a> <a href="https://t.co/jPNYw5tfjk">pic.twitter.com/jPNYw5tfjk</a></p>&mdash; pandanote.info (@Pandanote_info) <a href="https://twitter.com/Pandanote_info/status/1267967011482529792?ref_src=twsrc%5Etfw">June 2, 2020</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## HackGenNerdフォントのセットアップ
### インストール
HackGenNerdフォントのWindows10へのインストールは他のフォントのWindows10へのインストールの方法と同様ですので、本記事では割愛します。

なお、Windows10へのフォントのインストールに成功した時点で、Emacsから使用することができます。
### インストールの状況の確認
インストールの状況の確認は、以下の手順で行うことができます。
1. Emacsを起動して、メニューバーから「Options」を選択します。
1. 表示されたメニューから「Set Default Font」を選択します。
1. 下図のような「フォント」ポップアップが表示されます。
1. 上部の検索窓に"Hack"くらいまで入力した時点で"HackGenNerd"が表示されていれば、EmacsからHackGenNerdが使用できる状態になっていることが確認できます。
<a href="https://pandanote.info/?attachment_id=6334"><img src="https://pandanote.info/wordpress/wp-content/uploads/2020/06/ricty_from_scratch_scene7.png"/></a>
### init.elへの設定例
インストールの状況が確認できたら、init.el(またはそれに相当する設定ファイル)に以下の例のように記述を追加して保存します。

<script src="https://gist.github.com/pandanote-info/7a0c4a7380083a683d7a4538f03e95d1.js"></script>

なお、上記の設定よりもっと良い設定があるかもしれません。

{%include thirdintervalad.html %}

### 表示例
前節の設定を行ってからEmacsを再起動する等の方法によって保存したinit.elを読み込ませると、以下のように表示することができます。

<a href="https://pandanote.info/?attachment_id=6335"><img src="https://pandanote.info/wordpress/wp-content/uploads/2020/06/ricty_from_scratch_scene6.png"/></a>

ソーシャルディスタンスが削除されていますね。
## (おまけ)今回利用を試みたDiminishedじゃない方のRictyフォントの生成に使用した材料
Diminishedじゃない方のRictyフォントのVersion 4.0.0以降のものはライセンスの関係で直接配布することができないため、今回Diminishedじゃない方のRictyフォントを作成するにあたり使用したフォントのファイル等を以下に示します。
1. Inconsolata.zip (Google Fonts Inconsolataのページからダウンロードできるやつ)
1. migu-1m-20200307.zip
## まとめ
この記事はここまでに記述した方法によってHackGenNerdフォントを使用するように設定したEmacsで書いていますが、Courier New(+ビットマップ日本語フォント)と比較すると、見やすさが段違いですね。

正直なところ、Ricty Diminishedとの比較という点では甲乙つけ難く、好みの問題というレベルな感じもしますが、Ricty Diminishedは前述のライセンスの関係で今後更新されない可能性が高いため、新しいフォントをお手軽にインストール及びセットアップしてEmacsで(日本語に限らず)文字をきれいに表示させたい場合にはHackGenフォント(及びそのファミリー)はかなりおすすめです。

また、古来Emacsで日本語が乱れずに表示できるフォントの種類は極めて限られていましたので、フォントの選択肢が増えることは良いことであると思います。

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
