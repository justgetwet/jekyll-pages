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


```python
from time import sleep
from selenium import webdriver
from selenium.webdriver.chrome import service as fs

from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.ui import WebDriverWait
from selenium.common.exceptions import TimeoutException

# import sys

inet_id = 'CWUYACZB'
member_id = '11065494'
p_ars = '7662'
pw = '5852'

DRIVER = "../python-chromedriver-binary-103.0.5060.53.0-py38h50d1736_0/lib/python3.8/site-packages/chromedriver_binary/chromedriver"
chrome_service = fs.Service(executable_path=DRIVER)
browser = webdriver.Chrome(service=chrome_service)

url = "https://n.ipat.jra.go.jp/"
# url = "http://www.ipat.jra.go.jp/"
browser.get(url)


for _ in range(3):
    try:
        WebDriverWait(browser, 15).until(EC.presence_of_all_elements_located((By.TAG_NAME, 'h1')))
        sleep(1)
    except TimeoutException as te:
        print("timeout excepion: ", te)
    else:
        break
else:
        browser.close()
        # sys.exit()

if browser.find_element(By.TAG_NAME, "h1").text == "お知らせ":
    print("The site is closed.")
    sleep(1)
    browser.close()
# else:
#     browser.find_element_by_name('inetid').send_keys(inet_id)
#     browser.find_element_by_class_name('button').click()
#     sleep(1)
#     browser.find_element_by_name('i').send_keys(member_id)
#     browser.find_element_by_name('r').send_keys(p_ars)
#     browser.find_element_by_name('p').send_keys(pw)
#     browser.find_element_by_class_name('buttonModern').click()

# sleep(1)
# browser.close()
```
