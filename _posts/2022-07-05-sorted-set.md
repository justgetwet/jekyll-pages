---
layout: post
title: 順序を保持しながら重複排除
---

s
```python
>>> a = 3,3,3,2,2,2,4,4,4
>>> set(a)
{2,3,4}
>>> sorted(set(a), key=a.index)
[2,3,4]
```

ループ内でリストの要素を削除する方法

スライスを使いコピーのリストでループ

```pythn
for e in ls[:]:
    if re.match("spam", e)
        ls.remove(e)

```

ss
