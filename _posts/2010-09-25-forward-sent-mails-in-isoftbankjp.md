---
layout: post
tags: ruby gmail iphone
title: i.softbank.jp の送信メールも Gmail に転送する
---
[i.softbank.jp 宛のメールを Gmail に転送する](/2010/09/22/forward-isoftbankjp-to-gmail.html) の続き。

* 受信メールだけではなく送信メールも対象にして転送させることで全部 Gmail で見れるようにしたい。
* しかも転送ではなく移動してしまった方が二重で管理する必要もなくスッキリしているような気がしたのでそういう実装にしてみた。
* また、Inbox にメールを attach するだけだと、[boxcar](http://http://boxcar.io/) が反応してくれないので、直接通知するようにした。

{% highlight ruby %}
SB_ACCOUNT = ['USERNAME', 'PASSWORD']
GM_ACCOUNT = ['USERNAME', 'PASSWORD']
BOXCAR_ADDR = "123456.123456@push.boxcar.io"

sb.select 'INBOX'
imap_each(sb, %w(UNDELETED)) do |mail, m|
  Net::SMTP.start('127.0.0.1', 25) {|smtp| smtp.send_mail mail.attr['BODY[HEADER]'], m[:from], BOXCAR_ADDR}
  gm.append 'INBOX', m[:src], nil, m[:date]
  sb.store mail.seqno, '+FLAGS', [:Deleted]
end

sb.select 'Sent Messages'
imap_each(sb, %w(UNDELETED)) do |mail, m|
  gm.append '[Gmail]/Sent Mail', m[:src], [:Seen], m[:date]
  sb.store mail.seqno, '+FLAGS', [:Deleted]
end

BEGIN {
  require 'net/imap'
  require 'net/smtp'
  require 'time'

  def sb; @sb ||= imap_login 'imap.softbank.jp', *SB_ACCOUNT; end
  def gm; @gm ||= imap_login 'imap.gmail.com',   *GM_ACCOUNT; end

  def imap_login host, id, pw
    imap = Net::IMAP.new host, 993, true
    imap.login id, pw
    imap
  end

  def imap_each imap, search
    bodys = %w(BODY[HEADER] BODY[TEXT])
    if ids = imap.search(search) and ids.size > 0
      imap.fetch(ids, bodys + %w(ENVELOPE)).each do |mail|
        ev = mail.attr['ENVELOPE']
        yield mail, { :date => Time.parse(ev.date),
            :src => bodys.map{|b|mail.attr[b]}.join,
            :from => "#{ev.from[0].mailbox}@#{ev.from[0].host}"
          }
      end
    end
  end
}
{% endhighlight %}

Gmail の言語設定を日本語にすると、IMAPフォルダも日本語になってしまうので注意が必要
