---
layout: post
title: 基本のデータ
---
s
```python
ua = {"User-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.57"}
from bs4 import BeautifulSoup
import pandas as pd
import pickle
import re
import requests

def get_soup(url):
    try:
        res = requests.get(url, headers=ua)
    except requests.RequestException as e:
        print("Error: ", e)
    else:
        return BeautifulSoup(res.content, "html.parser")

def get_dfs(url):
    dfs = []
    soup = get_soup(url)
    if soup:
        if soup.find("table"):
            dfs = pd.io.html.read_html(soup.prettify())
        else:
            print(f"It's no table! {url}")
    return dfs

if __name__ == "__main__":

```



urlに、日付 + コースコード + 開催コード + レース番号

日付, コース, 開催コードのタプルを作成し、リスト化する。

```python
def strj(x):
    return str(x).rjust(2, "0")

races = []
races += [(f"01{strj(i)}", "川崎", f"11{strj(i)}") for i in range(1, 5)]
races += [(f"01{strj(i)}", "川崎", f"11{strj(i-1)}") for i in range(6, 8)]
races += [(f"01{strj(i+9)}", "船橋", f"10{strj(i)}") for i in range(1, 6)]
# print(races[0])
# ("0101", "川崎", "1101")
```

for で回す

```python
data = []
for i, (dt, course, hold) in enumerate(races):
    for n in range(1, 13):
        race = str(n).rjust(2, "0")
        target_code = dt + course_d[course] + hold + race

        result_url = nankan_url + "/result/" + yyyy + target_code + ".do"
        dfs = get_dfs(result_url)
        if not dfs: # レースなし
            print(f"{dt} {race}R is nothing..")
            continue
        else:
            df = dfs[0]
            if not df.columns[0] == "着": # 結果なし
                print(f"{dt} {race}R has no result..")
                continue
        df = [df for df in dfs if df.columns[0] == "天候"][0]
        condition = df["天候"][0] + "/" + df["馬場"][0].split()[1]

        raceno = course + " " + race + "R"

        info_url = nankan_url + "/race_info/" + yyyy + target_code + ".do"
        soup = get_soup(info_url)
        racename = soup.select_one("span.race-name").text
        racename = re.sub("\u3000", " ", racename).strip()

        tag = soup.select_one("div#race-data01-a")
        dist = tag.select_one("a").text.strip()
        dist = dist.strip("ダ")

        entry_df = get_dfs(info_url)[0]
        head_count = str(len(entry_df)) + "頭"

        t = dt, raceno, racename, dist, head_count, condition, target_code
        print(t)
        data.append(t)
```

pickleする

```python
filename = "./data/" + "races_2022.pickle"
with open(filename, "wb") as f:
    pickle.dump(data, f, pickle.HIGHEST_PROTOCOL)
```
