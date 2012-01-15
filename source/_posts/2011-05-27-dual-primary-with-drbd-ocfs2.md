---
layout: post
categories: drbd ocfs2 debian lvm
title: DRBD + OCFS2 で Dual Primary クラスタ構築
---

DRBD で Dual Primary な構成を実現するには [OCFS2](http://bit.ly/iZ2N4Z) か [GFS2](http://red.ht/k2CYeG) 等のファイルシステムを導入する必要がある。

<!--more-->

[弊社](http://fujisan.co.jp/)[CTO](http://twitter.com/akamiya)曰く、
> GFS2のほうがクラスタノードへの書き込み反映が早くて、OCFS2のほうがロックマネージメントがうまいっていう感触があるかな。

とのこと。

今回はよりシンプルな OCFS2 の方を試してみる。

OSはいつものとおり Debian です。

## DRBD の導入と設定

### インストール
    sudo aptitude install drbd8-utils
    sudo modprobe drbd

### 必要なLVM領域の確保
- 同期するデータを置くパーティションをLVMで作成
- メタ情報を同一パーティション内か外部かで選択できる
  - 今回は外部に持つことにするのでメタ情報用パーティションも作成
  - 内部に持つとオンラインリサイズができなかったりパフォーマンス的に若干不利だったり
    - [DRBD リソース・サイズを拡張](http://bit.ly/jMWKe1)
  - [メタデータサイズの見積もり](http://bit.ly/mgVetG)
    - 128MB あれば充分


sv1,sv2 の両方で実行
    sudo lvcreate -L 10G -n drbd0 sys
    sudo lvcreate -L 128M -n drbd0_meta sys

### 設定
#### `/etc/drbd.d/r0.res` の編集
```
resource r0 {
  protocol C;

  startup {
    wfc-timeout 30;
    degr-wfc-timeout 10;
    become-primary-on both;
  }

  syncer {
    rate 1G;
  }

  disk {
    on-io-error detach;
  }

  net {
    allow-two-primaries;
    after-sb-0pri discard-zero-changes;
    after-sb-1pri discard-secondary;
    after-sb-2pri disconnect;
  }

  on sv1 {
    device    /dev/drbd0;
    disk      /dev/sys/drbd0;
    address   192.168.0.1:7789;
    flexible-meta-disk /dev/sys/drbd0_meta;
  }
  
  on sv2 {
    device    /dev/drbd0;
    disk      /dev/sys/drbd0;
    address   192.168.0.2:7789;
    flexible-meta-disk /dev/sys/drbd0_meta;
  } 
}
```

- sv1, sv2 は実際のホスト名である必要があります。
- sv1,sv2 全く同じものを配置

#### メタ情報の作成
sv1,sv2 の両方で実行
    sudo drbdadm create-md r0

#### 起動
sv1,sv2 の両方で実行
    sudo /etc/init.d/drbd start

#### 状態の確認
    cat /proc/drbd

`st:Secondary/Secondary ds:Inconsistent/Inconsistent` な表示になっているはず

#### 片方を Primary に昇格
片方(sv1)を Primary に昇格させることで、同期も開始されます。
    sudo /sbin/drbdadm -- -o primary r0

`/proc/drbd` を監視しましょう
    watch cat /proc/drbd
`st:Primary/Secondary ds:Inconsistent/Inconsistent` な表示になり、`[>...................] sync'ed:  0.9%` な部分から同期中であることがわかります。

同期が終わると、`st:Primary/Secondary ds:UpToDate/UpToDate` という表示になります。

- 同期速度(syncer rate) を設定しないとデフォルト 250KB になってしまうので適切に設定しておきましょう。[同期速度の設定](http://bit.ly/kdf1Cq)

#### もう片方も Primary に昇格させ Dual Primary に！
もう片方(sv2)にて
    sudo /sbin/drbdadm primary r0

とすることで、`st:Primary/Primary ds:UpToDate/UpToDate` な状態になりブロックデバイスレベルでの Dual Primary 構成の完成です。

## OCFS2 の導入と設定
この Dual Primary なブロックデバイス上にファイルシステムを構築します。

### インストール
    sudo aptitude install ocfs2-tools


### 設定

#### `/etc/ocfs2/cluster.conf` の編集
```
cluster:
  node_count = 2
  name = ocfs2

node:
  ip_port = 7777
  ip_address = 192.168.0.1
  number = 0
  name = sv1
  cluster = ocfs2

node:
  ip_port = 7777
  ip_address = 192.168.0.2
  number = 1
  name = sv2
  cluster = ocfs2
```

- sv1,sv2 全く同じものを配置

#### 設定ツールの起動
    sudo dpkg-reconfigure ocfs2-tools

↑すべてデフォルト値でOK

### サービス開始
    sudo /etc/init.d/o2cb start
ここまで両方のサーバで実行します。

    sudo /etc/init.d/o2cb status

`Checking O2CB heartbeat: Not active` となりますが正常です。

## DRBD ブロックデバイス上に OCFS2 ファイルシステム作成
既にブロックデバイスレベルで同期されているので片方どちらかで実行します。
    sudo mkfs.ocfs2 -N 2 /dev/drbd0

早速両方のサーバでマウントしてみましょう。
    sudo mkdir /mnt/drbd0
    sudo mount /dev/drbd0 /mnt/drbd0

ここでもう一度ステータスの確認してみると
    sudo /etc/init.d/o2cb status

`Checking O2CB heartbeat: Active` になってます。

これで両方から同時にマウントできるファイルシステムの完成です。
試しに、両方のサーバからファイルを作成したり更新したり削除したりしてみてください。
互いに変更が反映されるようになっているはずです。

まだ書きたいことはあるが長くなったので一旦ここまで。
