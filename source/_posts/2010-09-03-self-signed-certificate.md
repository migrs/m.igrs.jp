---
layout: post
categories: linux
title: Self Signed Certificate
---
何度やっても忘れるのでメモ

    openssl genrsa -des3 -out server.key 1024
    openssl rsa -in server.key -out server.key
    openssl req -new -x509 -key server.key -out server.crt
