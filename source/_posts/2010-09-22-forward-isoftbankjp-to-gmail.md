---
layout: post
categories: ruby gmail iphone
title: i.softbank.jp 宛のメールを Gmail に転送する
---
i.softbank.jp メールは転送する手段が用意されていないのでスクリプトを自作した。
(i.softbank.jp メールは使ってないけど)

<!--more-->

``` ruby source http://gist.github.com/591166 gist
require 'net/imap'
require 'time'

sb_account = %W(USERNAME PASSWORD)
gm_account = %W(USERNAME PASSWORD)

sb = Net::IMAP.new 'imap.softbank.jp', 993, true
sb.login *sb_account
sb.select 'INBOX'

if ids = sb.search(%w(UNSEEN)) and ids.size > 0
  gm = Net::IMAP.new 'imap.gmail.com', 993, true
  gm.login *gm_account

  bodys = %w(BODY[HEADER] BODY[TEXT])
  sb.fetch(ids, bodys + %w(ENVELOPE)).each do |mail|
    ev = mail.attr['ENVELOPE']
    date = Time.parse(ev.date)
    puts %!#{date} | #{'%-30.30s' % "#{ev.from[0].mailbox}@#{ev.from[0].host}"} | #{ev.subject && ev.subject.toutf8}!
    gm.append 'INBOX', bodys.map{|b|mail.attr[b]}.join, nil, date
  end
  puts "#{ids.size} mail(s) forwarded."
end
```
