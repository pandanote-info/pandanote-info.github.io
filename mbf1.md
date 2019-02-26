---
title: panda大学習帳外伝
description: 第1種変形Bessel関数の次数が整数のときに成り立つ関係式を証明してみた。
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}

# 第1種変形Bessel関数の次数が整数のときに成り立つ関係式を証明してみた。
## はじめに
この記事では、第1種変形Bessel関数$I_n(x)$の次数が整数のときに成り立つ関係式

\begin{align}
I_n(x) &= I_{-n}(x) \label{eq:mbf1int}
\end{align}

を$I_n(x)$の級数による表現((\ref{eq:mbf1inpowerseries})式)を計算することで示してみます。
\begin{align}
I_n(x) &= \left(\frac{x}{2}\right)^n\sum_{p=0}^{\infty}\frac{1}{p!\Gamma(n+p+1)}\left(\frac{x}{2}\right)^{2p} \label{eq:mbf1inpowerseries}
\end{align}
## サクサクと計算します。
{% include firstad.html %}
まず、(\ref{eq:mbf1int})式の右辺から左辺を引きます。すると…
\begin{align}
I_{-n}(x)-I_{n}(x) &= \left(\frac{x}{2}\right)^{-n}\sum_{p=0}^{\infty}\frac{1}{p!\Gamma(-n+p+1)}\left(\frac{x}{2}\right)^{2p} - \left(\frac{x}{2}\right)^n\sum_{p=0}^{\infty}\frac{1}{p!\Gamma(n+p+1)}\left(\frac{x}{2}\right)^{2p} \label{eq:mbf1diff}
\end{align}
となります。
### 分母をよく見ます。
いきなり計算に行き詰った感じがしなくもないですが、ここで(\ref{eq:mbf1diff})の右辺第1項の分母のあたりに注目すると、$\Gamma$関数の引数が正でない整数になる場合があること、すなわち、$0 \le p \le n-1, p \in \mathbb{Z}$のときは$-n+p+1 \le 0$となるので、
\begin{align}
\frac{1}{p!\Gamma(-n+p+1)} &= 0 \label{eq:mdf1ignore}
\end{align}
となることがわかります。

そこで、(\ref{eq:mdf1ignore})式を(\ref{eq:mbf1diff})式に適用すると…
\begin{align}
I_{-n}(x)-I_{n}(x) &= \left(\frac{x}{2}\right)^{-n}\sum_{p=n}^{\infty}\frac{1}{p!\Gamma(-n+p+1)}\left(\frac{x}{2}\right)^{2p} - \left(\frac{x}{2}\right)^n\sum_{p=0}^{\infty}\frac{1}{p!\Gamma(n+p+1)}\left(\frac{x}{2}\right)^{2p} \label{eq:mbf1diffignored}
\end{align}

{% include secondintervalad.html %}

さらに、(\ref{eq:mbf1diffignored})式の右辺第1項だけ$p$を$p+n$に置き換えると…

\begin{align}
I_{-n}(x)-I_{n}(x) &= \left(\frac{x}{2}\right)^{-n}\sum_{p=0}^{\infty}\frac{1}{(p+n)!\Gamma(p+1)}\left(\frac{x}{2}\right)^{2(p+n)} - \left(\frac{x}{2}\right)^n\sum_{p=0}^{\infty}\frac{1}{p!\Gamma(n+p+1)}\left(\frac{x}{2}\right)^{2p} \label{eq:mbf1diffreplaced}
\end{align}

と書き換えることができます。
### 次は$x$の冪に着目します。
次は、(\ref{eq:mbf1diffreplaced})式の右辺の第1項と第2項をまとめることを考えます。

$\sum$の前に括り出されている$x$の冪を$\sum$の中に入れてみます。すると…

\begin{align}
I_{-n}(x)-I_{n}(x) &= \sum_{p=0}^{\infty}\frac{1}{(p+n)!\Gamma(p+1)}\left(\frac{x}{2}\right)^{2p+n} - \sum_{p=0}^{\infty}\frac{1}{p!\Gamma(n+p+1)}\left(\frac{x}{2}\right)^{2p+n} \label{eq:mbf1diffxpn}
\end{align}

となるので、$x$の指数を$2p+n$で揃えることができました!! (｀・ω・´)

### 最後の仕上げです。
ここから最後の仕上げにかかります。

$n,p$はともに整数で、(\ref{eq:mbf1diffxpn})式右辺の$\Gamma$関数の引数はすべて正の数ですから、(\ref{eq:mbf1diffxpn})式右辺に登場している$\Gamma$関数はすべて階乗の形で表すことができます。よって、(\ref{eq:mbf1diffxpn})式の右辺は…

\begin{align}
I_{-n}(x)-I_{n}(x) &= \sum_{p=0}^{\infty}\frac{1}{(p+n)!p!}\left(\frac{x}{2}\right)^{2p+n} - \sum_{p=0}^{\infty}\frac{1}{p!(n+p)!}\left(\frac{x}{2}\right)^{2p+n} \nonumber \cr
{} &= 0 \label{eq:mbf1diffqed}
\end{align}

と計算できて、右辺は$0$になります。

よって、(\ref{eq:mbf1int})式が成り立つことがわかります。$\qquad\blacksquare$

{% include thirdintervalad.html %}

# まとめ
(\ref{eq:mbf1int})式自体は極めてシンプルな式ですが、その級数表現を見る限りでは成り立つことについてはあまり自明ではないと感じたので、計算を行ってみました。

この記事は以上です。

## 参考文献

* [ベッセルの微分方程式](http://eman-physics.net/math/differential20.html)

## リンク 
{% include pagelink.md %}

{% include fourthintervalad.html %}
