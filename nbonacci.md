---
title: n-bonacci数列を出力するPython3のコードを書いてみた。- panda大学習帳外伝
description: n-bonacci数列を出力するPython3のコードを書いてみたところ、Python3のおさらいが捗った件。
image: https://pandanote.info/wordpress/wp-content/uploads/2020/04/P_20200416_185914_vHDR_On_HP-scaled.jpg
twitter:
  card: summary_large_image
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}
# n-bonacci数列を出力するPython3のコードを書いてみた。
## はじめに
突然ですが、みんな大好きフィボナッチ数列${a_n} (n \ge 1)$の漸化式は(\ref{eq:fibonacci})式で表すことができます。

\begin{align}
a_1 &= a_2 = 1,\quad a_{n+2} = a_{n+1} + a_n \label{eq:fibonacci}
\end{align}

(\ref{eq:fibonacci})式は3項間漸化式ですが、これにもう一項付け足して4項間漸化式とすると…

\begin{align}
a_1 &= a_2 = a_3 = 1,\quad a_{n+3} = a_{n+2} + a_{n+1} + a_n \label{eq:tribonacci}
\end{align}

という漸化式を考えることもできます。(\ref{eq:tribonacci})式で表される漸化式をトリボナッチ数列といいます。

それで、(\ref{eq:tribonacci})式をさらに一般化して…

\begin{align}
a_1 &= \cdots = a_n = 1,\quad a_{m+n} = \sum_{i=0}^{n-1} a_{m+i} \label{eq:nbonacci}
\end{align}

という$(n+1)$項間漸化式で定義される数列${a_n} (n \ge 1)$(nボナッチ数列)を考え、これを初項から指定した項までを計算するPython3のコードを書いてみました。

{% include firstad.html %}

## 仕様を考えます。
Python3のコードは以下の2つの引数を取ります。
* 第1引数: 次の項を求めるために必要な項の数。3項間漸化式であれば2となります。
* 第2引数: 計算の対象となる項の数。初項からの項数になります。
## コード例
以下のような感じのコードを書いてみました。

なお、コマンドライン引数の解釈についてはargparseなどのライブラリは使用せず、シンプルにまとめています。
<script src="https://gist.github.com/pandanote-info/8838de42bfe8cef428125cd810c452a1.js"></script>
## 実行例
Windows 10にインストールしたPython3で実行すると、以下のような感じの実行結果が出力されます。

第1引数を大きくすると、最初のいくつかの項についてはゆるやかに増加するものの、その後急激に増加することがわかります。
### 第1引数: 2, 第2引数: 10
```
C:\Users\Pandanote\Documents>python3 nbonacci.py 2 10
1
1
2
3
5
8
13
21
34
55
```
### 第1引数: 3, 第2引数: 10
```
C:\Users\Pandanote\Documents>python3 nbonacci.py 3 10
1
1
1
3
5
9
17
31
57
105
```
### 第1引数: 4, 第2引数: 15
```
C:\Users\Pandanote\Documents>python3 nbonacci.py 4 15
1
1
1
1
4
7
13
25
49
94
181
349
673
1297
2500
```
### 第1引数: 5, 第2引数: 30
$a_{30}$までのすべての項が奇数になってますね。
```
C:\Users\Pandanote\Documents>python3 nbonacci.py 5 30
1
1
1
1
1
5
9
17
33
65
129
253
497
977
1921
3777
7425
14597
28697
56417
110913
218049
428673
842749
1656801
3257185
6403457
12588865
24749057
48655365
```
### 第1引数: 0, 第2引数: 300
※エラーメッセージとして使い方を表示します。
```
C:\Users\Pandanote\Documents>python3 nbonacci.py 0 300
Usage: nbonacci.py <number of terms to compute the next term> <number of terms to calculate>
```

{%include secondintervalad.html %}

## まとめ
上記のnボナッチ数列のコードはシンプルで短いコードですが、Python3における配列の扱い方(初期化や要素の追加・削除)やif文の条件式の書き方、さらにはprint文の書き方といった基本的ではあるものの、他のプログラミング言語とは異なる書き方が必要になるポイントが凝縮されていて、面白いコードになっていると思います。

Python3のコードを何かのはずみで書かなければならなくなった時に参考にしていただけると幸いです。

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
