---
title: sqrt(1-t)をx=0を中心にテイラー展開してみた。- panda大学習帳外伝
description: sqrt(1-t)をx=0を中心にテイラー展開してみたら一般化二項係数の形式で書くと簡潔に書けることがわかったので、φ(..)メモメモ
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2020/05/P_20200430_125724_vHDR_On_HP-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
---
{% include pagelink.md %}
# sqrt(1-t)をx=0を中心にテイラー展開してみた。
## はじめに
(\ref{eq:minushalftimesofoneminusx})式を$x=0$を中心にテイラー展開してみたら、いろいろあったので、ここにメモ書きすることにしました。
\begin{align}
f(x)&= (1-x)^{\frac{1}{2}} \label{eq:minushalftimesofoneminusx}
\end{align}
なお、$x$の定義域は$x \in [0,1]$とするので、テイラー展開を行った結果得られる関数は絶対収束するものと仮定し、絶対収束性についての議論は省略します。

{% include firstad.html %}

## まず、普通にテイラー展開。
$f(x)$を$x=0$を中心としたテイラー展開は(\ref{eq:taylorexpansion})式で表されます。
\begin{align}
f(x) &= \sum_{n=0}^{\infty} \frac{f^{(n)}(0)}{n!}x^n \label{eq:taylorexpansion}
\end{align}
(\ref{eq:taylorexpansion})式の右辺をじっと見る限り、$f^{(n)}(0)$を求める必要がありそうな感じがするので、(\ref{eq:minushalftimesofoneminusx})式を2,3回ほど微分してみます。

すると…
\begin{align}
f^{\prime}(x) &= -(1-t)^{-\frac{1}{2}} \cdot \frac{1}{2} \nonumber \cr
f^{\prime\prime}(x) &= (-1)^2\cdot(1-t)^{-\frac{1}{2}} \cdot \frac{1}{2} \cdot \left( -\frac{1}{2} \right)\nonumber \cr
&= (-1)^2\cdot\frac{1}{2} \cdot \left( -\frac{1}{2} \right)(1-t)^{-\frac{3}{2}} \nonumber \cr
&= (-1)^3\cdot\frac{1}{2} \cdot \frac{1}{2} \cdot (1-t)^{-\frac{3}{2}} \nonumber \cr
f^{(3)}(x) &= (-1)^3\cdot\frac{1}{2} \cdot \left( -\frac{1}{2} \right)\cdot \left( -\frac{3}{2} \right)(1-t)^{-\frac{5}{2}} \nonumber \cr
&= (-1)^5\cdot\frac{1}{2} \cdot \frac{1}{2} \cdot \frac{3}{2} \cdot (1-t)^{-\frac{5}{2}} \nonumber
\end{align}
となるので、$n \ge 1$の場合に限り、
\begin{align}
  f^{(n)}(x) &= (-1)^{2n-1} \frac{(2n-3)!!}{2^n}(1-t)^{-\frac{2n-1}{2}} \nonumber \cr
  &= -\frac{(2n-3)!!}{2^n}(1-t)^{-\frac{2n-1}{2}} \label{eq:taylorcoefficient}
\end{align}
となりそうな感じがします。なお、$(2n-3)!!$の$!!$は二重階乗を表しますが、$k \le 1$の場合は$k!! = 1$とします。

念のため(\ref{eq:taylorcoefficient})式を1回微分すると…
\begin{align}
  f^{(n+1)}(x) &= (-1)^{2} \frac{(2n-3)!!}{2^n}\cdot\left(-\frac{2n-1}{2}\right)(1-t)^{-\frac{2n+1}{2}} \nonumber \cr
  &= -\frac{(2n-1)!!}{2^{n+1}}(1-t)^{-\frac{2n+1}{2}} \label{eq:nexttaylorcoefficient}
\end{align}
と計算できます。

(\ref{eq:taylorcoefficient})式の$n$を$n+1$とおくと、(\ref{eq:nexttaylorcoefficient})式と一致していることが確認できます。

よって、(\ref{eq:taylorcoefficient})式に$x=0$を代入すると、$n \ge 1$の場合に限り、
\begin{align}
f^{(n)}(0) &= -\frac{(2n-3)!!}{2^n} \label{eq:xatzero}
\end{align}
となるので、$f(0) = 1$であることとまとめると、
\begin{align}
(1-x)^{\frac{1}{2}} &= 1 - \sum_{n=1}^{\infty} \frac{(2n-3)!!}{2^n n!}x^n \label{eq:expansionsolution}
\end{align}
となります。$\blacksquare$

