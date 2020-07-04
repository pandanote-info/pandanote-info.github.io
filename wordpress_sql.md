---
title: Wordpressの記事データを操作するときによく使うかもしれないSQL文n選。 - panda大学習帳外伝
description: Wordpressの過去の記事データに含まれる特定の文字列等を一斉に変換したくなったとき等に確実に使えるようにしたいSQL文のメモ書きです。
image: https://pandanote.info/wordpress/wp-content/uploads/2019/12/P_20191224_202329_vHDR_On_HP_a.jpg
twitter:
  card: summary_large_image
encoding: UTF-8
mathjax: true
---
{% include pagelink.md %}

# Wordpressのデータを操作するときによく使うかもしれないSQL文n選。

## 前置き

WordpressはRDBMS(通常はMariaDBかMySQL)に記事のデータを格納していますが、HTMLのタグやショートコードのタグを書くことができます。

しかし、[この記事](https://pandanote.info/?p=5463)で書いたような事態が発生して、HTMLやショートコードのうちの特定のタグを別のタグに書き換える必要が生じた場合に、Wordpressのエディタを開いてコードを修正するのでは手間がかかります。

そこで、この記事では上記のケースに限定せずに、Wordpressの記事データを操作するときによく使うかもしれないので、知っていると便利なSQL文(の断片)をメモ書きします。

### ここで、注意書き。

なお、Wordpressが使用しているデータベースを直接操作しますので、誤ったSQL文を実行することによりデータベースの中身を失う可能性がないとは言えません。そこで、作業を始める前にデータベースのバックアップを取得されることをお勧めいたします。

{% include firstad.html %}

## 特定の文字列を含むWordpressの記事を探し、そのIDを返す。

Wordpressで公開中の記事の中から特定の文字列(以下の例では"panda大学習帳")を含む記事のIDを得るためには以下のSQL文を実行します。

```
select ID from wp_posts where post_status='publish' and post_content like '%panda大学習帳%' and post_type in ('page','post');
```

公開中の記事に対応するwp_postsテーブルのレコードではpost_statusカラムの値が'publish'になることを利用しています。また、投稿タイプは公開中の記事(に対応すると思われる)固定ページ('page')及び投稿('post')に限定しています。

## 特定の文字列を別の文字列に置き換える。

MariaDBではregexp_replace関数が使えますので、update文と組み合わせて使用します([この記事](https://pandanote.info/?p=3510)参照)。

{% include thirdintervalad.html %}

## まとめ

この記事を最初に書いた時点では$n = 1+\varepsilon$的な書きかけ感満載の記事になっていますが、徐々に書き足していきます。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
