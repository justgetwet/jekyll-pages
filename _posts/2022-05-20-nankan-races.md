---
layout: post
title: "１ヶ月のレース内訳"
---

2022年4月のデータを調べる。

```python
ua = {"User-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.57"}
from bs4 import BeautifulSoup
import pandas as pd
import pickle
import re
import requests

nankan_url =  "https://www.nankankeiba.com"
course_d = { "浦和": "18", "船橋": "19", "大井": "20", "川崎": "21" }
eng_d = { "18": "urawa", "19": "funabashi", "20": "ooi", "21": "kawasaki" }
yyyy = "2022"

def get_soup(url):
    res = requests.get(url, headers=ua)

    return BeautifulSoup(res.content, "html.parser")

def get_dfs(url):
    soup = get_soup(url)
    dfs = []
    if soup.find("table"):
        dfs = pd.io.html.read_html(soup.prettify())
    else:
        print(f"it's no table! {url}")
    return dfs

if __name__ == "__main__":

    srj = lambda i: str(i).rjust(2, "0")
    # month = [("0401", "大井", "0101")] # 中止
    def april_races():
        month = [(f"04{srj(i+4)}", "川崎", f"01{srj(i+1)}") for i in range(5)]
        month += [(f"04{srj(i+11)}", "船橋", f"01{srj(i+1)}") for i in range(5)]
        month += [(f"04{srj(i+18)}", "大井", f"02{srj(i+1)}") for i in range(5)]
        month += [(f"04{srj(i+25)}", "浦和", f"01{srj(i+1)}") for i in range(5)]

        return month

    def get_racename(info_url):
        soup = get_soup(info_url)
        number_of_horses = len(soup.select("td.titi-haha"))
        dist_tag = soup.select_one("div#race-data01-a")
        distance = dist_tag.select_one("a").text.strip()
        title = soup.select_one("span.race-name").text
        title = re.sub("　| ", "", title)
        date = info_url[42:-11]
        racename = date + " " + course + " " + race + "R" + " " + title
        racename +=  " " + distance + " " + str(number_of_horses) + "頭"

        return racename

    races = april_races()
    racenames = []
    for i, (dt, course, hold) in enumerate(races):
        if i > -1:
            for race in (srj(n) for n in range(1, 13)):
                target = dt + course_d[course] + hold + race + ".do"
                info_url = nankan_url + "/race_info/" + yyyy + target
                racename = get_racename(info_url)
                print(racename)
                racenames.append(racename)

    filename = "./data/" + "april" + "_racenames.pickle"
    with open(filename, "wb") as f:
        pickle.dump(racenames, f, pickle.HIGHEST_PROTOCOL)

```


```python
def class_counts(racenames):
    race_class = "２歳", "３歳", "Ｃ", "Ｂ", "Ａ", "Ｊｐｎ", "オープン",
    each_class = []
    for racename in racenames:
        found = False
        for i, c in enumerate(race_class):
            if c in racename:
                if not found:
                    each_class.append(i)
                    found = True

    print("length:", len(racenames), "->", len(each_class))
    srs = []
    for i in range(len(race_class)):
        items = race_class[i], each_class.count(i)
        sr = pd.Series(items, index=["Class", "Count"])
        srs.append(sr)

    pd.set_option('display.unicode.east_asian_width', True)
    df = pd.DataFrame(srs)
    print(df)

if __name__ == "__main__":

    filepath = "./data/april_racenames.pickle"
    with open(filepath, mode="rb") as f:
        racenames = pickle.load(f)

    class_counts(racenames)

# 出力
  length: 240 -> 240
        Class  Count
  0      ２歳      1
  1      ３歳     55
  2        Ｃ    136
  3        Ｂ     36
  4        Ａ      3
  5    Ｊｐｎ      2
  6   オープン      7
```

```python
def dist_count(racenames):
    c_racenames = [name for name in racenames if "Ｃ" in name]
    print("length:", len(c_racenames))
    dist_l = []
    for racename in c_racenames:
        s_dist = racename.split()[-2].strip("ダ").split("m")[0]
        dist = int(s_dist.replace(",", ""))
        dist_l.append(dist)
    distance = sorted(set(dist_l))
    srs = []
    for dist in distance:
        items = dist, dist_l.count(dist)
        sr = pd.Series(items, index=("Distance", "Count"))
        srs.append(sr)

    df = pd.DataFrame(srs)
    print(df)

if __name__ == "__main__":

    filepath = "./data/april_racenames.pickle"
    with open(filepath, mode="rb") as f:
        racenames = pickle.load(f)

    class_counts(racenames)

# 出力
length: 136
    Distance  Count
0        800      5
1        900      6
2       1000      2
3       1200     27
4       1300      1
5       1400     36
6       1500     31
7       1600     17
8       1650      1
9       1700      1
10      1800      1
11      2000      6
12      2200      2

```

Cクラスの1400m, 1500m, 1600m の94レースを対象とする。
