---
layout: post
title: Rubyist が今すぐ Elixir を使ってみるべき理由
date: 2012-03-12 00:33
comments: true
categories: elixir ruby translate
---

{% img center http://f.cl.ly/items/3f2z0j113p1W2J3P3E0t/elixir-logo.png 227 95 elixir %}

Elixir の読み方は多分「エリクサー」。RPGゲームのアイテムにありそうな名前だ。
個人的には「エリクシール」と読みたいところだが多分「エリクサー」で良いだろう。
Elixir は最近になって開発が活発化しており、公式サイトも最近立ち上げられたようだ。

<http://elixir-lang.org/>

つい先週のことだが Github でも公式にサポートされている。
<blockquote class="twitter-tweet"><p>Elixir is officially supported on Github! Including file identification and syntax highlight: <a href="https://t.co/YaKXApRH" title="https://github.com/languages/Elixir">github.com/languages/Elix…</a></p>&mdash; Elixir Lang (@elixirlang) <a href="https://twitter.com/elixirlang/status/176735692938936321" data-datetime="2012-03-05T18:27:27+00:00">March 5, 2012</a></blockquote>
<script src="//platform.twitter.com/widgets.js" charset="utf-8"></script>


ここにきて盛り上がってきた感があるので、作者である [José Valim](http://twitter.com/josevalim) が約1年前に書いた [Why Rubyists should try Elixir](http://blog.plataformatec.com.br/2011/03/why-rubyists-should-try-elixir/) という記事を訳してみた。

英語・日本語問わず語学苦手なので読み難い代物になってしまっているが間違いがあったら指摘して欲しい。

#### 追記(2012-03-13)：
昨日 Elixir 勉強会(Shinjuku.ex #1)で初めて [Getting Started Guide](http://elixir-lang.org/getting_started/1.html) を読んだのだが、今の Elixir は訳した記事が書かれた当時とはかなりシンタックスが変更されているようだ。 
なので記事中のコードを最新(0.4.0.dev)に合わせて書き直した。

<!-- more -->

変更されていた点を列挙すると、

- コメントアウトは `%` でなく `#`
- アトムは \` (シングルクォート)ではなく : (セミコロン)
- `module` -> `defmodule`
- `if` や `defmodule` には `do` が必要
- `else` -> `else:`

[Diff はこちら](https://github.com/migrs/m.igrs.jp/commit/0747d7c8cf7cbf867d1654e42f6c6a1bd296308)

少し突っ込んでみて分かったこととして Erlang と Ruby だけではなく Clojure っぽさを強く感じる言語であるということ。

勉強会については [@mizchi](http://twitter.com/mizchi) 氏のレポートがあるよ

[Elixir勉強会いってきました ~~ ErlangとRubyの中間、Elixir](http://d.hatena.ne.jp/mizchi/20120312/1331566107)

-------------------------------------------
## Rubyist が今すぐ Elixir を使ってみるべき理由 (Why Rubyists should try Elixir)

今月(※2011年3月25日現在)の初めに、私は[Elixir](http://github.com/elixir-lang/elixir)についての[スクリーンキャストを公開](http://blog.plataformatec.com.br/2011/03/screencast-elixir-simple-object-orientation-and-charming-syntax-on-top-of-erlang/)している。
 それを見てない人向けに説明すると、Elixir は **Erlangの上にシンプルなオブジェクト指向と魅力的な構文**を提供することを目指している。

私の強いRuby背景に基づいて、私は何度か質問された結果、なぜ Rubyists は Elixir を使ってみるべきかについてのブログ記事を書くことにした。


Elixir が持つ Ruby から来た *method missing* や *module eval* のような多くの構文やいくつかの機能によって同じようにメタプログラミングをすることができる。

しかしながら Elixir は他の何よりも Erlang に間違いなく近い。
単一代入変数、不変性、簡単なプロセス間通信、リスト、タプル、バイナリ、そしてOTPの振舞は、すべて Elixir で利用できる。
したがって Elixir を使うことを通じて多くを学ぶことができるだろう。

多くを学ぶ中で私が楽しく感じたのは次のとおりだ：

### パターンマッチング (Pattern matching)

私にとってパターンマッチングは関数型プログラミングの中で最も楽しい機能の一つだ。
これらによって簡単にデータ構造から情報を抽出することができるようになる。

例えば、Elixir では次のように記述する：

``` elixir
[first, second] = [1,2]
first # => 1
second # => 2
```

Ruby の代入演算子を使用して全く同じように書くことができるが、パターンマッチングの利点はメソッドのシグネチャの中で利用できることで、もしメソッドのシグネチャがある特定のパターンに一致しない場合は次のメソッドが試される。

例えば、文字列のリストを反復処理しそれらを出力する方法は次のとおりだ：

``` elixir
defmodule Printer do
  # これは少なくとも一つの要素が存在するリストにマッチするパターンだ
  # 最初の要素が head に割り当てられ、残りは tail に割り当てられる
  def print([head|tail]) do
    IO.puts head
    print(tail) # 再帰的に tail と引数として print が呼び出される
  end

  # リストが空になったとき上のメソッドではマッチぜず、かわりにこれがマッチする
  def print([]) do
    # 何もしない。すべての出力は完了している。
  end
end

Printer.print ["foo", "bar", "baz"]
```

また別のクールな例はリストが別のリストの接頭辞であるかどうかを確認する再帰的なメソッドだ：

``` elixir
defmodule Prefix do
  # 両方のリストを反復する。もし最初の要素が等しかったら自分自身を再び呼び出す。
  # もし最初の要素(i)が等しくなかったら、このメソッドにはマッチしない。
  def is?([i|prefix], [i|list]) do is?(prefix, list) end

  # もし接頭辞が空だったらこのメソッドにマッチし true を返す。
  def is?([], _list) do true end

  # それ意外なら、false を返す。
  def is?(_prefix, _list) do false end
end

Prefix.is?([1,2,3], [1,2,3,4,5]) # => true
Prefix.is?([0,1,2], [1,2,3,4,5]) # => false
```

最後に、パターンマッチングは Ruby 2.0 で計画されている機能の一つであるキーワード引数を可能にする。
この例は Elixir のコードそのものだ<del>（Elixir のシンボルはコロンではなくシングルクォートでることに注意）</del>：

``` elixir
defmodule Record do
  def retrieve(name, from: file) do
    # ここに実装を書く ...
  end
end
```

Elixir と Erlang のどちらも **while** のような条件ループを提供しないという事実は、あなたに異なる考え方やパターンマッチングの利用を強いることになる。

まずは Ruby で解決して、次に全く別の解決策を考え出すというように、問題について別視点で考えるということは一般的に非常に洞察的で楽しい過程だ。

また、注意として Elixir と Erlang の両方において末尾再起最適化するので、もし Ruby で似たようなメソッドを実装するなら、巨大なスタックトレースを取得することができる場合のみ上手く動作する。

### 単一代入変数と不変性 (Single assignment variables and immutability)

上記例において Erlang の変数は単一代入であることをまだ見せてなかった。
これにより次のエラーが発生する：

``` elixir
[first, second] = [1,2]
first = 10
```

これは bad match error を投げる。
なぜなら既に `first` に値が割り当てられており、2行目の `first = 10` は `1` と `10` を比較しているので当然ここで失敗するのだ。

変数は一度だけ割り当てられるということは、前述の prefix method のような実装が可能となり、両方のリストでマッチして `i` に値が割り当てられる。

また、Elixir と Erlang の両方において、オブジェクト/データ構造はその場で変更することはできない。
こらは不変だ。
すべての変更は新しいオブジェクト/データ構造体を生成する。

不変性は言語内部の共有状態を排除し（外部操作を実行する必要がある場合あなたはまだ状態を共有している）、Erlang と Elixir の並行性に重要な役割を果たしている。

個人的に、不変性は同時に幸福と不幸もたらすことが分かった。
Railsアプリケーションで作業するとき可変性は一般的に問題ではないが、Rails 自体や gem 等の実装においては頻繁に可変性について考える必要がある。変更するメソッドにオブジェクト（ハッシュや配列のような）を渡したときに、そのオブジェクトの中の新しい要素が結局どうなったのかを追跡するために時間を費やさなければならない。

Elixir で作業する際にすべてが不変であるので、このような場合を心配する必要はない、そう、それが気持ちいいのだ！
これは C から Java に行くような感覚で、私は突然メモリ管理を心配する必要もない。

しかし、このような利点はいくつかのコードをより冗長にさせるという明らかな欠点をもたらす。

この欠点を示すために、Rails ライクな PostsController の create アクションを、不変性と単一代入変数の両方を考慮して書き直してみる：

``` elixir
def create
  post0 = Post.new(params[:post])
  post1 = post0.set(:published, false)
  post2 = post1.save

  if post2.persisted? do
    redirect_to post2
  else:
    render :new
  end
end
```

この場合 ORM はよりよい API を提供することができそうだが、これは何度も繰り返されるパターンだ。
たとえば、クッキーを変更するとレスポンスオブジェクトに明示的な変更が必要になる。

``` elixir
response1 = response.cookies.set "tracker_code", "123456"
```

いずれにせよ、不変性と単一代入変数を提供する言語での作業は経験する価値がある。
私が今までのブログ記事で言及したことを試してみることによって多くを学ぶことができるだろう。

追記：
いくつかのコメントで指摘したように、Elixir は単一代入を削除することができて、その上で Erlang の基盤と正常にやりとりすることができる。
このような理由から、Elixir は今では複数回同じ変数に割り当てることができるし、Erlang と比較すると変数のスコープ（Ruby に似ている）に関連したより柔軟なルールがある。

### プロセス間通信 (Communication between processes)

パターンマッチング、単一代入変数と不変性は、プロセス間の通信のための良い基盤を提供する。
もしこれらの動作に興味があるなら[このスクリーンキャスト](http://blog.plataformatec.com.br/2011/03/screencast-elixir-simple-object-orientation-and-charming-syntax-on-top-of-erlang/)を見ると良い。

### 異なるオブジェクトモデル (A different Object Model)

Elixir は Ruby とは異なるオブジェクトモデルを持っている。
オブジェクトモデルはクラスが無いという意味では JavaScript のようなプロトタイプベースだが、JavaScript や Self のそれとは違い
オブジェクトはその子供達がどのようになるかを指示することができ、必ずしも親から正確にコピーされない。

これについてのより多くの情報は [Elixir の README](http://github.com/elixir-lang/elixir) にある。そこには、本当の private メソッド（多分それは Ruby2.0 含まれるかも？）やローカルメソッド呼び出しのようないくつかの他のクールな機能の情報も含まれる。

常に他のオブジェクトモデルを使用することによって多くを学ぶことができ、このチップは Elixir だけに制限されるものではない。
あなたがもし JavaScript のオブジェクトモデルまたは他のプロトタイプベースの言語に精通していないのであれば、今それを学ぶことを勧める。

### 学ぶ (Just learn)

スクリーンキャストやREADMEで述べたように、標準ライブラリとテストの両方が Elixir 自体で書かれているので Elixir に貢献するのはとても簡単だ。
さて、Elixir で [Ruby のセット](http://ruby-doc.org/stdlib/libdoc/set/rdoc/index.html)のような何かを実装しなければならないことを想像してみよう。

Ruby のセットについてさらに深く学ぶだけでなく、使用するための最良の構造はどうあるべきか、どのアルゴリズムがセットを更新するのに適しているか、それらのオブジェクトにアクセスするための優れた API はどうあるべきか、について学ぶ必要がある。

また、パッケージングシステム、ドキュメントパーサーやテスト·ライブラリのようにどの言語でも必要な基本的なツールだけど現在 Elixir で欠如しているこれらはあなたが実装する1つかもしれない！

### 結論 (Wrapping up)

私はあなたが Elixir を試してみること期待するし確信している。この言語に関してもっと知りたければ [README](http://github.com/elixir-lang/elixir) をチェックして欲しい。

最後に、クレイジーなことをするために別のインスピレーションが必要なのであれば [Forking Ruby talk by Dave Thomas](http://pragdave.blogs.pragprog.com/pragdave/2008/12/forking-rubymy-rubyconf-keynote-is-now-up.html) を勧める。

彼が言ったように、私たちは Ruby を愛し、そこからいますぐ離れるようなことは無いが、それを分岐したり新しい物事をしようとすることは言語とそのエコシステムを改善するための素晴らしい方法であり、Elixir がそのことについてさらに考える手助けになることを期待している。
