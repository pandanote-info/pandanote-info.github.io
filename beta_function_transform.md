---
title: ベータ関数の積分表示の変数変換(あまりメジャーじゃない方) - panda大学習帳外伝
description: ベータ関数の定義式を変数変換してみました。
mathjax: true
image: 
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sat Dec  9 00:00:48 2023 +0900
---
{% include pagelink.md %}
# ベータ関数の積分表示の変数変換(あまりメジャーじゃない方)
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
ベータ関数の積分表示
\begin{align}
B(x,y) &= \int_{0}^{1}t^{x-1}(1-t)^{y-1}dt \label{eq:betaxy}
\end{align}
(${\rm Re}\, x, {\rm Re}\, y \gt 0$)が
\begin{align}
B(x,y) &= \int_{0}^{\infty}\frac{t^{x-1}}{(1+t)^{x+y}}dt \label{eq:betatargetx} \cr
B(x,y) &= \int_{0}^{\infty}\frac{t^{y-1}}{(1+t)^{x+y}}dt \label{eq:betatargety}
\end{align}
と書けることを示したいと思います。

{% include firstad.html %}
## 最初にちょっと寄り道
最初に$B(x,y) = B(y,x)$であることを確認しておきます。

(\ref{eq:betaxy})式で$u = 1-t$とおくと、$t = 0$のとき$u = 1$で、$t = 1$のとき$u = 0$、さらに$du = -dt$となるため、

\begin{align}
B(x,y) &= \int_{1}^{0}(1-u)^{x-1}u^{y-1}(-du)\nonumber\cr
&= \int_{0}^{1}(1-u)^{x-1}u^{y-1}du\nonumber\cr
&= \int_{0}^{1}u^{y-1}(1-u)^{x-1}du \label{eq:betadu}
\end{align}
(\ref{eq:betadu})式の$u$は積分変数ですので、$t$と書き換えて、
\begin{align}
B(x,y) &= \int_{0}^{1}t^{y-1}(1-t)^{x-1}du\nonumber\cr
&= B(y,x) \label{eq:betayx}
\end{align}
であることがわかります。$\blacksquare$

{%include secondintervalad.html %}
## 本題
ここからが本題です。

\begin{align}
u &= \frac{1}{t}-1\label{eq:utott}
\end{align}
とおいて、(\ref{eq:betayx})式に代入します。


$t = 0$のとき$u = \infty$で、$t = 1$のとき$u = 0$、さらに、$du = -\displaystyle\frac{1}{t^2}dt$となり、$t = \displaystyle\frac{1}{1+u}$と表すことができます。

したがって、(\ref{eq:betayx})式は、

\begin{align}
B(x,y) &= \int_{\infty}^{0}\frac{1}{(1+u)^{y-1}}\cdot\left(\frac{u}{u+1}\right)^{x-1}\cdot\frac{-1}{(1+u)^2}du\nonumber\cr
&= \int_{0}^{\infty}\frac{u^{x-1}}{(1+u)^{y-1+x-1+2}}du\nonumber\cr
&= \int_{0}^{\infty}\frac{u^{x-1}}{(1+u)^{x+y}}du \label{eq:betauxy}
\end{align}

(\ref{eq:betauxy})式の$u$は積分変数ですので、これを$t$と書き換えて、

\begin{align}
B(x,y) &= \int_{0}^{\infty}\frac{t^{x-1}}{(1+t)^{x+y}}dt \label{eq:betatxy}
\end{align}

と表すことができますし、(\ref{eq:betayx})式より、

\begin{align}
B(x,y) &= \int_{0}^{\infty}\frac{t^{y-1}}{(1+t)^{x+y}}dt \label{eq:betatyx}
\end{align}

と表すこともできます。

(\ref{eq:betatxy})式と(\ref{eq:betatyx})式は(\ref{eq:betatargetx})式及び(\ref{eq:betatargety})式とそれぞれ一致します。$\blacksquare$

{%include thirdintervalad.html %}
## まとめ
どこかに載っていそうで載っていなかった変数変換だったので、メモ書きしておくことにしました。

何かのお役に立てば幸いです。

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
