---
title: sec(x)とcosec(x)とcot(x)の不定積分を計算してみた。 - panda大学習帳外伝
description: sec(x),cosec(x),cot(x)が突如として登場しても慌てないようにするための心の備え的な記事という名の落書きです。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2023/10/P_20230924_161752-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Fri Jan  5 22:26:31 2024 +0900
---
{% include pagelink.md %}
# sec(x)とcosec(x)とcot(x)の不定積分を計算してみた。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
海外のYouTubeの動画を見ていると、

時々…

\begin{align}
I_1 &= \int \frac{dx}{\sin x} = \int\csc\, x\,dx\label{eq:intsinx} \cr
I_2 &= \int \frac{dx}{\cos x} = \int\sec\, x\,dx\label{eq:intcosx} \cr
I_3 &= \int \frac{dx}{\tan x} = \int\cot\, x\,dx\label{eq:inttanx}
\end{align}

のような式が登場するので、計算しておくことにします。

なお、この記事では積分定数を$C$とします。

また、cosecについては時々cscと書くことがありますが、気にしない方向でお願いいたします。

{% include firstad.html %}
## サクサク計算
### cosec(x),あるいはcsc(x)の不定積分
まず、(\ref{eq:intsinx})式を計算します。

\begin{align}
  I_1 &= \int\frac{\sin x}{(\sin x)^2}dx \nonumber\cr
  &= \int\frac{\sin x}{1-\cos^2 x}dx \label{eq:intinvsinxfirst}
\end{align}

ここで、$t=\cos x$とおくと、$\displaystyle\frac{dt}{dx} = -\sin x$となります。
そこで(\ref{eq:intinvsinxfirst})式に代入すると、

\begin{align}
  I_1 &= \int\frac{1}{1-t^2}\left(-\frac{dt}{dx}\right)dx \nonumber \cr
  &= \int\frac{1}{t^2-1}dt \nonumber \cr
  &= \int\frac{1}{2}\left(\frac{1}{t-1}-\frac{1}{t+1}\right)dt \nonumber \cr
  &= \frac{1}{2}(\log\left|t-1\right|-\log\left|t+1\right|)+C \nonumber \cr
  &= \frac{1}{2}\log\left|\frac{t-1}{t+1}\right|+C \nonumber \cr
  &= \frac{1}{2}\log\left|\frac{\cos x-1}{\cos x+1}\right|+C \label{eq:intinvsinxsecond}
\end{align}

$-1 \le \cos x \le 1$なので、$\cos x-1 \le 0$, $\cos x+1 \ge 0$であることに注意すると(\ref{eq:intinvsinxsecond})式の絶対値記号を外すことができて、

\begin{align}
I_1 &= \frac{1}{2}\log\left(\frac{1-\cos x}{1+\cos x}\right)+C \label{eq:intinvsinxthird}
\end{align}

と変形できます。$\blacksquare$

また、$\sin$及び$\cos$の半角の公式

\begin{align}
\sin^2\frac{x}{2} &= \frac{1-\cos x}{2} \label{eq:sinhalfangles} \cr
\cos^2\frac{x}{2} &= \frac{1+\cos x}{2} \label{eq:sinhalfangles} \cr
\end{align}

を利用すると、(\ref{eq:intinvsinxthird})式は

\begin{align}
I_1 &= \frac{1}{2}\log\left(\dfrac{\sin^2\frac{x}{2}}{\cos^2\frac{x}{2}}\right)+C \nonumber\cr
&= \frac{1}{2}\log\left(\tan^2\frac{x}{2}\right)+C \nonumber\cr
&= \log\left(\tan\frac{x}{2}\right)+C \label{eq:intinvsinxwithtangent}
\end{align}

と表すこともできます。
### sec(x)の不定積分
次に、(\ref{eq:intcosx})式を2通りの方法で計算します。
#### sec(x)を用いて表さないスタイル
$\sec$というのがなじみがない(※個人の感想です。)ので、いったん$\sec$を使わないで不定積分を求めてみます。

(\ref{eq:intcosx})式を以下のように変形します。

\begin{align}
  I_2 &= \int \frac{\cos x}{\cos^2 x}dx \nonumber \cr
  &= \int \frac{\cos x}{1-\sin^2 x}dx \label{eq:intinvcosfirst}
\end{align}

ここで、$t=\sin x$とおくと、$\displaystyle\frac{dt}{dx} = \cos x$となります。
そこで(\ref{eq:intinvsinxfirst})式に代入すると、

\begin{align}
I_2 &= \int\frac{1}{1-t^2}\left(\frac{dt}{dx}\right)dx \nonumber \cr
  &= \int\frac{dt}{1-t^2} \nonumber \cr
  &= \int\frac{1}{2}\left(\frac{1}{1-t}+\frac{1}{1+t}\right)dt \nonumber \cr
  &= \frac{1}{2}(-\log\left|1-t\right|+\log\left|1+t\right|)+C \nonumber \cr
  &= \frac{1}{2}\log\left|\frac{1+t}{1-t}\right|+C \nonumber \cr
  &= \frac{1}{2}\log\left|\frac{1+\sin x}{1-\sin x}\right|+C \label{eq:intinvcosxsecond}
