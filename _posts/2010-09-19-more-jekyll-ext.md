---
layout: post
tags: [jekyll]
title: more jekyll ext
---
昨日に引き続き[jekyll_ext](http://github.com/rfelix/jekyll_ext)のお試し。

[my_jekyll_extensions](http://github.com/rfelix/my_jekyll_extensions) の中から


* [archive_gen](http://github.com/rfelix/my_jekyll_extensions/tree/master/archive_gen/)
  - 年／月／日毎にアーカイブページを生成する
  - [年](/2010/) ([_layout/archive_yearly.html](http://github.com/migrs/migrs.github.com/blob/master/_layouts/archive_yearly.html))
  - [月](/2010/09/) ([_layout/archive_monthly.html](http://github.com/migrs/migrs.github.com/blob/master/_layouts/archive_monthly.html))
  - [日](/2010/09/19/) ([_layout/archive_daily.html](http://github.com/migrs/migrs.github.com/blob/master/_layouts/archive_daily.html))
* [tag_gen](http://github.com/rfelix/my_jekyll_extensions/tree/master/tag_gen/)
  - 記事にタグが付けられる
    + `tags: hoge foo bar` のようにスペース区切りで
  - [tag page](/tags/jekyll/) ([_layouts/tag_index.html](http://github.com/migrs/migrs.github.com/blob/master/_layouts/tag_index.html))
  - [tag cloud](/tags/) ([tags/index.html](http://github.com/migrs/migrs.github.com/blob/master/tags/index.html))
* [categories_in_posts](http://github.com/rfelix/my_jekyll_extensions/tree/master/categories_in_posts/)
  - `_posts/` 以下にディレクトリを作成することでカテゴリー分けすることができる(未使用)
* [category_gen](http://github.com/rfelix/my_jekyll_extensions/tree/master/category_gen/)
  - カテゴリー別のページを生成する
  - まだ記事にカテゴリー付けてないのでサンプル無し
  - [category list](/categories/) ([categories/index.html](http://github.com/migrs/migrs.github.com/blob/master/categories/index.html))
* [tag_category_iterator](http://github.com/rfelix/my_jekyll_extensions/tree/master/tag_category_iterator/)
  - `site.tags` や `site.categories` が使えるようになる


これでだいぶブログっぽくなってきた。
