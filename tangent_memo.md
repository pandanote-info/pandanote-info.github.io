---
title: 時々忘れがちになるタンジェントの公式の導き方のメモ(余談を添えて)。 - panda大学習帳外伝
description: サインとコサインの公式からタンジェントの加法定理と倍角の公式を導出します。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2021/11/tan1_rational_number.png
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sat Nov  6 01:10:12 2021 +0900
---
{% include pagelink.md %}
# 時々忘れがちになるタンジェントの公式の導き方のメモ(余談を添えて)。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
いきなり余談です。

ちょっと面白いフォントがないかと思い探してみたところ、[「Oradano明朝GSRR」フォント](http://www.asahi-net.or.jp/~sd5a-ucd/freefonts/Oradano-Mincho/)という明治時代の明朝体を再現したフォントがあったので、インストールして[バナー画面等で使ってみた](https://vsse.pandanote.info/)ところ、いい感じで使えています。

そこで、大学入試の試験問題をOradano明朝GSRRで書いてみると…

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">Oradano明朝GSRRフォントを使って、100年くらい前の大学入試の問題っぽくしてみた。<br>※2006年の京都大学の入試問題です。<a href="https://twitter.com/hashtag/lifeinyokohama?src=hash&amp;ref_src=twsrc%5Etfw">#lifeinyokohama</a> <a href="https://t.co/M8VbrQK83b">pic.twitter.com/M8VbrQK83b</a></p>&mdash; pandanote.info (@Pandanote_info) <a href="https://twitter.com/Pandanote_info/status/1452417042955390980?ref_src=twsrc%5Etfw">October 24, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

昔の帝國大学の試験の問題っぽい見た目になります。

{% include firstad.html %}

それで、↑のような問題を目にすると「tanの公式ってどんなのがあるんだっけ?」と思うところですが、tanの公式はあまり使う機会がないので、暗記しても忘れがちです。

そこで、tanの公式のうち、↑の問題を解くのに必要そうなものをsinとcosの公式から導く方法についてメモすることにしました。

## tanの公式2選
### 加法定理
$\sin$、$\cos$及び$\tan$の間には…

\begin{align}
\tan\theta &= \frac{\sin\theta}{\cos\theta}\label{eq:sincostan}
\end{align}

という関係があります。

また、$\sin$と$\cos$の加法定理の公式は

\begin{align}
\sin (\alpha + \beta ) &= \sin\alpha\cos\beta + \cos\alpha\sin\beta \label{eq:sinadd} \cr
\cos (\alpha + \beta ) &= \cos\alpha\cos\beta - \sin\alpha\cos\beta \label{eq:cosadd}
\end{align}

で表すことができます。

そこで、(\ref{eq:sincostan})式で$\theta = \alpha + \beta$とおいて、(\ref{eq:sinadd})式及び(\ref{eq:cosadd})式と組み合わせると…

\begin{align}
\tan(\alpha + \beta) &= \frac{\sin(\alpha + \beta)}{\cos(\alpha + \beta)} \nonumber \cr
&= \frac{\sin\alpha\cos\beta + \cos\alpha\sin\beta}{\cos\alpha\cos\beta - \sin\alpha\cos\beta} \label{eq:tanaddfirst}
\end{align}

次に、(\ref{eq:tanaddfirst})式右辺の分母及び分子から$\sin$及び$\cos$を排除し、$\tan$及び定数のみを含んだ形式で表現できないか考えます。

(\ref{eq:sincostan})式の形から、分母に$\cos$が出てくれば$\tan$を含んだ形式に変形できそうですので、(\ref{eq:tanaddfirst})式右辺の分母及び分子を$\cos\alpha\cos\beta$で割ってみます。

すると…
\begin{align}
\frac{\sin\alpha\cos\beta + \cos\alpha\sin\beta}{\cos\alpha\cos\beta - \sin\alpha\cos\beta} &= \frac{\displaystyle\frac{\sin\alpha\cos\beta + \cos\alpha\sin\beta}{\cos\alpha\cos\beta}}{\displaystyle\frac{\cos\alpha\cos\beta - \sin\alpha\cos\beta}{\cos\alpha\cos\beta}} \nonumber \cr
&= \frac{\displaystyle\frac{\sin\alpha\cos\beta}{\cos\alpha\cos\beta} + \displaystyle\frac{\cos\alpha\sin\beta}{\cos\alpha\cos\beta}}{\displaystyle\frac{\cos\alpha\cos\beta}{\cos\alpha\cos\beta} - \displaystyle\frac{\sin\alpha\cos\beta}{\cos\alpha\cos\beta}} \nonumber \cr 
&= \frac{\displaystyle\frac{\sin\alpha}{\cos\alpha} + \displaystyle\frac{\sin\beta}{\cos\beta}}{1 - \displaystyle\frac{\sin\alpha\cos\beta}{\cos\alpha\cos\beta}} \nonumber \cr 
&= \frac{\tan\alpha + \tan\beta}{1 - \tan\alpha\tan\beta} \label{eq:tanaddsecond}
\end{align}
となって、$\tan$及び定数のみを含んだ式が現れます。

(\ref{eq:tanaddfirst})及び(\ref{eq:tanaddsecond})式をまとめると、

\begin{align}
\tan(\alpha + \beta) &= \frac{\tan\alpha + \tan\beta}{1 - \tan\alpha\tan\beta} \label{eq:tanaddfinal}
\end{align}

であることがわかります。

(\ref{eq:tanaddfinal})式がタンジェントの加法定理の式になります。$\blacksquare$
### 2倍角の公式
(\ref{eq:tanaddfinal})式で$\beta = \alpha$とおくと…

\begin{align}
\tan 2\alpha &= \frac{2\tan\alpha}{1 - \tan^2\alpha} \label{eq:tandouble}
\end{align}

であることがわかります。

(\ref{eq:tandouble})式がタンジェントの2倍角の公式です。$\blacksquare$

{%include secondintervalad.html %}

## まとめ
ここまでの議論でタンジェントの加法定理と2倍角の公式を無事導出できました。

…で、この議論のきっかけとなった冒頭の入試問題ですが、(概略ですが、)以下のような感じで結論までたどり着くことができます。

$\tan 1^{\circ}$が有理数であるかないかだけを示せばよい(具体的な値は求めなくてよい。)ので、$\tan 1^{\circ}$が有理数であると仮定し、適当な整数$a,b(b \neq 0)$を用いて$\tan 1^{\circ} = \displaystyle\frac{a}{b}$と書くことにします。

すると、タンジェントの2倍角の公式を用いて$\tan 2^{\circ}$を$a,b$を用いて表すことができる有理数であることを計算によって示すことができます(計算については省略します)。これを繰り返すと負でない整数$k$について$\tan 2^k{}^{\circ}$、すなわち$\tan 1^{\circ}, \tan 2^{\circ}, \cdots, \tan 32^{\circ}, \cdots$が有理数であることになります。

ここでタンジェントの加法定理が登場します。$\tan 30^{\circ} = \tan (32^{\circ}+\tan (-2^{\circ}))$と書けますが、$\tan 32^{\circ}$及び$\tan 2^{\circ}$が有理数であるならば、タンジェントの加法定理により$\tan 30^{\circ}$も有理数であると計算できます。しかし、$\tan 30^{\circ} = \displaystyle\frac{1}{\sqrt{3}}$であり、この数は無理数ですから、ここで矛盾が生じます。よって$\tan 1^{\circ}$は有理数でない、という結論になります(たぶん)。

## リンク
[panda大学習帳のpandaの大計算用紙のカテゴリ](https://pandanote.info/?cat=13) \| {% include pagelink.md %}

{% include fourthintervalad.html %}
