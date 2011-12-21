---
layout: post
categories: linux, dropbox, debian
title: Linux CUI 環境で Dropbox を使う
---
公式 Wiki の方に詳しく書いているのでその通りの手順で設定できた。

* [How To Install Dropbox In An Entirely Text Based Linux Environment](http://wiki.dropbox.com/TipsAndTricks/TextBasedLinuxInstall)

## Setup ##
### Dropbox のインストール ###
    wget -O dropbox.tar.gz http://www.dropbox.com/download/?plat=lnx.x86
    tar zxvf dropbox.tar.gz
    mv .dropbox-dist ~

### Dropbox CLI のインストール ###
    mkdir -p ~/bin
    wget -P ~/bin http://www.dropbox.com/download?dl=packages/dropbox.py
    chmod 755 ~/bin/dropbox.py

#### Dropbox CLI の使い方
<pre>
Dropbox command-line interface

commands:

 status       get current status of the dropboxd
 help         provide help
 puburl       get public url of a file in your dropbox
 stop         stop dropboxd
 start        start dropboxd
 filestatus   get current sync status of one or more files
 ls           list directory contents with current sync status
</pre>

### 自動起動設定 ###
[ここ](http://wiki.dropbox.com/Regole/TextBasedLinuxInstall)にあるものだと stop/status 等動かなかったので若干修正
``` sh /etc/init.d/dropbox http://gist.github.com/592840 gist
#!/bin/sh
# /etc/init.d/dropbox
### BEGIN INIT INFO
# Provides:          dropbox
# Required-Start:    $network $syslog $remote_fs
# Required-Stop:     $network $syslog $remote_fs
# Should-Start:      $named $time
# Should-Stop:       $named $time
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Start and stop the dropbox daemon for debian/ubuntu
# Description:       Dropbox daemon for linux
### END INIT INFO

DROPBOX_USERS="user1 user2"
start() {
    echo "Starting dropbox..."
    for dbuser in $DROPBOX_USERS; do
        start-stop-daemon -b -o -c $dbuser -S -x /home/$dbuser/.dropbox-dist/dropboxd
    done
}

stop() {
    echo "Stopping dropbox..."
    for dbuser in $DROPBOX_USERS; do
        start-stop-daemon -o -c $dbuser -K -x /home/$dbuser/.dropbox-dist/dropboxd
    done
}

status() {
    for dbuser in $DROPBOX_USERS; do
        dbpid=`pgrep -u $dbuser dropbox`
        if [ -z $dbpid ] ; then
            echo "dropboxd for USER $dbuser: not running."
        else
            echo "dropboxd for USER $dbuser: running."
        fi
    done
}


case "$1" in
  start)
    start
    ;;

  stop)
    stop
    ;;

  restart|reload|force-reload)
    stop
    start
    ;;

  status)
    status
    ;;

  *)
    echo "Usage: /etc/init.d/dropbox {start|stop|reload|force-reload|restart|status}"
    exit 1

esac

exit 0
```


あとは、
    chmod +x /etc/init.d/dropbox
    update-rc.d dropbox defaults
で設定完了。
