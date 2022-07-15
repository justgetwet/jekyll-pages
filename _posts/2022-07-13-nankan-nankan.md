---
layout: post
title: 南関南関
---

```shell
% conda install -c conda-forge selenium
% conda install -c conda-forge python-chromedriver-binary==103.0.5060.114
```

Chrome は最新の状態です
バージョン: 103.0.5060.114（Official Build） （x86_64）

https://anaconda.org/conda-forge/python-chromedriver-binary/files?page=1

osx-64/python-chromedriver-binary-103.0.5060.53.0-py38h50d1736_0.tar.bz2

展開したフォルダをpythonディレクトリに移動、そこにプログラム上からパスを指定して直接使う。

最初macは、「"chromedriver"は開発元を検証できないため開けません。」と吐く。
キャンセルし、システム環境設定 -> セキュリティとプライバシー -> 一般 を選び、
"chromedriver"は開発元を検証できないため、仕様がブロックされました。[このまま許可]


テスト

```python
from time import sleep
from selenium import webdriver

CHROMEDRIVER = "../../python-chromedriver-binary-103.0.5060.53.0-py38h50d1736_0/lib/python3.8/site-packages/chromedriver_binary/chromedriver"
browser = webdriver.Chrome(CHOROMEDRIVER)
sleep(1)
browser.close()
```

警告が出る。

DeprecationWarning: executable_path has been deprecated, please pass in a Service object
browser = webdriver.Chrome(CHOROMEDRIVER)

パスをサービスオブジェクトへ通せとのこと。

```python
from time import sleep
from selenium import webdriver
from selenium.webdriver.chrome import service as fs

CHROMEDRIVER = "../../python-chromedriver-binary-103.0.5060.53.0-py38h50d1736_0/lib/python3.8/site-packages/chromedriver_binary/chromedriver"
chrome_service = fs.Service(executable_path=CHROMEDRIVER)
browser = webdriver.Chrome(service=chrome_service)
sleep(1)
browser.close()
```
