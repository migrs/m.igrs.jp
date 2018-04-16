---
layout: post
title: "Pow をもっと便利に使うためのツール比較 - Powder / Powify Comparison"
date: 2012-01-16 09:30
comments: true
categories: pow
---

Mac and Ruby なウェブ開発者必携、[37signals](http://37signals.com/) 謹製の非常に便利な [Pow](http://pow.cx) ですがみなさん活用してますか？

{% img center http://pow.cx/images/logo-pow.png 410 300 pow %}

私はいわゆるプログラマーと呼ばれる人だけではなく、ウェブデザイナーな人たちにこそ活用して欲しいプロダクトだと思っているのですがそのことについては置いておいて（また別途）
ここでは周辺ツールについて。

<!--more-->

Pow 自体非常にシンプルでサードパーティツールの類はほとんど必要ないのですが、
さらに便利に扱うためのツールが[マニュアル](http://pow.cx/manual.html)でいくつか[紹介](http://pow.cx/manual.html#section_4)されています。

ここにある二つのプロダクト
([Powder](https://github.com/Rodreegez/powder)/[Powify](https://github.com/sethvargo/powify))
が非常にクリソツ（死語）で何が違うのか一目では分からなかったので（自分の為にも）表にして比較してみた。

結論から言うと両者ほとんど同じ。Powify の方が若干高機能かな〜ってくらい。

## Powder / Powify Comparison

<table>
  <thead>
    <tr>
      <th width="45%" style="text-align:center;"><a href="https://github.com/Rodreegez/powder">Powder</a></th>
      <th width="55%" style="text-align:center;"><a href="https://github.com/sethvargo/powify">Powify</a></th>
    </tr>
  </thead>
  <tbody style="font-size:medium;">
    <tr>
      <th colspan="2"><strong style="font-size:x-large;">Server Commands</strong></th>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Install pow server ( <small><code>curl get.pow.cx | sh</code></small> )</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder install</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server install</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Reinstall pow server</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>-</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server reinstall</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Update pow server</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>-</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server update</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Uninstall pow server ( <small><code>curl get.pow.cx/uninstall.sh | sh</code></small> )</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder uninstall</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server uninstall</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">List all pow apps ( <small><code>ls -l ~/.pow/</code></small> )</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder list</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server list</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Start the pow server ( <small><code>launchctl load ~/Library/LaunchAgents/cx.pow.powd.plist</code></small> )</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder up</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server start</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Stop the pow server ( <small><code>launchctl unload ~/Library/LaunchAgents/cx.pow.powd.plist</code></small> )</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder down</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server stop</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Restart the pow server</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;">-</td>
      <td style="padding:0 0 10px 20px;"><code>powify server restart</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Updates hosts file to map pow domains to 127.0.0.1</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder host</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server host</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Removes pow domains from hostfile</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder unhost</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server unhost</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Shows current pow status</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder status</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server status</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Shows current pow configuration</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder config</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server config</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Tails the Pow log ( <small><code>tail -f ~/Library/Logs/Pow/access.log</code></small> )</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>-</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify server logs</code></td>
    </tr>

    <tr>
      <th colspan="2"><strong style="font-size:x-large;">App Commands</strong></th>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Create a pow app from the current directory ( <small><code>ln -s `pwd` ~/.pow/[NAME]</code></small> )</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder link [NAME]</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify create [NAME]</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Destroy the pow app served from the current directory ( <small><code>rm ~/.pow/[name]</code></small>)</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder unlink [NAME]</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify destroy [NAME]</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Clean up invalid symbolic link</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder cleanup</code></td>
      <td style="padding:0 0 10px 20px;"><code>-</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Restart pow app ( <small><code>touch tmp/restart.txt</code></small>)</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder restart</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify restart [NAME]</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Always restart pow app ( <small><code>touch tmp/always_restart.txt</code></small>)</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder always_restart</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify always_restart [NAME]</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Reset restart settings ( <small><code>rm tmp/always_restart.txt</code></small>)</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder no_restarts</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify always_restart_off [NAME]</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Rename the pow app to [NAME]</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>-</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify rename [NAME]</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Run the this pow app in a different environment</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>-</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify env [ENV]</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Open a pow in the browser</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder open</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify browse [NAME]</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Tail the application logs ( <small><code>tail -f ~/Library/Logs/Pow/apps/[NAME].log</code></small> )</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder log</code></td>
      <td style="padding:0 0 10px 20px;"><code>powify logs [NAME]</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Set this app as default (http://localhost/)</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder default</code></td>
      <td style="padding:0 0 10px 20px;"><code>-</code></td>
    </tr>

    <tr>
      <td colspan="2" style="color:#AAA;">Remove current default app</td>
    </tr>
    <tr>
      <td style="padding:0 0 10px 20px;"><code>powder un_default</code></td>
      <td style="padding:0 0 10px 20px;"><code>-</code></td>
    </tr>


  </tbody>
</table>

Non-Japanese な人向けに [gist](https://gist.github.com/1615032) も用意した。

## Conclusion

Powify には専用の管理アプリ([powify.dev](https://github.com/sethvargo/powify.dev))も用意されており、以下のコマンドで設置可能。
(今のところPow情報表示するだけのシンプルなもの)

  - <code>powify utils install</code>
  - <code>powify utils reinstall</code>
  - <code>powify utils uninstall</code>

敢えて言うなら、シンプルな Powder・高機能な Powify といった感じか？  
今のところ善し悪し微妙なので好き好きで！

### References

- [Rackアプリ開発するならPowはもう常識だよね～](http://d.hatena.ne.jp/marutanm/20110418/p1) [<img style="border:none;" src="http://b.hatena.ne.jp/entry/image/http://d.hatena.ne.jp/marutanm/20110418/p1">](http://b.hatena.ne.jp/entry/http://d.hatena.ne.jp/marutanm/20110418/p1)

