---
title: OpenVPNのためのSELinuxポリシーを変更する際にポリシー名を"openvpn"にしたところ、変更に失敗した件。 - panda大学習帳外伝
description: ポリシー名のご利用は計画的に。
image: https://pandanote.info/wordpress/wp-content/uploads/2020/05/P_20200522_183454_vHDR_On_HP-scaled.jpg
twitter:
  card: summary_large_image
mathjax: true
encoding: UTF-8
---
{% include pagelink.md %}
# OpenVPNのためのSELinuxポリシーを変更する際にポリシー名を"openvpn"にしたところ、変更に失敗した件。
## はじめに
panda大学習帳のWebサーバ(https://pandanote.info/)のFedoraのバージョンを32に変更してしばらくたってからのこと。

スマホから上記サーバにログインしてipコマンドを実行してみたところ…

```
[panda@pandanote.info ~]$ ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
(中略)
4: ens5: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 9c:a3:ba:05:2e:bb brd ff:ff:ff:ff:ff:ff
    altname enp0s5
```

```
(　ﾟдﾟ) ・・・
```

なんか、OpenVPN用のインタフェースがいつの間にか起動しなくなっていたようです。

そこで、なんでそうなるのか原因を調べつつ、OpenVPNサーバが起動するように再度設定を行うこととしました。

{% include firstad.html %}
## ログファイルの確認
問題が発生したときにはまずログの確認です。

まず、/var/log/messagesの中身を確認します。

すると…

```
Jun 21 00:00:00 pnr systemd[1]: Starting OpenVPN service for server...
Jun 21 00:00:01 pnr audit[1074387]: AVC avc:  denied  { write } for  pid=1074387 comm="openvpn" name="openvpn-status.log" dev="dm-0" ino=17093069 scontext=system_u:system_r:openvpn_t:s0 tcontext=system_u:object_r:openvpn_etc_t:s0 tclass=file permissive=0
Jun 21 00:00:01 pnr systemd[1]: openvpn-server@server.service: Main process exited, code=exited, status=1/FAILURE
Jun 21 00:00:01 pnr systemd[1]: openvpn-server@server.service: Failed with result 'exit-code'.
```

いきなりビンゴのようです!!

SELinuxに邪魔されているようです…
## audit2allowでポリシーファイルを作成
ここまでの作業はソファに寝つつ、スマホ(Zenfone4(ZE554KL))を使って作業していましたが、ここからは複雑なコマンドを入力せねばならないので、PCの前に移動です。
### うまくいかなかった例
早速、root権限で以下のコマンドを実行です。

「これにて一件落着!!」と思われたのですが…
```
[root@pandanote.info panda]# grep avc /var/log/audit/audit.log | audit2allow -M openvpn
[root@pandanote.info panda]# semodule -i openvpn.pp
libsemanage.semanage_direct_install_info: Overriding openvpn module at lower priority 100 with module at priority 400.
Failed to resolve typeattributeset statement at /var/lib/selinux/targeted/tmp/modules/400/openvpn/cil:1
semodule:  Failed!
```
設定に失敗してしまいました。

初めて見るエラーメッセージですね。
### うまくいった例
失敗した原因を追究するために、Google先生にお伺いを立ててみます。

すると、「既にあるポリシーと同じ名前のポリシーを使おうとするとエラーになるよ。」というありがたい情報がありました。

そこで、root権限でポリシー名を変更し、再度以下のコマンドを実行してみました。
```
[root@pandanote.info panda]# grep avc /var/log/audit/audit.log | audit2allow -M openvpn_pandanote
[root@pandanote.info panda]# semodule -i openvpn_pandanote.pp
```
エラーメッセージが表示されず、コマンドが終了していきました。
## 動作の確認
/var/log/messagesを見る限り、OpenVPNはsystemdで起動されるもののようですので、ちょっと待ってから、ipコマンドを実行してみると…
```
[root@pandanote.info panda]# ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
(中略)
4: ens5: <BROADCAST,MULTICAST> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 9c:a3:ba:05:2e:bb brd ff:ff:ff:ff:ff:ff
    altname enp0s5
5: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 100
    link/none
    inet 192.168.ppp.qqq peer 192.168.ppp.rrr/32 scope global tun0
       valid_lft forever preferred_lft forever
    inet6 fe80::7b0d:10d4:1789:6eb4/64 scope link stable-privacy
       valid_lft forever preferred_lft forever
```
(一部改変しています。)

OpenVPN用のインターフェースが(再び)有効になりました!! &#128512;

pingも通るようです。

{%include secondintervalad.html %}
## まとめ
audit2allowコマンドの引数に指定したポリシー名が既存のものと被るのは想定外だったので、以後気をつけます。
## 参考文献
* [SELinux の ポリシ－を追加する](https://gokugetsu.plala.jp/selinux-%E3%81%AE-%E3%83%9D%E3%83%AA%E3%82%B7%EF%BC%8D%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B/)

## リンク
[OpenVPN設定外伝: 設定でハマったところn選](https://pandanote.info/?p=2038) \| [Fedora31からFedora32へのupgrade – WordPressまわりでちょっと作業が必要だった件。](https://pandanote.info/?p=6361) \| {% include pagelink.md %}

{% include fourthintervalad.html %}
