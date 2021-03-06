---
layout: post
title: Overview
---

2022年1月1日〜6月10日のデータ

```python
# overview.py
import datetime
import pandas as pd
import pickle
import re

def slash_dt(s):
    # "0101" -> "01/01"
    return datetime.datetime.strptime(s, "%m%d").strftime("%m/%d")

filepath = "./data/" + "races_2022.pickle"
with open(filepath, "rb") as f:
    races = pickle.load(f)

print("2022/" + slash_dt(races[0][0]), "->", slash_dt(races[-1][0]), len(races), "races", "\n")

# 距離
distances = [race[3] for race in races]
df = pd.DataFrame(distances, columns=("distance",))
print(df['distance'].value_counts()[:8], "\n")

# クラス
_3, c3, c2, c1, b = 0, 0, 0, 0, 0
for i, race in enumerate(races):
    dt, r, racename, dist, head_count, condition, code = race
    if not re.match("３歳新馬", racename) and (re.match("３歳\(", racename) or re.match("３歳", racename)):
        # print(dt, r, racename)
        _3 += 1
    if re.match("Ｃ３\(", racename):
        # print(dt, r, racename)
        c3 += 1
    if re.match("Ｃ２\(", racename):
        # print(dt, r, racename)
        c2 += 1
    if re.match("Ｃ１\(", racename):
        # print(dt, r, racename)
        c1 += 1
    if re.match("Ｂ１\(", racename) or re.match("Ｂ２\(", racename) or re.match("Ｂ３\(", racename):
        # print(dt, r, racename)
        b += 1

d = {"3old": _3, "C3": c3, "C2": c2, "C1": c1, "B": b}
for k, v in zip(d.keys(), d.values()):
    print(k.ljust(5), str(v).rjust(4), str(round(v/len(races), 2)).rjust(6))

# % python overview.py
# ->
# 2022/01/01 -> 06/10 1375 races
#
# 1,400m（外）    364
# 1,200m（外）    309
# 1,500m（外）    220
# 1,600m（内）    148
# 1,600m（外）     86
# 900m（外）       54
# 2,000m（外）     50
# 800m（外）       37
# Name: distance, dtype: int64
#
# 3old   176   0.13
# C3     186   0.14
# C2     182   0.13
# C1      76   0.06
# B       12   0.01
```
