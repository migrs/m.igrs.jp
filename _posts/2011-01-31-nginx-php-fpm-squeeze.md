---
layout: post
categories: php nginx debian
title: Debian Squeeze で nginx + php-fpm
---

<http://php-fpm.org/>
> **Jul 22, 2010**
> PHP 5.3.3 is released and now bundles PHP-FPM

Debian Squeeze に入っているのは PHP 5.3.3 なのだが何故か php5-fpm パッケージが存在しないかったので
ここ([PHP 5.3.5, now for Squeeze](http://www.dotdeb.org/2011/01/11/php-5-3-5-now-for-squeeze/)) にあるパッケージを利用した。

<!--more-->

    sudo aptitude install php5-fpm

