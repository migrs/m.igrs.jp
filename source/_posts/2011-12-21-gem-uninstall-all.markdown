---
layout: post
title: 全ての gem をアンインストール
date: 2011-12-21 11:17
comments: true
categories: ruby
---
`--all-installed` 的なオプションがありそうでないのでメモ  
(`--all` はあるけど特定の gem のすべてのバージョンを削除の意味)

<!--more-->

``` sh
gem uninstall -axI `gem list --no-versions`
```

- [rubygems](http://rubygems.org/)

