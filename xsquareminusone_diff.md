---
title: panda大学習帳外伝
description: (x^2-1)^nをl回微分してみた。
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}
# はじめに
さっそく微分していきます。
# とりあえず、1,2回微分してみる。
\begin{align}
\frac{d}{dx}\left[(x^2-1)^n\right] &= \sum_{k=1}^{n}\begin{pmatrix}
    n \cr
    k
\end{pmatrix} (-1)^{n-k}2k\cdot x^{2k-1} \cr
\frac{d^2}{dx^2}\left[(x^2-1)^n\right] &= \sum_{k=1}^{n}\begin{pmatrix}
    n \cr
    k
\end{pmatrix} (-1)^{n-k}2k\cdot (2k-1) \cdot x^{2k-2}
\end{align}
となります。
# それで、$l$回微分するとどうなるの?
こうなりそうです。
\begin{align}
  \frac{d^l}{dx^l}\left[(x^2-1)^n\right] &= \sum_{k=\left\lceil\frac{l}{2}\right\rceil}^{n}\begin{pmatrix}
    n \cr
    k
    \end{pmatrix} (-1)^{n-k}x^{2k-l}\prod_{p=2k-l+1}^{2k}p
\end{align}
となりそうである。
# それで、どういう性質があるの?
(3)式は残念ながらこれ以上は簡単な形になりそうにないので、

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
