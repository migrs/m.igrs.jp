---
layout: post
tags: etckeeper linux
title: etckeeper のカスタマイズ
---
`etckeeper log` が欲しい！ということで
[etckeeperのつかいかた（インストール、サブコマンド追加）](http://blog.udzura.jp/2010/11/22/tutorial-of-etckeeper/)
を参考に作成した。


### サブコマンドの追加
`/etc/etckeeper/log.d/10git-log`
{% highlight sh %}
    #!/bin/sh
    LV='-Ou8 -c' git --git-dir=/etc/.git log --stat
{% endhighlight %}

`/etc/etckeeper/show.d/10git-show`
{% highlight sh %}
    #!/bin/sh
    LV='-Ou8 -c' git --git-dir=/etc/.git show $1
{% endhighlight %}

chmod +x も忘れずに。

### サブコマンドの利用
{% highlight sh %}
    sudo etckeeper log
    sudo etckeeper show {commit-ish}
{% endhighlight %}
    
