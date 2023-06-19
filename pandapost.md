---
title: Twitter API v2でWordPressの最新記事(?)の追加のお知らせをコマンドラインからツイートする簡易プログラムを作った。 - panda大学習帳外伝
description: Termuxから使える簡易プログラムをPHPで作ってみました。
mathjax: true
image: https://ipfs.io/ipns/pandanote.info/Screenshot_2023-06-17_215616.png
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Tue Jun 20 00:25:39 2023 +0900
---
{% include pagelink.md %}
# Twitter API v2でWordPressの最新記事(?)の追加のお知らせをコマンドラインからツイートする簡易プログラムを作った。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
WordPressで絶賛運用中の「<a href="https://pandanote.info/">panda大学習帳</a>」に新しい記事が追加されるごとにTwitterにその旨をツイートし、Google先生による検索結果を介さずに新規の記事が追加されたこと世に広く知らしめるためのWordPressのプラグインとして使用していたSocial Networks Autoposter (SNAP)がこの度使えなくなってしまいました。

{% include firstad.html %}

そこで、やむを得ず同様の機能を持つツールを自作することも辞さないという不退転の決意を持って、代替手段を探ることを検討することにしました。

## SNAPが使えなくなったときの状況
### 状況の確認
SNAPが使えなくなっていたことが発覚したのは、<a href="https://pandanote.info/?p=10586">この記事</a>を投稿した直後のことでした。

投稿してから5分程度待ってもツイートがされなかったので、再投稿(repost)の設定を行った上で再度しばらく放置してツイートがされないことを確認して、SNAPのログを確認すると…

<a href="https://ipfs.io/ipns/pandanote.info/Screenshot_2023-06-17_215616.png"><img width="540" src="https://ipfs.io/ipns/pandanote.info/Screenshot_2023-06-17_215616.png"/></a>

エラーメッセージが表示されています。

Twitter API経由で投稿を試みた結果として、"Could not authenticate you."とのメッセージが返されています。

実に慇懃無礼な感じのメッセージです。

Twitter APIのページを確認したところ、Screenshotは取るのを忘れてしまったのですが、SNAPで使用していたTwitterアプリケーションのAPIキー(Twitter API v1.1専用)のステータスが"SUSPENDED"になっていました。

### とりあえずの対応
Twitter APIのページにはSNAP用のものも含め、2個のTwitterアプリケーションが作られていました。

2023年2月以降、何回かにわたって行われたTwitter APIの仕様変更に伴い、Freeプランでは2個以上のTwitterアプリケーションを持つことができなくなってしまったようです。また、Twitter API v1.1は2023年4月29日に公式には非推奨となっていました(参考文献1参照)。

そこで、Twitter API v1.1専用だったSNAP用のTwitterアプリケーションを削除しました。

{%include secondintervalad.html %}
## 簡易プログラムの作成
### プログラムができあがるまでの気の迷い
SNAP用のTwitterアプリケーションを削除すると、Twitter APIのページにはいつ作ったのか忘れたものの、なぜかTwitter API v2対応になっているTwitterアプリケーションが残りました。

APIキーは発行できそうだったので、APIキーを発行し直すことにしました。

次に、SNAPをTwitter API v2対応にできないかと考え、SNAPのコードを見てみたものの、コードが複雑すぎて、修正作業は日曜プログラミングの範疇を超えたものになると判断したため断念しました。

一方で、PHPからTwitter API v2をお手軽に扱えるSDKのようなものがないか調べたところ、<a href="https://twitteroauth.com">TwitterOAuth</a>なるライブラリが存在していることがわかりました。

そこで、SNAPのことは完全に忘れることにして、Twitter API v2対応のプログラムを作ることとしました。

作るついでに、スマホ上で稼働しているTermuxからも投稿できるようにするために、Termuxのコマンドラインから投稿可能なプログラムとすることにしました。

{%include thirdintervalad.html %}

### プログラム例
投稿するメッセージ中には新規に追加した記事のURLが必要ですが、「panda大学習帳」ではURLの一部にWordPressのpost IDを使用しています。

そこで、PDOを使って有効なpost IDのうち最大のものを取得するコードを書いています(詳細は<a href="https://sidestory.pandanote.info/wordpress_sql.html">こちら</a>参照)。

ここまでの考察の結果出来上がったプログラムは以下のようになります(APIキーとデータベースへの接続情報は削除しています)。

```
<?php
require "vendor/autoload.php";

use Abraham\TwitterOAuth\TwitterOAuth;

$consumerKey = '???';
$consumerSecret = '???';
$accessToken = '???';
$accessTokenSecret = '???';

$dbh = new PDO("mysql:host:???; dbname=???; charset=utf8mb4;","???","???");

$currentid = $dbh->query("select max(ID) as currentid from wp_posts where post_status='publish' and post_type in ('page','post');")->fetch(PDO::FETCH_ASSOC);

if (count($currentid) == 0) {
   echo "Not Found!!";
   exit(1);
}

$connection = new TwitterOAuth($consumerKey, $consumerSecret, $accessToken, $accessTokenSecret);
$connection->setApiVersion("2");

$tweet_parameters['text'] = "My new blog post → pandanote.info/?p=".$currentid['currentid']."\n#lifeinyokohama\nhttps://pandanote.info/?p=".$currentid['currentid'];
$result = $connection->post('tweets',$tweet_parameters,true);
```

…とここまで書いてきたところで、コマンドラインで動かすことしか考えないのならPHPよりもPython3の方が良かったような気がしてきましたが、WordPressのプラグイン化の夢が完全に捨てきれないのでPHPで押し通すことにしました。
### 動作例
上記のプログラムを適当な場所に保存し、「panda大学習帳」に新しい記事を投稿してから実行すると、以下のツイートがTwitterに投稿されます。

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">My new blog post → <a href="https://t.co/bI3o3lRGw5">https://t.co/bI3o3lRGw5</a><a href="https://twitter.com/hashtag/lifeinyokohama?src=hash&amp;ref_src=twsrc%5Etfw">#lifeinyokohama</a><a href="https://t.co/zeMMJhYdCH">https://t.co/zeMMJhYdCH</a></p>&mdash; pandanote.info (@Pandanote_info) <a href="https://twitter.com/Pandanote_info/status/1670351578849751041?ref_src=twsrc%5Etfw">June 18, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

無事投稿できました。
## まとめ
「課金品しなければほぼ何もできない。」というレベルにまで有料化されてしまったTwitter APIですが、人力で更新しているブログの記事の新規追加のお知らせをTwitterに投稿するだけなら「人力で更新する」プロセスが律速段階となるため、何とか使えそうなことが確認できました。

当面は「panda大学習帳」に新しい記事を投稿後に本記事で書いた簡易プログラムでTwitterに投稿する方法で運用します。

この記事は以上です。
## 参考文献
1. <a href="https://twittercommunity.com/t/deprecating-the-premium-v1-1-api/191092">Deprecating the Premium v1.1 API</a>

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
