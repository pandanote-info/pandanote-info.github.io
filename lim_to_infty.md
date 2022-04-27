---
title: xe^{-x}でx→∞としたときの極限が0になることを確認したときのメモ。 - panda大学習帳外伝
description: 時々疑心暗鬼になるところです。
mathjax: true
image: https://ipfs.io/ipfs/QmXTvaspK3zR4MKvKgAPG43HFcfc7oMhRkNTH99WnWxs2Q
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Wed Apr 27 19:44:26 2022 +0900
---
{% include pagelink.md %}
# xe^{-x}でx→∞としたときの極限が0になることを確認したときのメモ。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
みんな大好き
\begin{align}
f(x) &= xe^{-x} \label{eq:xeoverminusx}
\end{align}
で$x \to \infty$としたときの極限 $\displaystyle\lim_{x \to \infty} f(x)$を求めてみます。

{% include firstad.html %}

## サクサク計算
### 略解
まずは略解です。

$x > 0$のときは(\ref{eq:exapprox})式が成り立つことを利用します。

\begin{align}
e^x &> 1 + x + \frac{x^2}{2} \label{eq:exapprox}
\end{align}

(\ref{eq:exapprox})式の両辺の逆数を取ると…

\begin{align}
e^{-x} &< \frac{1}{1 + x + \displaystyle\frac{x^2}{2}} \label{eq:mexapprox}
\end{align}

が成り立ちます。

すると、$x > 0$で$xe^{-x} > 0$であり、さらに(\ref{eq:xexapprox})式が成り立ちます。

\begin{align}
xe^{-x} &< \frac{x}{1 + x + \displaystyle\frac{x^2}{2}} \cr
 &= \frac{1}{\displaystyle\frac{1}{x} + 1 + \displaystyle\frac{x}{2}} \label{eq:xexapprox}
\end{align}

(\ref{eq:xexapprox})式右辺の分母は$x \to \infty$のとき$+\infty$に発散するので、(\ref{eq:xexapprox})式の右辺全体としては0に収束します。

よって、

\begin{align}
\lim_{x \to \infty} f(x) &= 0 \label{eq:solution}
\end{align}

となります。$\blacksquare$

{%include secondintervalad.html %}

### (2)式の確認
(\ref{eq:exapprox})式を無条件で使うべきではないかもしれませんので、確認します。

以下の関数$g(x) (x \ge 0)$を考えます。$x > 0$ならば$g(x) > 0$であることを示します。

\begin{align}
g(x) &= e^{x} - 1 - x - \frac{x^2}{2} \label{eq:difffunc}
\end{align}

次に、(\ref{eq:difffunc})式の両辺を微分します。

\begin{align}
g^{\prime}(x) &= e^{x} - 1 - x \label{eq:difffuncfirst}
\end{align}

(\ref{eq:difffuncfirst})式の両辺を再度微分します。

\begin{align}
g^{\prime\prime}(x) &= e^{x} - 1 \label{eq:difffuncsecond}
\end{align}

(\ref{eq:difffuncsecond})式より$x > 0$ならば$g^{\prime\prime}(x) > 0$となりますので、$g^{\prime}(x)$は単調増加となります。

さらに、(\ref{eq:difffuncfirst})式より$g^{\prime}(0) = 0$ですので、$x > 0$ならば$g^{\prime}(x)$も正の値でかつ単調増加となります。

ここまでの考察でようやく $g^{\prime}(x)$ の$x > 0$における符号かつ増減がわかったので、$g(x) (x > 0)$の符号及び増減を調べると、(\ref{eq:difffunc})式より$g(0) = 0$であるので、$x > 0$であれば$g(x) > 0$であることがわかります。

よって、(\ref{eq:exapprox})式が成り立つことがわかります。$\blacksquare$

{%include thirdintervalad.html %}

## まとめ
一見どうということはない計算ですが、いろいろなところで登場する(確率分布が指数分布になる連続確率分布の期待値の計算(\ref{eq:eexpodist})式の途中でも登場したりします。)ので、メモ書きしてみました。
\begin{align}
\int_{0}^{\infty} xe^{-x} &= 1 \label{eq:eexpodist}
\end{align}
$xe^{-x}$がどこからともなく現れて夜しか眠れないほど疑心暗鬼になったときなどに、ご参考にしていただれば幸いです。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
