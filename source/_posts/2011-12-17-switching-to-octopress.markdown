---
layout: post
title: "switching to octopress"
date: 2011-12-17 00:46
comments: true
categories: 
---

しばらくの間 [github パクリデザイン](http://gyazo.com/085cca9f560924d7357df4cf75743164)でしたが、
[レイアウト崩れて](http://gyazo.com/5a49da61cbd3f87582562f5739f9b9f4)きてしまった(リソース直接参照してました。すいません...)、
ので変更することにしました。

ということで今回採用したのが [octopress](http://octopress.org) というブログエンジンです。

## octopress とは
{% img http://gyazo.com/b4b39d29e0f26e05cf211deab638554f.png 629 196 octopress %}
<http://octopress.org/>

簡単に言えば [jekyll](http://jekyllrb.com/) にデザイン載せて便利にしたようなブログエンジンです。  
jekyll 自体に手を加えているわけではなく、jekyll を利用したフレームワークといった感じ。

### 特徴
- HTML5 / CSS3 でデザインもイケてるデフォルトテンプレート
- スマートフォン対応 ([320 and up](http://stuffandnonsense.co.uk/projects/320andup/) 採用)
- 外部サイト連携 ([Twitter](http://twitter.com/), [Google Plus](http://plus.google.com/), [Disqus](http://disqus.com/), [Pinboard](http://pinboard.in/), [Delicious](http://delicious.com/), [Google Analytics](http://www.google.com/analytics/))
- [Github pages](http:/pages.github.com/) や任意のサーバへの簡単なデプロイの提供
- [Pow](http://pow.cx/) / [Rack](http://rack.rubyforge.org/) 対応
- [Compass](http://compass-style.org/) / [Sass](http://sass-lang.com/) を利用したテーマ
- [Solarized](http://ethanschoonover.com/solarized) によるキレイなシンタックスハイライト

jekyll の思想や仕組みは好きだが、実際それなりのデザインにするのは難しいと感じていた私のような(なのでパクった)人に octopress は良いと思う。  
実際、移行もサクっとできた。

WordPress / Movable Type 等他ブログからの移行については jekyll 自体が対応している。See, [Blog Migrations](https://github.com/mojombo/jekyll/wiki/blog-migrations)

## Get Start
セットアップに関しては [Octopress Setup](http://octopress.org/docs/setup/) にあるとおりでハマリ所もないので省略。
**Ruby 1.9.2 必須** なのでそこだけ注意。
ちなみに私は [rbenv](https://github.com/sstephenson/rbenv) を利用してます。

### ローカルプレビュー
上記セットアップさえすればすぐデザインを確認できます。

ローカル環境で表示を確認したい場合は、

    rake preview

でサーバが立ち上がるので <http://localhost:4000/> で確認できます。
jekyllの場合の `jekyll --server` と同じですね。

octopress は [Pow](http://pow.cx/) (というか [Rack](http://rack.rubyforge.org/))にも対応しているのでマカーで Pow 使ってる人は `rake preview` しなくても `http://[SITENAME].dev` で確認できます。


ファイルの変更を自動で反映させるには、

    rake watch

します。 `jekyll --auto` オプションと同じです。

### 基本的な設定
jekyll の設定ファイルである [_config.yml](https://github.com/imathis/octopress/blob/master/_config.yml) を編集します。  
特にこだわら無いのであれば、

- [Main Configs](https://github.com/imathis/octopress/blob/master/_config.yml#L2)
- [3rd Party Settings](https://github.com/imathis/octopress/blob/master/_config.yml#L57)

あたりをちょろっと変更するくらいで大丈夫です。  
設定の変更は `rake watch` では反映されないようなので必要に応じて再実行しましょう。


### 記事の投稿

    rake new_post["switching to octopress"]

すると`source/_posts/2011-12-17-switching-to-octopress.markdown` が生成されるのでこれを編集します。
デフォルトは markdown ですが [Rakefile](https://github.com/imathis/octopress/blob/master/Rakefile) で設定変更できます。


### デプロイ
自分のサーバ等にデプロイする場合は [Rakefile](https://github.com/imathis/octopress/blob/master/Rakefile) の `ssh_user`, `document_root` あたりを変更します。  

Github pages を利用する場合は、

    rake setup_github_pages

することで `Rakefile` や `_config.yml` の設定部分が書き変わるので直接変更する必要はありません。

そして、

    rake deploy

することで本番環境にページが反映されます。

ただ Github pages デプロイ機能は毎回リポジトリ削除してから新規作成するようなのでコミット履歴が残らないのがちょっと残念。

## 感想
デフォルトでここまでデザインできているのはうれしいね！  
他にもいろいろ紹介したい機能等あるけど今回はとりあえずここまで。

## 参考
### rake タスク一覧
    rake clean                 # Clean out caches: .pygments-cache, .gist-cache, .sass-cache
    rake copydot[source,dest]  # copy dot files for deployment
    rake deploy                # Default deploy task
    rake gen_deploy            # Generate website and deploy
    rake generate              # Generate jekyll site
    rake install[theme]        # Initial setup for Octopress: copies the default theme into the path of Jekyll's ge...
    rake integrate             # Move all stashed posts back into the posts directory, ready for site generation.
    rake isolate[filename]     # Move all other posts than the one currently being worked on to a temporary stash l...
    rake list                  # list tasks
    rake new_page[filename]    # Create a new page in source/(filename)/index.markdown
    rake new_post[title]       # Begin a new post in source/_posts
    rake preview               # preview the site in a web browser
    rake push                  # deploy public directory to github pages
    rake rsync                 # Deploy website via rsync
    rake set_root_dir[dir]     # Update configurations to support publishing to root or sub directory
    rake setup_github_pages    # Set up _deploy folder and deploy branch for Github Pages deployment
    rake update_source[theme]  # Move source to source.old, install source theme updates, replace source/_includes/...
    rake update_style[theme]   # Move sass to sass.old, install sass theme updates, replace sass/custom with sass.o...
    rake watch                 # Watch the site and regenerate when it changes

