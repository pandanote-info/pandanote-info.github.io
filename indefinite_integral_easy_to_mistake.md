---
title: 符号を間違えたまま計算しがちな不定積分 - panda大学習帳外伝
description: マイナス符号は特に見逃しがちですよね…。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2023/05/P_20230527_203350-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sat Jul 22 22:36:12 2023 +0900
---
{% include pagelink.md %}
# 符号を間違えたまま計算しがちな不定積分
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
先日、微分方程式を解いている動画を見ながら計算をしていた時に、なんかものすごい勢いで計算を間違えたので、初心に帰って復習です。

{% include firstad.html %}

## 問題の不定積分
### 式です。
問題の不定積分は以下の式です。

\begin{align}
I &= \int \frac{x}{\sqrt{1-x^2}}\,dx \label{eq:integral_firstform}
\end{align}

なお、もとの動画内で登場した式より簡単な形としています。

{%include secondintervalad.html %}

### 解きます。

$t=1-x^2$とおくと、$x = \sqrt{1-t}$と表すことができるので、$t$の係数が$-1$であることに注意しつつ両辺を微分すると…

\begin{align}
\frac{dx}{dt} &= \left(-\frac{1}{2}\right)\frac{1}{\sqrt{1-t}}\label{eq:integral_secondform}
\end{align}

となります。

そこで、(\ref{eq:integral_secondform})式を利用して(\ref{eq:integral_firstform})式を変形すると、

\begin{align}
I &= \int \frac{\sqrt{1-t}}{\sqrt{t}}\frac{dx}{dt}\,dt \nonumber\cr
&= \int \frac{\sqrt{1-t}}{\sqrt{t}}\left(-\frac{1}{2}\right)\frac{1}{\sqrt{1-t}}\,dt \nonumber\cr
&= -\frac{1}{2}\int\frac{dt}{\sqrt{t}} \nonumber\cr
&= -\frac{1}{2}\left(2\sqrt{t}\right) + C \label{eq:integral_thirdform}
\end{align}

と計算できます(符号を忘れがちです)。

$t=1-x^2$とおいたことを思い出すと…

\begin{align}
I &= -\sqrt{1-x^2} + C \label{eq:integral_fourthform}
\end{align}

となることがわかります($C$は積分定数)。$\blacksquare$
## 確認です。
次に、(\ref{eq:integral_fourthform})式を微分します。

すると…

\begin{align}
\left(-\sqrt{1-x^2}+C\right)^{\prime} &= (-)\left(\frac{1}{2}\right)\frac{(1-x^2)^{\prime}}{\sqrt{(1-x^2)}} \nonumber\cr
&= \left(-\frac{1}{2}\right)\frac{-2x}{\sqrt{(1-x^2)}}\nonumber\cr
&= \frac{x}{\sqrt{(1-x^2)}} \label{eq:differential_firstform}
\end{align}

と計算できて、(\ref{eq:integral_firstform})式の被積分関数と一致します。$\blacksquare$

マイナスの符号を忘れがちですね。
## まとめ
不定積分の計算及び微分計算の両方でマイナス符号が大量に登場する計算は注意して計算したいですね。

$\LaTeX$で書きながら計算をすると意外に間違えなかったりするので、数式は普段から走り書きで書いたりしないで、少し時間がかかっても良いので綺麗に書くべきであるという今更感満載の気づきを得た次第です。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
