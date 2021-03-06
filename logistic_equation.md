---
title: ロジスティック方程式のような微分方程式を解いてみた。 - panda大学習帳外伝
description: ロジスティック方程式のような微分方程式を解いてみたら、計算途中の式変形の方法の相違により2通りの異なる形式の解が求まった件。
image: https://pandanote.info/wordpress/wp-content/uploads/2020/02/logisitic_equation_solution.png
twitter:
  card: summary_large_image
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}
# ロジスティック方程式のような微分方程式を解いてみた。
## はじめに
ロジスティック方程式でよく見かけるタイプの微分方程式
\begin{align}
  \frac{dx}{dt} &= \alpha x - \beta x^2 \label{eq:logistic}
\end{align}
($\alpha,\beta > 0$) を解いてみることにします。

{% include firstad.html %}
## とりあえず、サクサク解きます。
(\ref{eq:logistic})式の右辺をちょっと変形して、$x$と$\beta$を括り出すと…
\begin{align}
  \frac{dx}{dt} &= \beta \left(\frac{\alpha}{\beta}-x\right)x \label{eq:logisticsecond}
\end{align}
として、(\ref{eq:logisticsecond})式の両辺を$\left(x- \dfrac{\alpha}{\beta}\right)x$で割ると、右辺が$-\beta$になることに注意しつつ…
\begin{align}
  \frac{1}{\left(x-\dfrac{\alpha}{\beta}\right)x}\frac{dx}{dt} &= -\beta \label{eq:logisticsthird}
\end{align}
と変形できます。

次に、任意の$x \in \mathbb{R}$について、
\begin{align}
  \frac{a}{x-\dfrac{\alpha}{\beta}} + \frac{b}{x} &= \frac{1}{\left(x - \dfrac{\alpha}{\beta}\right)x} \label{eq:identity}
\end{align}
を満たす$a,b$を求めてみます。(\ref{eq:identity})式の両辺に$\left(x-\dfrac{\alpha}{\beta}\right)x$をかけると…
\begin{align}
  ax + b\left(x-\frac{\alpha}{\beta}\right) &= 1 \label{eq:identitysecond}
\end{align}
さらに$x$について整理して…
\begin{align}
  (a+b)x - b \frac{\alpha}{\beta} &= 1 \label{eq:identitythird}
\end{align}
となります。

任意の$x \in \mathbb{R}$について(\ref{eq:identity})式を成立させるためには、$a = -b, -b \dfrac{\alpha}{\beta}-1 = 0$でなければならないので、
\begin{align}
  b &= -\frac{\beta}{\alpha} \label{eq:idb} \cr
  a &= -b = \frac{\beta}{\alpha} \label{eq:ida}
\end{align}
になります。(\ref{eq:idb}),(\ref{eq:ida})式を(\ref{eq:logisticsthird})式に代入すると…
\begin{align}
  \left( \frac{\beta}{\alpha}\cdot\frac{1}{x-\dfrac{\alpha}{\beta}} - \frac{\beta}{\alpha}\cdot\frac{1}{x}\right)\frac{dx}{dt} &= -\beta \label{eq:logisticsfourth}
\end{align}
(\ref{eq:logisticsfourth})式の両辺に$\dfrac{\alpha}{\beta}$をかけると…
\begin{align}
  \left( \frac{1}{x-\dfrac{\alpha}{\beta}} - \frac{1}{x}\right)\frac{dx}{dt} &= -\alpha \label{eq:logisticsfifth}
\end{align}
(\ref{eq:logisticsfifth})式の両辺の不定積分を取ると…
\begin{align}
  \log\left|x-\dfrac{\alpha}{\beta}\right| - \log|x| &= -\alpha t + C \label{eq:logisitcsint}
\end{align}
($C$は積分定数)となりますが、左辺をちょいと整理して、
\begin{align}
  \log\left|1-\dfrac{\alpha}{\beta x}\right| &= -\alpha t + C \label{eq:logisticsintsecond}
\end{align}
(\ref{eq:logisticsintsecond})式の自然対数を取りつつ絶対値記号を外し、$\pm e^C$を新たな定数$C$と置きなおすと…
\begin{align}
  1 - \dfrac{\alpha}{\beta x} &= \pm e^{-\alpha t+C} \nonumber \cr
  &= Ce^{-\alpha t} \label{eq:solutionzero}
\end{align}
(\ref{eq:solutionzero})式を$x$について解くと…
\begin{align}
  x &= \frac{\alpha}{\beta}\cdot\frac{1}{1-Ce^{-\alpha t}} \label{eq:solution}
\end{align}
となります。$\blacksquare$

