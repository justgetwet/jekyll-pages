---
layout: post
title: パリミューチュアル方式のシュミレート
---

日本の公営競技は、全てパリミューチュアル方式により投票券が販売されている。パリミューチュアル方式は投票券の総売り上げをプールし、興行主はそこから一定割合を差し引き残りの金額を勝ち投票券に配分する方法。興行主の取り分を決める割合は控除率と呼び、賭式により20％～30％が設定されている。

興行主の取り分である控除率は、より低く設定された賭式がベッターにとり有利である。具体的には競馬の単勝・複式

パリミューチュアル方式のモデルは、競技結果の的中率に関わらずベッターは控除率分の負債を追う。

14頭立てのレースで常に1番の馬に掛けた場合の100万回のシュミレート

```python
import numpy as np
from numpy.random import default_rng
rng = default_rng()

DEDUCTION = 0.8
RACERS = 14
BETTORS = 1000
TRIAL = 1000000

races = rng.integers(1, RACERS+1, size=(TRIAL, BETTORS))
bet = 100
payout = 0
for race in races:
    votes = np.sum(race==1)
    p = votes/BETTORS
    odds = BETTORS * DEDUCTION/votes
    win = rng.choice([1, 0], p=[p, 1-p])
    if win:
        payout += odds * bet

invest = TRIAL * bet
rate = payout/invest
print(rate)
```
