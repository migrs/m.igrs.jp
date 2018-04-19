---
layout: post
title: Setup Jekyll and GitHub Pages Again
---

これまで[さくらのVPS](https://vps.sakura.ad.jp/)で運用していたのですが、更新忘れて契約が切れいつの間にかサーバ毎消えてしまっていました。
8ヶ月ほどサイトダウンしていたようです。
それまで利用していた [Octopress](http://octopress.org/) もすっかり息を潜めたのでこれを気に原点に戻って素の [Jekyll](https://jekyllrb.com/) ベースで構築し直しました。

<!--more-->

## 構成

今回はメンテナンスレスにしたかったので [GitHub Pages](https://pages.github.com/) でホスティングすることにしました。  

`_site => ../migrs.github.io`

のようシンボリックリンク貼って、コンテンツの出力先を GitHub Pages のディレクトリに設定しておき、あとは、

1. 記事書いて
2. `bundle exec jekyll build` して
3. `migrs.github.io` で変更コミットして
4. `git push`

で記事の公開完了です。

最近、小ネタ溜まってきてるのでちょいちょい更新していこうかなと。

### リポジトリ

- [Jekyll プロジェクト](https://github.com/migrs/m.igrs.jp)
- [生成されたコンテンツ](https://github.com/migrs/migrs.github.io)
