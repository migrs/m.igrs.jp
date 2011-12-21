---
layout: post
categories: server
title: muumuu dns
---
EveryDNS では TXT Record がサポートされないことを知り、他の DNS Provider をいろいろ調べていたのだがたくさんあってどれも決定打が無い。

ドメイン管理に[ムームードメイン](http::/muumuu-domain.com/)を使っているのですが、そういえば[ムームーDNS](http://muudns.muumuu-domain.com/)を提供し始めたことを思いだし、同じところで管理できた方が都合良さそうなので、移行した。

ゾーン転送許可しているみたいなんだけど、大丈夫なのかな？

`dig @dns01.muumuu-domain.com igrs.jp axfr`
