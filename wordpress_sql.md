---
title: WordPressの記事データを操作するときによく使うかもしれないSQL文n選。 - panda大学習帳外伝
description: WordPressの過去の記事データに含まれる特定の文字列等を一斉に変換したくなったとき等に確実に使えるようにしたいSQL文のメモ書きです。
image: https://pandanote.info/wordpress/wp-content/uploads/2019/12/P_20191224_202329_vHDR_On_HP_a.jpg
twitter:
  card: summary_large_image
encoding: UTF-8
mathjax: true
update: Sun Jun 18 14:45:10 2023 +0900
---
{% include pagelink.md %}

# WordPressのデータを操作するときによく使うかもしれないSQL文n選。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## 前置き

WordPressはRDBMS(通常はMariaDBかMySQL)に記事のデータを格納していますが、HTMLのタグやショートコードのタグを書くことができます。

しかし、[この記事](https://pandanote.info/?p=5463)で書いたような事態が発生して、HTMLやショートコードのうちの特定のタグを別のタグに書き換える必要が生じた場合に、WordPressのエディタを開いてコードを修正するのでは手間がかかります。

そこで、この記事では上記のケースに限定せずに、WordPressの記事データを操作するときによく使うかもしれないので、知っていると便利なSQL文(の断片)をメモ書きします。

### ここで、注意書き。

1. このページの情報はWordPress 5.6に対応した情報です。5.6以外のバージョンの場合にはデータベースの構造が異なる場合があります。
1. WordPressが使用しているデータベースを直接操作しますので、誤ったSQL文を実行することによりデータベースの中身を失う可能性がないとは言えません。そこで、作業を始める前にデータベースのバックアップを取得されることをお勧めいたします。

{% include firstad.html %}

## 特定の文字列を含むWordPressの記事を探し、そのIDを返す。

WordPressで公開中の記事の中から特定の文字列(以下の例では"panda大学習帳")を含む記事のIDを得るためには以下のSQL文を実行します。

```SQL
select ID from wp_posts where post_status='publish' and post_content like '%panda大学習帳%' and post_type in ('page','post');
```

公開中の記事に対応するwp_postsテーブルのレコードではpost_statusカラムの値が'publish'になることを利用しています。また、投稿タイプは公開中の記事(に対応すると思われる)固定ページ('page')及び投稿('post')に限定しています。

## 公開されているWordPressの記事の中でIDが最大のものを返す。

WordPressで公開中の記事の中からIDが最大のものを得るには、以下のSQL文を実行します。

```SQL
select ID from wp_posts where post_status='publish' and post_type in ('page','post');
```

「IDが最大の記事」=「最も最近に公開された記事」とは必ずしも言えないのですが、書きかけの記事が最大で1個しか存在させないというポリシーで記事を作成している状況下などにおいては使えるSQL文だと思います。

## 特定の文字列を別の文字列に置き換える。

MariaDBではregexp_replace関数が使えますので、update文と組み合わせて使用します([この記事](https://pandanote.info/?p=3510)参照)。

なお、regexp_replace関数に絵文字等のutf8mb4に指定した場合にのみサポートされる文字の部分が(変換の対象とならない場合でも)"?"に変換されてしまう問題があるので、絵文字等を本文中で使用する場合には数値文字参照を使用した方が良いでしょう([この記事](https://pandanote.info/?p=1023)も参照)。

{% include secondintervalad.html %}

## プラグインの設定用データを検索する。

WordPressのプラグインで設定用のデータをデータベースに保管する場合には、wp_postmetaテーブルを使用することが一般的なようです。

wp_postmetaテーブルのテーブル構造は以下の通りです。

| Field      | Type                | Null | Key | Default | Extra          | 
|------------|---------------------|------|-----|---------|----------------|
| meta_id    | bigint(20) unsigned | NO   | PRI | NULL    | auto_increment |
| post_id    | bigint(20) unsigned | NO   | MUL | 0       |                |
| meta_key   | varchar(255)        | YES  | MUL | NULL    |                |
| meta_value | longtext            | YES  |     | NULL    |                |

よって、wp_postmetaテーブルのレコードは以下のSQL文で取得できます。

```SQL
select meta_id,post_id,meta_key,meta_value from wp_postmeta;
```

## Python3+mysql-connector-pythonでプリペアードステートメントを使用する際のおまじない

WordPressが使用しているMariaDBのデータベース(でかつ文字コードがutf8mb4のもの。)にアクセスするためにPython3のコードを書くことを考えます。

なお、データベースへの接続用のドライバとしてmysql-connector-pythonを使用します。

### 動作しない例

この時、データベースの文字コードがutf8mb4になっているということで、以下のコード片のように記述しても動きません。

```Python
import mysql.connector

dbconfig = ... # データベース接続用の情報の設定

conn = mysql.connector.connect(user=dbconfig["db_user"],password=dbconfig["db_password"],host=dbconfig["host"],database=dbconfig["db_name"],charset="utf8mb4")

cur = conn.cursor(prepared=True)

stmt = "select * from hogehoge where id=?"
cur.execute(stmt,(1,))
```

### 動作する例

とりあえず、以下のように記述すると動作します。SET NAMESを使って文字コード及びCollationを設定しています。

```Python
import mysql.connector

dbconfig = ... # データベース接続用の情報の設定

conn = mysql.connector.connect(user=dbconfig["db_user"],password=dbconfig["db_password"],host=dbconfig["host"],database=dbconfig["db_name"])

cur = conn.cursor(prepared=True)
cur.execute("SET NAMES 'utf8mb4' collate 'utf8mb4_general_ci'");

stmt = "select * from hogehoge where id=?"
cur.execute(stmt,(1,))
```

Collationについては(文字の照合順は異なりますが)、utf8mb4_unicode_ci等も指定できるようです。

{% include thirdintervalad.html %}

## まとめ

この記事を最初に書いた時点では$n = 1+\varepsilon$的な書きかけ感満載の記事になっていましたが、徐々に書き足していきます。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
