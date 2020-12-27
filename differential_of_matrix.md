---
title: ちょっと気になる行列の微分の公式 - panda大学習帳外伝
description: 
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2020/12/P_20201217_134242_vHDR_On_HP-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sun Dec 27 10:37:12 2020 +0900
---
{% include pagelink.md %}
# ちょっと気になる行列の微分の公式
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
機械学習の本や論文を読んでいると時々登場するかもしれない行列の微分ですが、多変数(かつ多出力)の線形回帰分析を行う際に登場する、
\begin{align}
\frac{\partial \\| XW - Y \\|^2_F}{\partial W} &= 2X^T (XW-Y) \label{eq:frobeniusnorm}
\end{align}
($X \in \mathbb{R}^{n_1\times n_2}, W \in \mathbb{R}^{n_2\times n_3}, Y \in \mathbb{R}^{n_1\times n_3}, n_1,n_2,n_3 \in \mathbb{N},\\|\cdot\\|_F$は$\cdot$のフロベニウスノルムを表します。)の導出方法が気になったので、成分ごとに書き下して計算してみることにします。

{% include firstad.html %}

## サクサク計算します。
### 成分ごとに書き下します。
最初に$XW-Y=U (U \in \mathbb{R}^{n_1\times n_3})$とおいて、$U$の$i,j$成分$u_{ij}$を計算してみます。

すると…
\begin{align}
u_{ij} &= \sum_{k=1}^{n_2} x_{ik}w_{kj} - y_{ij} \label{eq:ufirst}
\end{align}
となります。

したがって、$U_F^2$は(\ref{eq:ufirst})式を用いて、
\begin{align}
\\| XW-Y \\|_F^2 &= \sum_{i=1}^{n_1}\sum_{j=1}^{n_3}\left(\sum_{k=1}^{n_2} x_{ik}w_{kj} - y_{ij}\right)^2 \label{eq:usecond}
\end{align}
と書くことができます。

{%include secondintervalad.html %}

### 行列の成分ごとに微分します。
次に、行列$W$の成分ごとに微分していきますが、前節まででsuffixを使いまくっているので、$W$の成分を(自然数っぽい感じではないですが、)$w_{\alpha\beta} (\alpha, \beta \in \mathbb{N})$で表すことにします。

すると…
\begin{align}
  \frac{\partial \\| XW - Y \\|^2_F}{\partial w_{\alpha\beta}} &= \frac{\partial}{\partial w_{\alpha\beta}} \left[ \sum_{i=1}^{n_1}\sum_{j=1}^{n_3}\left(\sum_{k=1}^{n_2} x_{ik}w_{kj} - y_{ij}\right)^2 \right] \label{eq:frobeniusnormsecond}
\end{align}
となります。ここで、(\ref{eq:frobeniusnormsecond})式右辺のsummationのうち、2番目のものについては$j=\beta$の場合のみ$w_{\alpha\beta}$を含む項が存在し、かつそれらの項は$w_{\alpha\beta}$で偏微分しても0になりません。

したがって、(\ref{eq:frobeniusnormsecond})式の右辺は、
\begin{align}
\frac{\partial \\| XW - Y \\|^2_F}{\partial w_{\alpha\beta}} &= \frac{\partial}{\partial w_{\alpha\beta}} \left[ \sum_{i=1}^{n_1}\left(\sum_{k=1}^{n_2} x_{ik}w_{k\beta} - y_{i\beta}\right)^2 \right] \label{eq:frobeniusnormthird}
\end{align}
と書き換えることができます。

ここで、(\ref{eq:frobeniusnormthird})式右辺の括弧内に(\ref{eq:ufirst})式を用いて$w_{\alpha\beta}$で偏微分すると…
\begin{align}
  \frac{\partial u_{i\beta}}{\partial w_{\alpha\beta}}\,\cdot\,\frac{\partial}{\partial u_{i\beta}}u_{i\beta}^2 &= x_{i\alpha}\,\cdot\,2u_{i\beta} \nonumber \\
  &= 2x_{i\alpha}\left(\sum_{k=1}^{n_2} x_{ik}w_{k\beta} - y_{i\beta}\right) \label{eq:frobeniusnormfourth}
\end{align}
(\ref{eq:frobeniusnormfourth})式を使って(\ref{eq:frobeniusnormthird})式を書き換えると…
\begin{align}
  \frac{\partial \| XW - Y \|^2_F}{\partial w_{\alpha\beta}} &= 2\sum_{i=1}^{n_1}x_{i\alpha}\left(\sum_{k=1}^{n_2} x_{ik}w_{k\beta} - y_{i\beta}\right) \label{eq:frobeniusnormfifth}
\end{align}
$x_{i\alpha}$は$X$の$(i,\alpha)$成分を表しますが、$X$の転置行列$X^T$及びその$(\alpha,i)$成分である$x_{\alpha i}^T$を考えると、$x_{i\alpha} = x_{\alpha i}^T$が成り立ちます。

よって、
\begin{align}
  \frac{\partial \\| XW - Y \\|^2_F}{\partial w_{\alpha\beta}} &= 2\sum_{i=1}^{n_1}x_{\alpha i}^T\left(\sum_{k=1}^{n_2} x_{ik}w_{k\beta} - y_{i\beta}\right) \label{eq:frobeniusnormfinal}
\end{align}
と表すことができます。(\ref{eq:frobeniusnormfinal})式の右辺は行列$X^T(XW-Y)$の$(\alpha,\beta)$成分を表しますので、(\ref{eq:frobeniusnorm})式が成り立つことがわかります。$\blacksquare$

{%include thirdintervalad.html %}

## まとめ
$W$は重みづけ関数、$X$は変数、$Y$は出力の意味合いでそれぞれ使用されることが多いようです。

また、$X$を$n_2$の横ベクトル(入力ベクトル)を$n_1$個積み重ねたものと考えると、(\ref{eq:frobeniusnorm})式において、
\begin{align}
\frac{1}{n_1}\\|XW-Y\\|_F^2 &= L(W) \label{eq:lossfunction}
\end{align}
とおくと、$L(W)$は損失関数そのものを表していたりします。

したがって、$L(W)=0$とおくと(詳細は触れませんが、)$W$が求まったりします。

ただ、これらの式を丸暗記というのはあまり筋の良いやり方ではないような気もするので、要素ごとの計算ができるようになっておいた方が良さそうです。

この記事は以上です。

{%include fifthintervalad.html %}

## 参考文献
1. [Ordinary Least Squares Linear Regression](https://www.cs.princeton.edu/courses/archive/fall18/cos324/files/linear-regression.pdf)
1. [「ベクトルで微分・行列で微分」公式まとめ](https://qiita.com/AnchorBlues/items/8fe2483a3a72676eb96d)
1. [Derivative of squared Frobenius norm of a matrix](https://math.stackexchange.com/questions/2128462/derivative-of-squared-frobenius-norm-of-a-matrix)

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
