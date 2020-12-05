---
title: MariaDBで文字コードの設定が原因で"Foreign key constraint is incorrectly formed"と言われてしまった話。 - panda大学習帳外伝
description: 
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2020/12/P_20201130_123127_vHDR_On_HP-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Sat Dec  5 09:29:36 2020 +0900
---
{% include pagelink.md %}
# MariaDBで文字コードの設定が原因で"Foreign key constraint is incorrectly formed"と言われてしまった話。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
MariaDB 10.4.14でテーブルを後付けで追加しつつ、そのテーブルのあるカラムに対して外部キー制約を設定しようとしたら…

```
"Foreign key constraint is incorrectly formed"
```

と返されてしまい、解決に手間取ってしまって大変に遺憾であったのでここに記します。

{% include firstad.html %}

## 現象
MariaDB 10.4.14でテーブルを後付けで追加しつつ、そのテーブルのあるカラムに対して外部キー制約を設定しようとしたら、

```
Can't create table <table_name> (error: 150 "Foreign key contraint is incorrectly formed")
```

というエラーが発生してテーブルが作成できない(※テーブル名はフィクションであり、実在のデータベースのテーブル名とは関係ありません)。なお、外部キー制約を削除してテーブルを作成することは可能であった。

{%include secondintervalad.html %}

## 原因
Google先生に原因を教えてもらおうとするも、検索結果のページで提示された原因のいずれにも該当せず(※この記事を最初に書いた時点(2020年12月)の情報です。)、途方に暮れかけました。

途方に暮れかけて昼休みを取ろうとしたまさにその時、追加先のデータベースもmysqldumpコマンドにより取得したdumpファイルから作成したものであったことを思い出しました。

ピコーン!!&#x1f4a1;

「dumpファイル中のテーブルを作成するSQL文と比較すればなんかわかるんじゃね?」

という淡い期待の下、dumpファイル中のテーブルを作成するSQL文と上記の現象が発生したSQL文を見比べたところ、dumpファイル中のSQL文ではengine句の後に

```
CHARSET=utf8
```

と書かれているのを発見しました。
## 対応策
### SQL文の修正
そこで、これを上記の現象が発生したテーブル作成用のSQL文の末尾が

```
ENGINE=InnoDB;
```

となっていたところを、

```
ENGINE=InnoDB CHARSET=utf8;
```

に変更すると…

なんと!!

動きました。ビンゴでした。&#x1f3af;
### 所要時間
2時間くらい溶かしました。

{%include thirdintervalad.html %}

## まとめ
今回は文字コードを指定して解決しましたが、MariaDBの文字コードの最新流行はutf8mb4であって、今時元のデータベースも込みでまだutf8で消耗しているのかといったような方面からのツッコミは平にご容赦ください。

この記事は以上です。

## 参考文献
- [Djangoのmigrateでerrno: 150 "Foreign key constraint is incorrectly formed"](https://qiita.com/t-kigi/items/6acbae8dd1dc8949f110)

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
