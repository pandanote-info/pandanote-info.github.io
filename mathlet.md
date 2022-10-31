---
title: Webブラウザ上でLaTeXの数式が編集できると捗る件。 - panda大学習帳外伝
description: MathJax3の助けを借りてWebブラウザ上でLaTeXの数式を編集するツールを作ってみました。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene1.png
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Mon Oct 31 23:40:01 2022 +0900
---
{% include pagelink.md %}
# Webブラウザ上でLaTeXの数式が編集できると捗る件。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
MathJax3の助けを借りてWebのページにちょっと込み入った数式を書いて表示しようとしたとします。

そのような時にいきなりすべての数式を書こうとしても、一度で意図した数式がビシッと書けるということは稀で、どこかしらで表記ミスやエラーが発生してしまいます。

そこで、表記ミスやエラーの原因を探り修正を行ってWebのページをリロードして表示をさせてみて、問題がないか確認することになりますが、ここで問題にしている表記ミスやエラーの発生箇所は数式の記載の範囲内で閉じているもののはずで、数式以外の部分を再表示するのはあまり意味のないことのように思えます。

…とここまでもっともらしい理屈を考えて書き並べてみたのですが、そのような理屈を考える以前に、作りかけの数式をWebページのリロードや$\LaTeX$のコマンドを使って出来具合を随時確認したいという極めて自然な人間の欲求にちょっとだけ応えるエディタがあっても良いのではないかと考えました。

「Webブラウザ上で $\LaTeX$ の数式の編集結果を随時確認できて、かつその結果がダウンロードできてしまう簡易エディタ」を作ることにしました。

{% include firstad.html %}

## mathlet
作ってみた結果出来上がった物は[こちら](https://vsse.pandanote.info/mathlet.html)(*)にあります(「[第三倉庫(仮)](https://vsse.pandanote.info/)」内)。

以下のような感じで表示できます。

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene1.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene1.png"/></a>

いい感じのものができたので名前をつけることとし、「mathlet」と命名しました。

leafletみたいなネーミングにしてみました。

mathletのページの領域は大きく以下の2つの領域に分類できます。

1. 編集領域
1. 表示領域

(*)のリンクをクリックすると、編集領域にガウス積分の $\LaTeX$ による記述がデフォルトの文字列として記述されているテキストエリアが、表示領域にはMathJax3による変換結果を黒板のようなものに書いたものがそれぞれ現れます。

{%include secondintervalad.html %}

### 編集領域
編集領域のテキストエリアには $\LaTeX$ による記述をそのまま記述することができます(具体的な記述法については $\LaTeX$ の解説本などをご参照願います)。

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene3.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene3.png"/></a>

上図の赤枠内のボタンについては「nonumber+cr」ボタンを除き、ボタンのラベルに記載の文字列を出力するための $\LaTeX$ のマクロ等をテキストエリアの文字列のカーソルの位置に追加することができます。

なお、「nonumber+cr」ボタンについては、「\nonumber\cr」をテキストエリアの文字列の位置に追加することができます。

さらに…

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene4.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene4.png"/></a>

上図の(a)のボタンを押すとガウス積分をテキストエリアの文字列のカーソルの位置に追加することができて、(b)のボタンを押すとボタンを押した時点でテキストエリアに入力されている文字列がダウンロードできます(拡張子は"tex"固定で、ファイル名も入力されている文字列を入力として生成されたSHA256によるハッシュ値(16進表現)で固定になります)。

また、(c)のボタンを押すとテキストエリアの文字列がクリアされます。
### 表示領域
表示領域には編集領域のテキストエリアの文字列に対する MathJax3による変換の結果が表示されます。

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene5.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene5.png"/></a>

上図の(a)の部分のうち、[+]ボタンを押すと表示領域に表示されている数式が拡大され、[-]ボタンを押すと表示領域に表示されている数式が縮小されます。

また、(b)のボタンを押すごとに…

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene6.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene6.png"/></a>

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene7.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene7.png"/></a>

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene8.png"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/10/mathlet_scene8.png"/></a>

のように、背景色を「黒板色」→「白色」→「黒色」に切り替えることができます。

文字の色についても、文字に対して色指定を直接行っていない場合に限り、以下のように変化します。

|背景色 | 黒板色 | 白色 | 黒色 |
|文字の色 | 白色 | 黒色 | 白色 |

{%include thirdintervalad.html %}

## まとめ
mathletの使い方をまとめてみましたので、Webページで数式を表示してみたくなった際のお試し記述用に使ってみていただけると良いのではないかと思います。

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
