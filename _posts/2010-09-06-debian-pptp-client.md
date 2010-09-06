---
layout: post
title: Debian PPTP Client
---
今迄需要がなかったので試したことはなかったが、Debian から Client として VPN 接続する方法についてメモ。

導入は、`sudo aptitude install pptp-linux` のみ。

`/etc/ppp/chap-secrets` にアカウント情報を記述し
`/etc/ppp/peers/sample` にサーバ情報を登録。

`sudo pon sample` で接続し、`sudo poff sample` で切断。

ここまでの内容は公式ドキュメントを見ればだいたい分かる。
<http://pptpclient.sourceforge.net/howto-debian.phtml>

VPN接続したところで、Routing の設定も変更する必要あり。
<http://pptpclient.sourceforge.net/routing.phtml>
