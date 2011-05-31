---
layout: post
tags: [drbd, ocfs2, debian, lvm]
title: DRBDボリュームのオンラインリサイズ
---

Dual Primary で構成している状態だとオンラインリサイズ出来ないようなので(出来るようであれば教えてください！)、片方 Secondary に降格させてからリサイズすることになる。

## リサイズ手順

両方のサーバ(sv1,sv2)で LVMパーティションの拡張をする

    sv1$ sudo lvextend -L +1G /dev/sys/drbd0
    sv2$ sudo lvextend -L +1G /dev/sys/drbd0

片方を Secondary に降格

    sv2$ sudo drbdadm secondary r0

drbdadm resize コマンドの実行。Primary のみで実行。(see [リソースのサイズ変更](http://bit.ly/kj3Yk5))

    sv1$ sudo drbdadm resize r0

ファイルシステムの拡張(ocfs2の場合)。Primary のみで実行。

    sv1$ sudo tunefs.ocfs2 -S /dev/drbd0

これでリサイズ完了。

最後に一時降格した Secondary を Primary に昇格

    sv2$ sudo drbdadm primary r0

両方のサーバで拡張されたボリュームをマウントして終了

    sv1$ mount /dev/drbd0 /mnt/drbd0
    sv2$ mount /dev/drbd0 /mnt/drbd0

## サイズ確認方法
上記手順中にて実際拡張されているか確認する方法

ブロックデバイスのサイズ確認
    sudo blockdev --getsz /dev/sys/drbd0

マウントされているファイルシステムのサイズ確認
    df -h

## 参考URL
- [リソースのサイズ変更](http://bit.ly/kj3Yk5)
- [DRBD リソース・サイズを拡張](http://bit.ly/jMWKe1)
