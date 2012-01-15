---
layout: post
title: PHPより気軽に、Rubyで簡単ウェブ開発
date: 2012-01-06 07:09
comments: true
categories: rack-server-pages ruby
---

元旦に [rack-server-pages](http://github.com/migrs/rack-server-pages) というものを[リリース](http://rubygems.org/gems/rack-server-pages)しました。

<blockquote class="twitter-tweet tw-align-center"><p>元旦リリースしました。僕からのお年玉です。 &gt; rack-server-pages <a href="http://t.co/MODtXuOL" title="http://j.mp/uNthnL">j.mp/uNthnL</a> <a href="https://twitter.com/search/%2523ruby">#ruby</a></p>&mdash; Masato Igarashi (@migrs) <a href="https://twitter.com/migrs/status/153393608664424448" data-datetime="2012-01-01T08:34:20+00:00">January 1, 2012</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

実は数年前からずっと作りたいと思っていたもので個人ToDoリストに長らく居座っていたものがやっと着手できた。

<!--more-->

Ruby で WEB開発といえば [Ruby on Rails](http://rubyonrails.org/) というデファクトスタンダードを筆頭に
MVCフレームワークを利用するのが一般的ですが、現状フレームワークを利用しないという選択肢がほとんど無いんですよね。

フレームワークというキーワードを聞くだけで「よく分からない」「プログラマの為のもの」
感覚になってしまう人も多いはずです。
たとえシンプルで軽量といわれている [Sinatra](http://sinatrarb.com/) ですら。

[PHP](http://php.net/) が初心者やデザイナーも含め広く受け入れられたのは
HTMLファイルの延長のような感覚で扱えたからというのも一つの大きな要因でしょう。

<blockquote class="twitter-tweet tw-align-center"><p>PHPは言語仕様以外の部分は別に悪いと思ってないし、Better PHP として mod_ruby + erb のような構成はあっても良いはずと昔から思っている</p>&mdash; Masato Igarashi (@migrs) <a href="https://twitter.com/migrs/status/99322027403526145" data-datetime="2011-08-05T03:33:11+00:00">August 5, 2011</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

同じように思っている人もいるようで、

[super simple serving of ruby pages](http://www.ruby-forum.com/topic/82003)
> I'm starting to teach my 8yr daughter Ruby. We've covered HTML and CSS
> already and she handcoded her own static website. I'd like to
> incorporate her Ruby learning experience into her website, which is
> much more interesting for her than using Ruby to write scripts or
> desktop apps. She's just starting out, so Rails is much too complicated
> for her. She's not ready for the whole MVC concept yet. What I'd like
> to do is to run very simple Ruby scripts from the site and incorporate
> Ruby code into rhtml files, but without Rails. I don't really want a
> "framework", just the ability to run a ruby file that will serve up an
> rhtml file. In other words, something very simple like PHP (I don't
> want to teach her PHP). [I'll get into Rails later once she's more
> advanced.]

[how do you create a simple web page with ruby?](http://www.codingforums.com/showthread.php?t=230780)
> I know how to set up html web sites. I started learning php, and it's really easy to create a php web page. You just name the file extension .php, and then you intersperse any php code you want in the html with <?php .... ?>. You throw the page up on the web, and it works exactly like you think it would.
> 
> But I have *no idea* how to set up a simple "hello world" web page in ruby. 

このような需要を満たす為に作りました。

もちろん効率的なWEB開発にはフレームワークは必要不可欠なのですが必要の無いケースも多々あるし、
何より気軽に体験できる環境を提供したかったのです。

幸運なことに [Rack](http://github.com/rack/rack) や [Tilt](http://github.com/github.com/rtomayko/tilt) という強力で素晴らしい資産のおかげで
気軽さだけではなく実用性も兼ね備えることが出来ました。

特に [Pow](http://pow.cx), [Rack Server Pages](http://github.com/migrs/rack-server-pages) の組み合わせはWEBデザイナーな人にも是非体験して欲しい環境で、
[Sass](http://sass-lang.com/), [Slim](http://slim-lang.com/), [CoffeeScript](http://jashkenas.github.com/coffee-script/) 等、ほぼプログラマ向けになってしまっている技術が気軽に活用でき少し幸せになれるはず。

ここでは紹介まで。

日本語のドキュメントが全くないので（実際 [Watchers](https://github.com/migrs/rack-server-pages/watchers) も外国の方ばかり）少しずつ書いていければと。（誰か私に文章力と英語力を！）

まだまだ発展途上ですが、問題・不具合あれば[連絡](https://github.com/inbox/new/migrs)・[フィードバック](https://github.com/migrs/rack-server-pages/issues)お願いします。

