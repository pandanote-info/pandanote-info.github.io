---
title: 関数の積をn回微分する。 - panda大学習帳外伝
description: 関数の積をn回微分してみた。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2021/08/P_20210626_110708_a-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Wed Dec  1 20:55:54 2021 +0900
---
{% include pagelink.md %}
# 関数の積をn回微分する。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
Twitterのタイムラインに流れてきた数学の問題を見ていて少し気になったので、$n$回以上微分可能な2個の関数($f(x), g(x)$とおきます。)の積を$n$回微分した結果が

\begin{align}
\frac{d^n}{dx^n}[f(x)g(x)] &= \sum_{k=0}^n
\begin{pmatrix}
n \cr
k
\end{pmatrix}
\frac{d^k}{dx^k}f(x) \frac{d^{n-k}}{dx^{n-k}}g(x) \label{eq:conclusion}
\end{align}

と表せることを確認してみることにしました。

{% include firstad.html %}

## 方針
数学的帰納法で示します。

すなわち、$l (\lt n)$回微分のときに(\ref{eq:conclusion})が成り立つならば、$l+1$回微分のときでも(\ref{eq:conclusion})がまた成り立つことを示しつつ、$l=1$の場合でも(\ref{eq:conclusion})が真であることを示すことにより、$1 \le l \le n$を満たすすべての整数$l$について(\ref{eq:conclusion})が真であることを示します。

{%include secondintervalad.html %}

## 計算
(\ref{eq:conclusion})で$n=l$とおいた式をもう1回微分します。

すると…

\begin{align}
  \frac{d^{l+1}}{dx^{l+1}}[f(x)g(x)] &= \frac{d}{dx}\left[ \frac{d^{l}}{dx^{l}}[f(x)g(x)] \right] \nonumber \cr
  &= \frac{d}{dx}\left[ \sum_{k=0}^l
\begin{pmatrix}
l \cr
k
\end{pmatrix}
\frac{d^k}{dx^k}f(x) \frac{d^{l-k}}{dx^{l-k}}g(x) \right] \nonumber \cr
  &= \sum_{k=0}^l
\begin{pmatrix}
l \cr
k
\end{pmatrix}
\left[ \frac{d^{k+1}}{dx^{k+1}}f(x) \frac{d^{l-k}}{dx^{l-k}}g(x) + \frac{d^{k}}{dx^{k}}f(x) \frac{d^{l-k+1}}{dx^{l-k+1}}g(x) \right] \label{eq:firstform}
\end{align}

と計算できます。

ここで、(\ref{eq:firstform})式の$f(x)$側の微分回数に注目し、$f(x)$の$m (1 \le m \le l)$回微分の項($m = 0,l+1$の場合は別途検討します。)の係数を取り出すと…

\begin{align}
  (f(x)\mbox{の}m\mbox{回微分の項}) &= \begin{pmatrix}
l \cr
m-1
\end{pmatrix} + \begin{pmatrix}
l \cr
m
\end{pmatrix} \label{eq:termofm}
\end{align}

になることがわかります。

(\ref{eq:termofm})式をもう少し変形してみます。

すると…

\begin{align}
  \begin{pmatrix}
l \cr
m-1
\end{pmatrix} + \begin{pmatrix}
l \cr
m
  \end{pmatrix} &= \frac{l!}{(m-1)!(l-m+1)!} + \frac{l!}{m!(l-m)!} \nonumber \cr
  &= \frac{l!m}{m!(l-m+1)!} + \frac{l!(l-m+1)}{m!(l-m+1)!} \nonumber \cr
  &= \frac{l!(m+l-m+1)}{m!(l-m+1)!} \nonumber \cr
  &= \frac{l!(l+1)}{m!(l-m+1)!} \nonumber \cr
  &= \frac{(l+1)!}{m!(l-m+1)!} \nonumber \cr
  &= \begin{pmatrix}
l+1 \cr
m
\end{pmatrix} \label{eq:termofmsecond}
\end{align}

と計算できます。これは、$1 \le m \le l$を満たす$m$について成り立ちます。

また、(\ref{eq:firstform})式より$m=0,l+1$の$m$回微分の項の係数はそれぞれ1となりますが、
\begin{align}
  \begin{pmatrix}
l+1 \cr
0
  \end{pmatrix} &= \begin{pmatrix}
l+1 \cr
l+1
  \end{pmatrix} \nonumber \cr
  &= 1 \label{eq:termofmthird}
\end{align}
であるため、(\ref{eq:termofmsecond})式に含めることができます。したがって、$l (< n)$回微分のときに(\ref{eq:conclusion})が成り立つならば、$l+1$回微分のときでも(\ref{eq:conclusion})がまた成り立つことがわかります。

また、$l=1$の場合については

\begin{align}
  \frac{d}{dx}[f(x)g(x)] &= g(x)\frac{d}{dx}f(x) + f(x)\frac{d}{dx}g(x) \nonumber \cr
  &= \sum_{k=0}^1
\begin{pmatrix}
1 \cr
k
\end{pmatrix}
\frac{d^k}{dx^k}f(x) \frac{d^{1-k}}{dx^{1-k}}g(x) \label{eq:conclusionatfirst}
\end{align}

となります。

これは(\ref{eq:conclusion})式を満たしますので、$l$が1以上$n$以下のすべての整数の場合において、(\ref{eq:conclusion})が成り立ちます。$\blacksquare$

{%include thirdintervalad.html %}

## まとめ
ここまでの計算の全体を通して壮大かつスペクタクルなオチはありませんが、二項係数がしれっと現れるところが興味深いところです。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
