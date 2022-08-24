---
title: Linux上のEmacsにおける日本語入力のための設定をWindows上におけるEmacsの操作感に合わせるための設定。 - panda大学習帳外伝
description: 「カタカナ/ひらがな」キーの名前が想定外過ぎたので、メモっておくことにしました。
mathjax: true
image: https://pandanote.info/wordpress/wp-content/uploads/2022/08/P_20220824_221854-scaled.jpg
twitter: 
  card: summary_large_image
encoding: UTF-8
update: Wed Aug 24 23:06:42 2022 +0900
---
{% include pagelink.md %}
# Linux上のEmacsにおける日本語入力のための設定をWindows上におけるEmacsの操作感に合わせるための設定。
{% if page.update %}最終更新日: {{ page.update }} {% endif %}
## はじめに
久々にLinux上のEmacsを使ってある程度まとまった長さの文章を書こうとしたのですが、あまりにも久々過ぎたせいか、Linux上のEmacsではほぼ定番の

「Ctrl-backslashを使って日本語入力のON/OFFを切り替える。」

操作にそこはかとない違和感を覚えました。

そこで、

「Linux上のEmacsにおける操作感をWindows上にEmacsの操作感に合わせる。」

ための設定方法を探ることにしました。

{% include firstad.html %}

## 実現したいこと
Windows上のEmacsではIMEを使用して入力を行っています。

IMEでは、「半角/全角」キー(下図の赤矢印(a))または「カタカナ/ひらがな」キー(下図の赤矢印(b))を押すことで日本語入力のON/OFFを切り替えることができます。

<a href="https://pandanote.info/wordpress/wp-content/uploads/2022/08/P_20220824_221854_a-scaled.jpg"><img width="540" src="https://pandanote.info/wordpress/wp-content/uploads/2022/08/P_20220824_221854_a-scaled.jpg"/></a>

これと同様の操作をLinux上のEmacsで実現する方法を考えます。

{%include secondintervalad.html %}

## Emacsの設定
Emacsの日本語入力システムとしてMozcを使用している場合において、「半角/全角」キーまたは「カタカナ/ひらがな」キーを日本語入力のON/OFFの切替用のキーとして使うためには以下の設定を.emacs/init.elに追加します。

```
(global-set-key [zenkaku-hankaku] 'toggle-input-method)
(global-set-key (kbd "<XF86Launch6>") 'toggle-input-method)
```

1行目が「半角/全角」キーのための設定で、2行目が「カタカナ/ひらがな」キーのための設定です。

「半角/全角」キーのキーの名前はある程度予想がつきますが、「カタカナ/ひらがな」キーについては全くの想定外の名前でした。

想定外の名前ではあったものの、「カタカナ/ひらがな」キーに機能を割り当てない状態で「カタカナ/ひらがな」キーを押すと、ミニバッファにキー名が表示されますので、キーの名前を知ることができます。

{%include thirdintervalad.html %}

## まとめ
前節の設定を行うことにより、Linux上のEmacsが使いやすくなったような気がします。

使いやすくなったような気はするものの、「カタカナ/ひらがな」キーの名前があまりにも想定外だったので、メモっておくことにしました。

何かの参考にしていただけると幸いです。

## リンク
{% include pagelink.md %}

{% include fourthintervalad.html %}
