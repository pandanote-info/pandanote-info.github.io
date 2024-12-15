---
title: xのx乗の微分を計算してみた。 - panda大学習帳外伝
description: とりあえずxのx乗の微分を計算してみました。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2024/08/P_20240822_080140-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sun Dec 15 16:16:25 2024 +0900
---
{% include pagelink.md %}
# xのx乗の微分を計算してみた。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
むかし東大が東京帝國大學と言っていた頃の入学試験問題で…

$x^{x^x}$を微分せよ。

という問題が出題されたことがあったそうです。

{% include firstad.html %}

簡単なように見えてかなり計算に手間取りそうな予感がします。

$x^{x^x}$を直接考えるよりも先に、まず$x^x$を考えた方が良さそうだと思ったので、$x^x$の微分を考えることにしました。
## サクサクと計算
計算すると決めたらサクサクと計算です。

$y=x^x$とおいて、両辺の対数を取ります。

すると…

\begin{align}
\log y &= x\log x\label{eq:yxlogx}
\end{align}

となります。

ここで両辺を$x$で微分するのですが、

\begin{align}
\frac{d(\log y)}{dx} &= \frac{d(\log y)}{dy} \frac{dy}{dx} \label{eq:dlogydx}
\end{align}

と(形式的に)書けるので、

\begin{align}
\frac{1}{y} \frac{dy}{dx} &= \log x+1 \label{eq:invydydx}
\end{align}

すなわち、

\begin{align}
  \frac{dy}{dx} &= y(\log x + 1) \nonumber \cr
  &= x^x(log x+1)\label{eq:finalform}
\end{align}

となることがわかります。$\blacksquare$

$f(x)=x$とおくと、$x \gt 1$のときに、$f(x)<f^\prime(x)$となるので、

「$x \le 1$の時はともかく、$x \gt 1$の時に急激に増加する関数」であることがわかります。

{%include secondintervalad.html %}
## まとめ
$x^{x^x}$は気が向いたら計算しますが、$x^x$を微分した結果を利用すると計算が捗るかもしれません。

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
