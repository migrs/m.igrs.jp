---
layout: post
categories: vim emacs
title: Vim Insert mode で Emacs Key Binding を使う
---
編集効率では Vim の方が上だけど、新規でテキスト書く時は Emacs が良いと思っている Vim ユーザなのですが、以下の設定を .vimrc に追加してます。

<!--more-->

インサートモードで Emacs Key Bindings
``` vim
imap <silent> <C-P> <Up>
imap <silent> <C-N> <Down>
imap <silent> <C-B> <Left>
imap <silent> <C-F> <Right>
imap <silent> <C-A> <Home>
imap <silent> <C-E> <End>
imap <silent> <C-D> <Del>
imap <silent> <C-K> <C-O>D
imap <silent> <C-Y> <C-R>"
```

コマンドモードで Emacs Key Bindings
``` vim
cmap <C-P> <Up>
cmap <C-N> <Down>
cmap <C-B> <Left>
cmap <C-F> <Right>
cmap <C-A> <Home>
cmap <C-E> <End>
cmap <C-D> <Del>
cmap <C-Y> <C-R>"
cmap <Esc><C-B> <S-Left>
cmap <Esc><C-F> <S-Right>
```

Cocoa のテキストフィールド程度の Emacs Key が対応しているだけで結構幸せになれます。
