---
layout: post
categories: lvm
title: LVM上の操作の復旧方法
---
誤って lvremove してしまい焦ったのですが、復旧方法が用意されていたのでメモ。

LVM操作で変更されたメタ情報はすべて `/etc/lvm/archive` に保存されており、これを元に復元作業を行います。

<!--more-->

誤って削除する
     lvremove samplelv

/etc/lvm/archive に保存されている一番最後のファイルを確認
     ls /etc/lvm/archive

バックアップされたメタ情報の確認
     vgcfgrestore -f /etc/lvm/archive/samplevg/samplevg_000XX.vg -l samplevg

メタ情報のリストア
     vgcfgrestore -f /etc/lvm/archive/samplevg/samplevg_000XX.vg samplevg

変更の反映
     vgchange -ay samplevg

LVの存在確認
     lvs