{%include secondintervalad.html %}
## よく見かける式への変形。
(\ref{eq:logistic})式で$\alpha = r, \beta = \dfrac{r}{K}$と置くとWikipediaとかに載っているロジスティック方程式になります。

(\ref{eq:solution})式に$\alpha = r, \beta = \dfrac{r}{K}$を代入し、本節に限り$x$を($x$が$t$の関数であることを明確にするために)$x(t)$と書くことにすると…
\begin{align}
x(t) &= r\cdot\frac{K}{r}\cdot\frac{1}{1-Ce^{-rt}} \nonumber \cr
&= K\cdot\frac{1}{1-Ce^{-rt}} \label{eq:xtc}
\end{align}
となります。

ここで、$t=t_0$のときに$x(t_0)=N_0$であるとすると…
\begin{align}
x(t_0) &= K\cdot\frac{1}{1-Ce^{-rt_0}} \nonumber \cr
&= N_0 \label{eq:xtcinitial}
\end{align}
となります。(\ref{eq:xtcinitial})式は$C$について解くことができて…
\begin{align}
C &= \left(1-\dfrac{K}{N_0}\right)e^{rt_0} \label{eq:Cattzero}
\end{align}
となります。

(\ref{eq:Cattzero})式を(\ref{eq:xtc})式に代入して、ちょっと整理すると…
\begin{align}
x(t) &= \frac{K}{1-\left(1-\dfrac{K}{N_0}\right)e^{-r(t-t_0)}} \nonumber \cr
&= \frac{K}{1+\left(\dfrac{K}{N_0}-1\right)e^{-r(t-t_0)}} \label{eq:solutionone}
\end{align}
となります。

(\ref{eq:solutionone})式に$t_0=0$を代入するとWikipediaに記述されている式になります。
## 別解。
なお、(\ref{eq:logisticsecond})式の両辺を$\left(\dfrac{\alpha}{\beta}-x\right)x$で割ると…
\begin{align}
  \frac{1}{\left(\dfrac{\alpha}{\beta}-x\right)x}\frac{dx}{dt} &= \beta \label{eq:yetanother}
\end{align}
と変形できます。すると(途中の計算は省略しますが…)、
\begin{align}
  \frac{1}{\left(\dfrac{\alpha}{\beta}-x\right)x}\frac{dx}{dt} &= \frac{\beta}{\alpha}\left( \dfrac{1}{\dfrac{\alpha}{\beta}-x} + \frac{1}{x}\right) \label{eq:yetanothersecond}
\end{align}
となりますので、(\ref{eq:yetanothersecond})式を(\ref{eq:yetanother})式に代入して両辺に$\dfrac{\alpha}{\beta}$をかけると…
\begin{align}
  \left( \frac{1}{\dfrac{\alpha}{\beta}-x}+\frac{1}{x}\right)\frac{dx}{dt} &= \alpha \label{eq:yetanotherthird}
\end{align}
(\ref{eq:yetanotherthird})式の両辺を積分すると、積分定数を$C$として、
\begin{align}
  \log\left| x \right| - \log\left| \frac{\alpha}{\beta}-x \right| &= \alpha t + C \label{eq:yetanotherfourth}
\end{align}
両辺の自然対数を取りつつ絶対値記号を外し、$\pm e^C$を$C$と置きなおして、
\begin{align}
  \dfrac{x}{\dfrac{\alpha}{\beta}-x} &= Ce^{\alpha t} \label{eq:yetanotherfifth}
\end{align}
(\ref{eq:yetanotherfifth})式を$x$について解くと…
\begin{align}
x &= \frac{\alpha}{\beta}\cdot\frac{Ce^{\alpha t}}{1+Ce^{\alpha t}} \label{eq:yetanothersolution} 
\end{align}
となります。

(\ref{eq:yetanothersolution})式と(\ref{eq:solution})式は一見異なる式のように見えますが、(\ref{eq:yetanothersolution})式の右辺の分子と分母を$Ce^{\alpha t}$で割ると…
\begin{align}
  x &= \frac{\alpha}{\beta}\cdot\dfrac{1}{\dfrac{1}{C}e^{-\alpha t}+1} \label{eq:yetanothersolutionsecond}
\end{align}
と変形できます。

(\ref{eq:yetanothersolutionsecond})式と(\ref{eq:solution})式はまだ相違があるようにも見えますが、(\ref{eq:yetanothersolutionsecond})式の$t$は$C$に依存しない定数であるので、$-\dfrac{1}{C}$を$C$と置き直すことで(\ref{eq:solution})式と形式的に一致させることができます。$\blacksquare$

{%include thirdintervalad.html %}
## まとめ
積分定数のとり方で一見違った形式の解になりますが、同じ解を表していることが確認できました。

初期条件を与えると同じ式になると思います(たぶん)。&#x1F60E;

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
