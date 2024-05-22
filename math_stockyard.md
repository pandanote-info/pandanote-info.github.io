---
title: The Math Stockyard / 数式置き場 - panda大学習帳外伝
description: panda大学習帳のトップページで使っていた数式を保管しています。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2024/04/P_20240420_142526-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Wed May 22 13:23:00 2024 +0900
---
{% include pagelink.md %}
# The Math Stockyard / 数式置き場
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに

$\LaTeX$の数式は書き始めると楽しいのですが、それなりに手間がかかります。

したがって、適当に書いたものでもどこかに保存しておきたくなったりします(※個人の感想です)。

そこで、数式置き場のページを作ることにしました。

{% include firstad.html %}

## panda大学習帳のトップページで使っていた数式

[panda大学習帳のトップページ](https://pandanote.info/)の数式の記載例として使っていたものです。

\begin{align}
I &= \displaystyle\frac{1}{2} \int^2_1 \frac{1}{x^{n+\frac{1}{2}}}\cdot\sum^n_{k=0}\begin{pmatrix}
n \cr
k
\end{pmatrix}x^k(-1)^{n-k}dx \nonumber \cr
&= \displaystyle\frac{1}{2} \int^2_1 \sum^n_{k=0}\begin{pmatrix}
n \cr
k
\end{pmatrix}x^{k-n-\frac{1}{2}}(-1)^{n-k}dx \nonumber \cr
&= \displaystyle\frac{1}{2} \left[ \sum^n_{k=0}\begin{pmatrix}
n \cr
k
\end{pmatrix}\frac{x^{k-n+\frac{1}{2}}}{k-n+\displaystyle\frac{1}{2}}(-1)^{n-k} \right]^2_1 \label{eq:utqione} \\
&= \displaystyle\frac{1}{2} \sum^n_{k=0}\begin{pmatrix}
n \cr
k
\end{pmatrix}\frac{(-1)^{n-k}}{k-n+\displaystyle\frac{1}{2}}(2^{k-n+\frac{1}{2}}-1) \label{eq:utqitwo}
\end{align}

{%include secondintervalad.html %}

## まとめ

このページの記載内容が増加するペースは極めてゆっくりとしたものになりそうですが、適宜書いていきます。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
