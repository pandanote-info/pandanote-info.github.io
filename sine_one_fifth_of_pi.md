---
title: panda大学習帳外伝
description: sin(pi/5)及びcos(pi/5)を計算してみた。
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}

# $\sin\dfrac{\pi}{5}$及び$\cos\dfrac{\pi}{5}$を計算してみた。
## はじめに
ちょいと野暮用で必要になりそうなので、$\sin\dfrac{\pi}{5}$及び$\cos\dfrac{\pi}{5}$の値を計算してみました。
## まずはcosから。
$\cos\dfrac{\pi}{5} = t$とおくと、cosの2倍角及び3倍角の公式より、
\begin{align}
  \cos\dfrac{2}{5}\pi &= 2t^2-1 \label{eq:cosdouble} \cr
  \cos\dfrac{3}{5}\pi &= 4t^3-3t \label{eq:costriple}
\end{align}
となります。

{% include firstad.html %}

ここで、
\begin{align}
  \cos\dfrac{3}{5}\pi &= -\cos\left(\pi-\dfrac{3}{5}\pi\right) \nonumber \cr
  &= -\cos\dfrac{2}{5}\pi \label{eq:doubletriple}
\end{align}
であることから、(\ref{eq:cosdouble})式及び(\ref{eq:costriple})式を用いると(\ref{eq:cosequation})式のように計算できます。
\begin{align}
  4t^3+2t^2-3t-1 &= 0 \label{eq:cosequation}
\end{align}
(\ref{eq:cosequation})式は$t=-1$を解の1つとして持ちますが、$0 \gt \cos\dfrac{\pi}{5} \gt 1$ですので、両辺を$t+1$で割ることができて、
\begin{align}
  4t^2-2t-1 &= 0 \label{eq:cosequationsecond}
\end{align}
となります。

(\ref{eq:cosequationsecond})式を解き、$t \lt 0$の解を求めると、
\begin{align}
  t &= \frac{1+\sqrt{5}}{4}
\end{align}
となります。$\blacksquare$
## ちょっと検算。
(\ref{eq:doubletriple})式が成り立つことを確認してみます。

\begin{align}
  \cos\dfrac{2}{5}\pi &= 2t^2-1 \nonumber \cr
  &= 2\frac{6+2\sqrt{5}}{16}-1 \nonumber \cr
  &= \frac{3+\sqrt{5}}{4}-1 \nonumber \cr
  &= \frac{\sqrt{5}-1}{4} \cr
  \cos\dfrac{3}{5}\pi &= t(4t^2-3) \nonumber \cr
  &= t(4\frac{6+2\sqrt{5}}{16}-3) \nonumber \cr
  &= \frac{\sqrt{5}+1}{4}\,(\frac{3+\sqrt{5}}{2}-3) \nonumber \cr
  &= \frac{\sqrt{5}+1}{4}\,\frac{-3+\sqrt{5}}{2} \nonumber \cr
  &= \frac{2-2\sqrt{5}}{8} \nonumber \cr
  &= \frac{1-\sqrt{5}}{4} \nonumber \cr
  &= -\cos\dfrac{2}{5}
\end{align}
になります。

(\ref{eq:doubletriple})式が成り立ちそうです。������

{% include secondintervalad.html %}

## 次にsinを求めます。
$\sin\dfrac{2}{5}\pi$は$\sin\dfrac{2}{5}\pi > 0$であることと、前節の結果より、
\begin{align}
  \sin\dfrac{2}{5}\pi &= \sqrt{1-\cos^2\frac{2}{5}\pi} \nonumber \cr
  &= \sqrt{\frac{5-\sqrt{5}}{8}} \nonumber \cr
  &= \frac{\sqrt{10-2\sqrt{5}}}{4}
\end{align}
となります。$\blacksquare$

{% include thirdintervalad.html %}

## まとめ
$\sin\dfrac{\pi}{5}$及び$\cos\dfrac{\pi}{5}$の計算は電卓で計算することがほとんどたっだりすることと、$\sin\dfrac{\pi}{5}$に至っては結果に二重根号が登場しますので、あまりなじみがないかもしれません。

何かの参考にしていただけると幸いです。

# リンク
[panda大学習帳のpandaの大計算用紙のカテゴリ](https://pandanote.info/?cat=13) \| {% include pagelink.md %}

{% include fourthintervalad.html %}
