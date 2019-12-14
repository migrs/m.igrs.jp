---
layout: post
date: 2019-12-14 12:00:00 +0900
title: Vimacs - VS Code で Vim と Emacs のいいとこどり
categories: vscode vim emacs vimacs
---


昨年からメインエディターを [Vim から VS Code に移行した](http://localhost:4000/blog/2018/05/06/goodbye-vim/)のですが、やはり Vim キーバインドからは逃れられず基本的には [Vim 拡張](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim) を利用して過ごしています。

また普段の Vim ではインサートモード時に基本的な Emacs キーバインディングを使えるようにカスタマイズしているのですが、それは別途キーバインディングファイル（`keybindings.json`）をカスタマイズすることで実現できていました。

今回は、そんなニッチな設定だけど同じようなことをしている人は他にもいるはずだし、オススメのスタイルなのでぜひみんなにも使って欲しいという思いから VS Code 拡張を作ったので紹介します。

## Vimacs for VS Code

![](https://raw.githubusercontent.com/migrs/vscode-vimacs/master/images/icon.png)

[VSCodeVim](https://marketplace.visualstudio.com/items?itemName=vscodevim.vim) のインサートモードで基本的な Emacs キーバインディングを利用できるようにする VS Code 拡張です。
（_VSCodeVim_ のアイコンをベースにしてますが、作者から許可は得ています）

- [Vimacs for VS Code](https://marketplace.visualstudio.com/items?itemName=migrs.vimacs#review-details) (Visual Studio Code Marketplace)
- [vscode-vimacs](https://github.com/migrs/vscode-vimacs) (GitHub)

### Original Vimacs

Vimacs という名前ですがもともと Vim Plugin として同様の名前のものがありました。

- [Vimacs: Vim-Improved Emacs](http://algorithm.com.au/code/vimacs/)
- [github.com/andrep/vimacs](https://github.com/andrep/vimacs)

コンセプトがほぼ同じということで *for VS Code* として名前を継承しつつ、よりシンプルな実装としました。

### Why use Vimacs?

Vim の最大の特徴はノーマルモードやブロックモードにおけるキーバインディングにあると思っていて、学習ハードルは高いものの一度その操作に慣れるとテキスト編集ツールとしては右に出るものがないくらい強力なツールとしてその威力を発揮します。

一方、インサートモードの実装は非常にシンプルで、ノーマルモードで編集することを前提としているのでコンセプトとしては理解できるのですが、入力・修正を繰り返すようなテキスト編集を行う際に頻度の高いモード切替は煩わしく感じることがあります。

また、macOS のほぼすべてのテキスト編集コンポーネントではシンプルな Emacs キーバインドが利用できるようになっていたり、シェル操作でも Emacs ベースなものが標準的になっていたりすることもあって、文字入力においては Emacs キーバインドの方が慣れ親しまれたものとなっています。

ということで、Vim のインサートモードのときに基本的な Emacs キーバインディングが利用できるようにすることで両者のメリットをいいところどりしてちょっと幸せになれるハイブリッドスタイルを提唱します。

### やりたいこと

- ベースの環境としては VS Code を使いたい
- カーソル操作は Vim キーバインドを使いたい
- 文字入力時は Emacs キーバインドを使いたい

|    -     |     命令     |        編集        |    入力     |
| :------: | ------------ | ------------------ | ----------- |
|  *Vim*   | Command Mode | Normal/Visual Mode | Insert Mode |
| *Vimacs* | VS Code      | Vim                | Emacs       |

Vim がコンテキストごとに各モードを使い分けるのと同じよな感覚でに各エディターを使い分けるイメージです。

### コンセプト

- コマンド系のキーバインドは VS Code 標準のものを利用する
- _VSCodeVim_ をベースとして基本的にインサートモードのときだけ Emacs キーバインドを定義

### できること

- インサートモードで基本的な Emacs キーバインディングが使える
- カーソル移動以外ではリージョン操作系にも対応
- VS Code のコマンド入力やファイル選択のUIでも `Ctrl+N`, `Ctrl+P` などのカーソル移動に対応

### てきてないこと

- キーバインディングが重複定義されたときの優先順の制御の仕様がよくわかっておらず、意図通り動かないキーバインディングがいくつかある
  - `keybindings.json` の方で再度定義したり邪魔なものを無効にしたりすることで回避している
- Column Region Mode も実装してみたのですがまともに動いてなかったのでいったん取り下げてます

Pull Request お待ちしております

### 設定例

参考までに私の _VSCodeVim_ 個人設定（`settings.json`）では以下のような設定となっています。Vimacs 独自の設定項目はとくにありません。

```json
{
    "vim.useCtrlKeys": false,
    "vim.overrideCopy": true,
    "vim.hlsearch": true,
    "vim.useSystemClipboard": false,
    "vim.visualstar": true,
    "vim.handleKeys": {
        "<C-f>": true,
        "<C-b>": true,
        "<C-u>": true,
        "<C-r>": true,
        "<C-v>": true,
        "<C-[>": true,
        "<C-w>": true,
    },
    "vim.cursorStylePerMode.normal" : "block",
    "vim.cursorStylePerMode.insert": "line-thin",
    "vim.cursorStylePerMode.replace": "block-outline",
    "vim.statusBarColorControl": true,
}
```

### その他注意点

- _VSCodeVim_ の Undo 履歴管理はちょっと挙動があやしいので VS Code 標準のキーバインド（`Cmd+Z`, `Cmd+Shift+Z`）を利用するのがオススメです

## 公開後の反応

昨年ひっそりリリースしてから1年以上経っているわけですが、ありがたいことに反応もあったようなのでいくつかピックアップしておきます。


<blockquote class="twitter-tweet"><p lang="ja" dir="ltr"><a href="https://twitter.com/hashtag/%E4%BB%8A%E6%97%A5%E3%81%AEVSCode?src=hash&amp;ref_src=twsrc%5Etfw">#今日のVSCode</a><br>Extensionをながめていたらviemacsというすてきなものがあった。Vim+Emacsである。<a href="https://t.co/fQgcDc2pgz">https://t.co/fQgcDc2pgz</a></p>&mdash; 結城浩 (@hyuki) <a href="https://twitter.com/hyuki/status/1083686907203117056?ref_src=twsrc%5Etfw">January 11, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
なんと、あの結城先生が言及してくれているではないですか！！（感激）

---

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr">VimacsはVimでEmacsｷｰﾊﾞｲﾝﾄﾞを使えるようにするやつだけど、VSCodeでVimのｷｰﾊﾞｲﾝﾄﾞをやるやつは活発に作られてるけど、Emacsのはなんか今いちだから（？）VSCodeのVimプラグインの上に乗っかったVimacsが出てきた…？</p>&mdash; Hideyuki Tanaka (@tanakh) <a href="https://twitter.com/tanakh/status/1019622585074503680?ref_src=twsrc%5Etfw">July 18, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
理由はちょっと違いますが・・・

---
[![](/assets/images/posts/1bd494a8576c3fe73994e5da7388c81d.png)](https://marketplace.visualstudio.com/items?itemName=migrs.vimacs&ssr=false#review-details)
少ないですがポジティブなレビューはやはり嬉しいものです