\end{align}

$-1 \le \sin x \le 1$なので、$1-\sin x \ge 0$, $1+\sin x \ge 0$であることに注意すると、(\ref{eq:intinvcosxsecond})式の絶対値記号を外すことができて、

\begin{align}
I_2 &= \frac{1}{2}\log\left(\frac{1+\sin x}{1-\sin x}\right)+C \label{eq:intinvcosxthird}
\end{align}

と変形できます。

なお、(\ref{eq:intinvcosxthird})式は、

\begin{align}
I_2 &= \log\left(\frac{1+\sin x}{1-\sin x}\right)^{\frac{1}{2}}+C \label{eq:intinvcosxfourth}
\end{align}

と書くこともできます。$\blacksquare$

{%include thirdintervalad.html %}
#### sec(x)を積極的に使っていくスタイル
前節では$\sec$を使わないで不定積分を計算してみましたが、

\begin{align}
I_2 &= \int\sec x\,dx \label{eq:intsecfirst}
\end{align}

の表記を受け入れつつ、別の置換方法がないか考えてみることにします。

{\ref{eq:intsecfirst})式の右辺を…

\begin{align}
   I_2 &= \int\sec x \cdot\frac{\tan x + \sec x}{\tan x+ \sec x}\,dx \nonumber \cr
   &= \int\frac{\sec x\tan x + \sec^2 x}{\tan x+ \sec x}\,dx \label{eq:intsecsecond}
\end{align}

と変形し、

\begin{align}
u &= \tan x+\sec x\label{eq:ux}
\end{align}

と置きます。

すると、$\dfrac{d}{dx}\tan x = \dfrac{1}{\cos^2 x} = \sec^2 x$及び$\dfrac{d}{dx}\sec x = \dfrac{\sin x}{\cos^2 x} = \sec x\tan x$になるので、

\begin{align}
\frac{du}{dx} &= \sec^2 x + \sec x\tan x\label{eq:dudx}
\end{align}

と計算できます。

(\ref{eq:ux})式の右辺と(\ref{eq:dudx})式の右辺を(\ref{eq:intsecsecond})式に代入すると…

\begin{align}
  I_2 &= \int\frac{1}{u}\frac{du}{dx}\, dx\nonumber \cr
  &= \int\frac{1}{u}\, du\nonumber \cr
  &= \log|u|+C \nonumber\cr
  &= \log|\tan x+\sec x|+C \label{eq:intsecthird}
\end{align}

という解が求まります。$\blacksquare$
#### 検算
(\ref{eq:intinvcosxthird})式と(\ref{eq:intsecthird})式が同じ値を表す数式になっているとはにわかには信じがたい((\ref{eq:intsecthird})式については絶対値記号を外すことができるかどうかが式変形なしでは判断し難いです。)ですが…

\begin{align}
  \tan x+\sec x &= \frac{\sin x}{\cos x}+\frac{1}{\cos x} \nonumber\cr
  &= \frac{1+\sin x}{\cos x} \nonumber\cr
  &= \frac{1+\sin x}{\sqrt{1 - \sin^2 x}} \nonumber\cr
  &= \frac{1+\sin x}{\sqrt{(1+\sin x)(1-\sin x)}} \nonumber\cr
  &= \frac{\sqrt{1+\sin x}}{\sqrt{1-\sin x}} \nonumber\cr
  &= \left(\frac{1+\sin x}{1-\sin x}\right)^{\frac{1}{2}} \label{eq:tanxsecx}
\end{align}

と変形できるので、(\ref{eq:intsecthird})式及び(\ref{eq:tanxsecx})式を組み合わせると、(\ref{eq:intinvcosxfourth})式と一致することがわかります。$\blacksquare$
### cot(x)の不定積分
最後に(\ref{eq:intsinx})式を計算します。

\begin{align}
I_3 &= \int \frac{\sin x}{\cos x}\,dx \label{eq:intinvtanfirst}
\end{align}

であるので、$t = \cos x$とおくと、$\displaystyle\frac{dt}{dx} = -\sin x$になります。

したがって、

\begin{align}
  I_3 &= -\int \frac{1}{t}\frac{dt}{dx}\,dx \nonumber\cr
  &= -\int \frac{dt}{t} \nonumber\cr
  &= -\log|t|+C \nonumber\cr
  &= -\log|\cos x|+C \label{eq:intinvtansecond}
\end{align}

と計算できます。

比較的簡単な計算結果になります。$\blacksquare$

{%include secondintervalad.html %}
## まとめ
$\sec$, $\csc$, $\cot$は海外の文献や数学方面の動画を見ていると容赦なく登場しますので、本記事で示した積分計算などを通して慣れておくと良いかもしれません。

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
