---
layout: post
tags: [python, osx]
title: Python で UnocodeDecodeError
---
以前もハマったことがあるのでメモ。

    UnicodeDecodeError: 'ascii' codec can't decode byte 0xe3 in position 27: ordinal not in range(128)

のようなエラーには、

`/Library/Python/2.6/site-packages/sitecustomize.py`

``` python
import sys
sys.setdefaultencoding("utf-8")
```

というファイルを作成するとこで解決。

ワンライナで対応するには、以下を実行しましょう。

    echo 'import sys\nsys.setdefaultencoding("utf-8")' | sudo tee /Library/Python/2.6/site-packages/sitecustomize.py
