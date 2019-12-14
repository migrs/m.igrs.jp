---
layout: post
date: 2018-05-05 12:00:00 +0900
title: Goodbye Mac and Vim
categories: mac vim ubuntu vscode
---

趣味的にいろんな OS やエディターに手を出しつつも、わりと長い間 Mac と Vim をメインの開発環境としてきたのだが、ここ最近その牙城が崩れ今ではすっかり [Ubuntu](https://www.ubuntu.com/) と [VSCode](https://code.visualstudio.com/) 中心な環境にシフトした。

わりと長い間というのは十数年なので僕のエンジニア人生の大部分を占めることになり、節目感じたので残しておく。

### Mac に求めていたこと

僕が開発環境として求めていたのは一言でいうと、  
**「実用的な GUI を備えた UNIX 互換環境」**  
である。

当時(2000年代前半)、Windows + [Cygwin](https://www.cygwin.com/) (+ GVim) な環境で頑張っていたのだが、UNIX 互換環境としては制限が多く、一方その点においては完璧な Linux 系 OS も実用的な GUI を備えてなかったので常用するには厳しかった。
そんな中、出てきた OS X([macOS](https://www.apple.com/jp/macos/))は両者を備えた環境として理想的で魅力的な存在だったし、ついでにカッコよかったので、[Intel Mac](https://ja.wikipedia.org/wiki/Intel_Mac) の到来と共に[僕は MacBook Pro を購入した](http://d.hatena.ne.jp/mig50/20060520/1148772244)。
そしておそらく同じ理由で世界中の開発者もこぞって Mac を選び始めた。

### 求めるものの変化〜仮想化とクラウドの時代

時代と共に仮想化技術が発達し、開発環境として求めるものが UNIX 互換環境からコンテナ実行環境に変わってきた。
[Docker for Mac](https://www.docker.com/docker-mac) などの存在はあるもののホストとのファイル共有において速度的なボトルネックが発生してしまうため快適に利用することは難しく、これは Windows においても同様である。
となると選択肢としては Linux 系 OS に限られてきて、 [Ubuntu](https://www.ubuntu.com/) でも [Gentoo](https://www.gentoo.org/) でも [Arch Linux](https://www.archlinux.org/) でもなんでも良いのだが一番使い慣れているということから今は Ubuntu を選択している。
GUI としては、Win / Mac には劣るものの、一昔前に比べて様々なものがクラウド化しブラウザさえあればなんとかなるものが増えてきていることもあって実用性としては低くはない。

### ハードウェアとしての Mac

ハードウェアとしての Mac を考えてみると、[Touch Bar](https://developer.apple.com/macos/touch-bar/) が搭載されて以降、欲しいと思えるモデルがなくなってしまった。今では大多数の人が Mac を使う世の中になってしまったこともあり所有欲的なものも薄れてきた。
一方、Windows マシンの方がバリエーション豊かでコストパフォーマンスもよく自分にあったマシン探しを楽しめる環境にある。（洗練された良いモデルは少ないが）

僕が今メインで利用しているのは [Lenovo ideapad 720S (13.3インチ)](https://www3.lenovo.com/jp/ja/notebooks-new-splitter/ideapad/ideapad-700-series/Ideapad-720S-13-Intel/p/88IP70S0893) だが 10万円切る価格で十分満足いくボディとスペックである。(できればメモリ16GB欲しいところではあるが)

### エディターについて

常用エディターを GVim から Visual Studio Code にスイッチした件も書くつもりだったが長くなってきたので別に書くことにする。