{%include secondintervalad.html %}

## 一般化二項係数で表してみる。
(\ref{eq:expansionsolution})式が求まると、数値計算ができそうな感じになります。楕円積分の計算の際にはこの形式を使うことが一般的です。

しかーし、もののWikipediaによりますと、一般化二項係数でもう少し簡潔な形で表現できるかもしれないっぽいので、(\ref{eq:expansionsolution})式の係数部を変形してみることにします。
### 説明しよう:-)
ここで、一般化二項係数について説明しよう :-)

二項級数の係数は負でない整数$n,k$について、二項係数${}_nC_r$は

\begin{align}
{}_nC_r &= \begin{pmatrix}
n \cr
r
\end{pmatrix}
\label{eq:binomialcoeffcientinpmatrix}
\end{align}
で表すことができます。これを$n$が負でない整数($m$と書きます。)以外の場合にも拡張することを考えると、
\begin{align}
\begin{pmatrix}
m \cr
r
\end{pmatrix}
&= \frac{1}{r!}\cdot\underbrace{m\cdot(m-1)\cdots(m-r+1)}_{r\,\mbox{factors}} \label{eq:generalizedbinomialcoeffcient}
\end{align}
と書くことができます。これを一般化二項係数と呼びます。なお、(\ref{eq:generalizedbinomialcoeffcient})式の右辺はポッホパマーの記号$(\cdot)_k$を用いると、$(m)_r$と書くことができます。
### 変形してみた。
ここからは、(\ref{eq:expansionsolution})式の右辺の係数部が(\ref{eq:generalizedbinomialcoeffcient})式の右辺のような形式で表現できないか考えていきます。

いったん$n=0$の場合のことは忘れて、$n \ge 1$の場合について考えると、(\ref{eq:expansionsolution})式の右辺の係数部の分子では1から$2n-3$までの奇数が$(n-1)$個掛け合わされていて、分母には2が$n$個掛け合わされているので…
\begin{align}
-\frac{(2n-3)!!}{2^n n!} &= -\underbrace{\frac{1}{2}\cdot\frac{3}{2}\cdots\frac{2n-3}{2}}_{(n-1)\mbox{個}}\frac{1}{2}\cdots\frac{1}{n!} \label{eq:binomialtryfirst}
\end{align}
と変形できます。

さらに、(\ref{eq:binomialtryfirst})式の右辺の最初の部分と最後の部分に着目し、最後にくっついている$\displaystyle\frac{1}{2}$を先頭に移動すると…
\begin{align}
  -\frac{(2n-3)!!}{2^n n!} &= \underbrace{-\frac{1}{2}\cdot\frac{1}{2}\cdot\frac{3}{2}\cdots\frac{2n-3}{2}}_{n\mbox{個}}\cdots\frac{1}{n!} \label{eq:binomialtrysecond}
\end{align}
(\ref{eq:generalizedbinomialcoeffcient})式の右辺と(\ref{eq:binomialtrysecond})式の右辺をよーく比較すると、(\ref{eq:generalizedbinomialcoeffcient})式の右辺において$r$を$n$, $n$を$\displaystyle\frac{2n-3}{2}$とそれぞれおくと、(\ref{eq:binomialtrysecond})式の右辺と一致させることができることがわかります。

よって、$n \ge 1$の場合には、
\begin{align}
-\frac{(2n-3)!!}{2^n n!} &= \begin{pmatrix}
\frac{2n-3}{2} \cr
n
\end{pmatrix} \nonumber \cr
&= \begin{pmatrix}
n-\frac{3}{2} \cr
n
\end{pmatrix} \label{eq:binominaltrythird} 
\end{align}
と書けて、一般化二項係数の形式で書けることがわかります。

ここまでは$n \ge 1$の場合について考えましたが、$n = 0$の場合については(\ref{eq:binominaltrythird})式の左辺は-1、右辺は1となるため等式は成立しません。しかし、右辺は1となることから、一般化二項係数の形式で書く場合には$n = 0$の場合も$n \ge 1$の場合とまとめて扱うことができて…
\begin{align}
(1-x)^{\frac{1}{2}} &= \sum_{n=o}^{\infty} \begin{pmatrix}
n-\frac{3}{2} \cr
n
\end{pmatrix}x^n\label{eq:binominalfinal}
\end{align}
と書くことができます。$\blacksquare$

{%include thirdintervalad.html %}

## まとめ
それにしても「一般化二項係数」って「一酸化二窒素$(N_2O)$」みたいなネーミングですね。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
