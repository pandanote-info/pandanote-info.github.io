---
title: 正の奇数の二乗の逆数の和を計算する。 - panda大学習帳外伝
description: ついでに、正の奇数のn乗の逆数の和も計算してみました。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2023/08/P_20230827_073334-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sun Aug 27 10:11:18 2023 +0900
---
{% include pagelink.md %}
# 正の奇数の二乗の逆数の和を計算する。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
正の奇数の二乗の逆数の和

\begin{align}
S &= \sum_{n=1}^{\infty}\frac{1}{(2n-1)^2}\label{eq:inverseoddsquare}
\end{align}

を計算してみます。

ただし、

\begin{align}
\sum_{n=1}^{\infty}\frac{1}{n^2} &= \frac{\pi^2}{6}\label{eq:zetatwo}
\end{align}

はバーゼル問題なので既知とします。

{% include firstad.html %}
## サクサクと計算
まず、(\ref{eq:zetatwo})式を奇数の部分と偶数の部分に分解します。すると…

\begin{align}
\sum_{n=1}^{\infty}\frac{1}{n^2} &= \sum_{n=1}^{\infty}\frac{1}{(2n-1)^2}+\sum_{n=1}^{\infty}\frac{1}{(2n)^2}\nonumber\cr
&= S+\frac{1}{4}\sum_{n=1}^{\infty}\frac{1}{n^2}\label{eq:firstform}
\end{align}

と変形できます。よって、

\begin{align}
S &= \frac{3}{4}\sum_{n=1}^{\infty}\frac{1}{n^2} \nonumber\cr
&= \frac{3}{4}\cdot\frac{\pi^2}{6}\nonumber\cr
&= \frac{\pi^2}{8}\label{eq:secondform}
\end{align}

であることがわかります。$\blacksquare$

{%include secondintervalad.html %}
## ちょっとした拡張
ちょっとだけ一般化して、「奇数の逆数を$s$乗した数の総和」を考えます。

まず、

\begin{align}
\sum_{n=1}^{\infty}\frac{1}{n^s} &= \Gamma(s) \label{eq:gammafirst}
\end{align}

とおきます。

前節の方法と同様に変形すると…

\begin{align}
\Gamma(s) &= \sum_{n=1}^{\infty}\frac{1}{(2n-1)^s}+\sum_{n=1}^{\infty}\frac{1}{(2n)^s}\nonumber\cr
&= \sum_{n=1}^{\infty}\frac{1}{(2n-1)^s}-\frac{1}{2^s}\Gamma(s)\label{eq:gammafirstform}
\end{align}

と変形できます。よって、

\begin{align}
\sum_{n=1}^{\infty}\frac{1}{(2n-1)^s} &= \left(1-\frac{1}{2^s}\right)\Gamma(s)\nonumber\cr
&=\frac{2^s-1}{2^s}\,\Gamma(s)\label{eq:gammafinal}
\end{align}

と計算できます。$\blacksquare$

{%include thirdintervalad.html %}
## まとめ
正の奇数の逆数の$n$乗の逆数を急に計算する必要が生じたときにこの記事のことを思い出していただいてお役立ていただけると幸いでございます。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
