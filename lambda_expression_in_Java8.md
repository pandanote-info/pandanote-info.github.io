---
title: Java8のラムダ式を使って配列の配列の要素数の総和を1行で求める。 - panda大学習帳外伝
description: ラムダ式を使うとコードが簡潔に書けるようになった件について書きました。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2021/05/P_20210522_190348_vHDR_On_HP-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sun May 23 13:46:53 2021 +0900
---
{% include pagelink.md %}
# Java8のラムダ式を使って配列の配列の要素数の総和を1行で求める。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
読み込んだデータの処理のための紐づけを行うためにMapを多用しているかなりレガシーなJavaのプログラムに、さらにMapを追加するプログラムを追加することになったので、ちょっと前にScalaで使ってみたラムダ式をJava8でも使ってみることにしました。

この記事では特にその中でもコードが簡潔になったと思う処理について書きます。

{% include firstad.html %}
## 課題
書くべきコードは以下のようなものです。

> 整数をキー、Setを値とするMapについて、値に含まれるSetの要素数をキーごとに求め、さらにその総和を求める。
> ただし、同様の処理を行うコードを大量に繰り返し記述することを想定し、コードの記述は自然な方法で記述し、かつ簡潔なものとしたい。

### レガシーなコード
まず、ラムダ式を使わずに書いてみます。
```
public static void test1(Map<Integer,Set<Integer>> a) {
	int count = 0;
	for (Entry<Integer,Set<Integer>> e: a.entrySet()) {
		count += e.getValue().size();
	}
	System.out.println(count);
	return;		
}
```
カウントの途中結果を格納するための変数を用意しなければならなかったり、途中で処理の最終結果にはあまり関係なさそうな型(Entry)が登場するのがちょっと気になるところです。
### ラムダ式を使ったコード
次にラムダ式を使って書いてみます。
```
public static void test2(Map<Integer,Set<Integer>> a) {
	System.out.println(a.entrySet().stream().mapToInt(e -> e.getValue().size()).sum());
}
```
mapToInt()メソッドを適用することで配列ごとの要素数を要素として持つ配列へのstream(IntStream)を返しますので、sum()メソッドを実行してそれらの総和を計算しています。

ラムダ式を用いて記述すると自然な記述方法で1行で書けます。

streamメソッドは直感的かとか流れるインタフェースかとかいわれると微妙なところはありますが、少なくともメソッドチェーンの形成には一役買っていると思います。

また、mapToIntというラムダ式を使わない限りはおそらく使うことがないであろうメソッドが登場しますが、このメソッドを知っていれば上記の通り簡潔に書けます。

型を意識しなくて良いというのは、かなり強力です。
## 動作確認
ここまでのコードはメソッド単位での記述でしたが、これらのメソッドをクラスメソッドして実行できる形に記述したもの(↓)を用意して実行してみます。

<script src="https://gist.github.com/pandanote-info/937d799a64e7a2efd125e0b815f15968.js"></script>

実行した結果は以下の通りになります。

```
13
13
```

計算結果が一致していることが確認できました。

{%include secondintervalad.html %}
## 考察
追加の対象となるMapが1ヵ所だけだと、「何だそんなもんか。」と思われるところかもしれませんが、例えばMapに格納されたデータ全体を使った処理で追加の対象となるものが100ヵ所近くあったりすると、この手のリファクタリングが地味に効いてきます。

ラムダ式を使うことによって、一時変数名を決めたり、Entryのような冗長な記述のために時間を割く必要がなくなり、出来上がったコードの可読性を向上させることができます。

{%include thirdintervalad.html %}
## まとめ
mapToIntメソッド及びsumメソッドが存在することを忘れないようにするためのメモ書き的な記事になっていますが、とりあえず書いてみました。

ラムダ式を使わなくても何となくコードが書けてしまうので、「プログラムが動いているかどうか」にのみ興味がある人に対してその良さを説明するのは難しい面はあるかと思いますが、コードを作ったりメンテナンスする人にとっては可読性は大事だと考えていますので、隙あらば使っていきたいと考えています。

この記事は以上です。
## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
