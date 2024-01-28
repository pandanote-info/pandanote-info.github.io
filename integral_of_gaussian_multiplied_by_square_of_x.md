---
title: x^{2n}e^{-x^2}の実数全体にわたる積分を計算してみた。 - panda大学習帳外伝
description: $\displaystyle\int_{-\infty}^{\infty}x^2e^{-x^2}dx$を計算するついでに$x^2$のところを$x^{2n}$として計算してみました。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2024/01/P_20240127_122933_a.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sun Jan 28 16:35:00 2024 +0900
---
{% include pagelink.md %}
# x^{2n}e^{-x^2}の実数全体にわたる積分を計算してみた。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
ちょっとした野暮用で、

\begin{align}
I_2&=\int_{-\infty}^{\infty} x^2e^{-x^2}dx\label{eq:x2exm2}
\end{align}

を計算する必要が出てきました。

そこでついでに、

\begin{align}
I_{2n}&=\int_{-\infty}^{\infty} x^{2n}e^{-x^2}dx\label{eq:x2nexm2}
\end{align}

$(n \gt 0)$も計算してみることにします。

### ちょっとしたおことわり
なお、$x^{2n-1}$は奇関数、$e^{-x^2}$は偶関数になるので、

\begin{align}
I_{2n-1}&=\int_{-\infty}^{\infty} x^{2n-1}e^{-x^2}dx\nonumber\cr
&= 0 \label{eq:xoddexm2}
\end{align}

となります。

さらに、以下の式も既知とし、証明を省略して利用します。

\begin{align}
\int_{-\infty}^{\infty}e^{-x^2} &= \sqrt{\pi} \label{eq:gaussintegral}
\end{align}

{% include firstad.html %}
## サクサク計算
例によってサクサクと計算します。
### I_2を計算

まず、(\ref{eq:x2exm2})式を計算します。部分積分を用いて、

\begin{align}
I_2 &= \int_{-\infty}^{\infty} x\left(-\frac{1}{2}e^{-x^2}\right)^{\prime}dx \nonumber\cr
&= \left[ -\frac{x}{2}e^{-x^2}\right]\_{-\infty}^{\infty} - \int_{-\infty}^{\infty} \left(-\frac{1}{2}e^{-x^2}\right)dx\label{eq:x2exm2firstform}
\end{align}

と変形できます。

ここで、(\ref{eq:x2exm2firstform})式右辺第1項は(\ref{eq:xoddexm2})式より0であり、第2項については(\ref{eq:gaussintegral})式を利用すると…

\begin{align}
I_{2n} &= \int_{-\infty}^{\infty}\frac{1}{2}e^{-x^2}dx\nonumber\cr
&= \frac{\sqrt{\pi}}{2}\label{eq:x2exm2finalform}
\end{align}

と計算できます。$\blacksquare$

{%include secondintervalad.html %}

### I_{2n}を計算
この調子で、(\ref{eq:x2nexm2})式を計算してみます。$I_{2n}$を$I_{2n-2}, \cdots , I_2$のいずれで表せないか考えます。

$I_2$の計算時と同様に、部分積分を用いて変形します。

すると…

\begin{align}
I_{2n} &= \int_{-\infty}^{\infty} x^{2n-1}\left(-\frac{1}{2}e^{-x^2}\right)^{\prime}dx \nonumber\cr
&= \left[ -\frac{x^{2n-1}}{2}e^{-x^2}\right]\_{-\infty}^{\infty} - \int_{-\infty}^{\infty} (2n-1)x^{2n-2}\left(-\frac{1}{2}e^{-x^2}\right)dx\label{eq:x2nexm2firstform}
\end{align}

と変形できます。

ここで、(\ref{eq:x2nexm2firstform})式右辺第1項は(\ref{eq:xoddexm2})式より0であることを利用すると、(\ref{eq:x2nexm2firstform})式は…

\begin{align}
I_{2n} &= \frac{2n-1}{2}\int_{-\infty}^{\infty}x^{2n-2}e^{-x^2}dx\nonumber\cr
&= \frac{2n-1}{2}I_{2n-2}\label{eq:x2nexm2secondform}
\end{align}

と書くことができ、$n$についての漸化式で書くことができることがわかります。

そこで、ここまでの式変形を(\ref{eq:x2nexm2secondform})式の右辺に対して$(n-2)$回繰り返すと…

\begin{align}
I_{2n} &= \frac{(2n-1)\cdots 3}{\underbrace{2 \cdots 2}_{(n-1)個}}I_2 \nonumber\cr
&= \frac{(2n-1)!!}{2^{n-1}}\frac{\sqrt{\pi}}{2}\nonumber\cr
&= \frac{(2n-1)!!\sqrt{\pi}}{2^n} \label{eq:x2nexm2thirdform}
\end{align}

と計算できます。$\blacksquare$

なお、$!!$は二重階乗を表す記号で、

\begin{align}
(2n-1)!! &= \prod_{k=1}^{n}(2k-1) \label{eq:doublefactorial}
\end{align}

です。

{%include thirdintervalad.html %}

## まとめ
ガウス関数に関する5次以上の高次のモーメントを計算する機会はあまりないかもしれませんが、(\ref{eq:x2nexm2thirdform})式自体はいい感じの式になっているので、試験の問題等には出題しやすい式かもしれません。

この記事は以上です。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
