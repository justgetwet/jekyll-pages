---
layout: post
title: simple viewer
---

5行程で

```python
# simpleviewer.py
import tkinter as tk
import sys

app = tk.Tk()

filename = sys.argv[1]
img = tk.PhotoImage(file=filename)

tk.Label(app, image=img).pack()
app.mainloop()
```

flj

```shell
$ python simpleviewer.py coffee.png
```

![chelsea]({{site.url}}{{site.baseurl}}/assets/images/coffee.png)


```shell
$ conda install -c anaconda scikit-image
```

jj

```python
# chelsea.py
from PIL import Image, ImageTk
import skimage
import tkinter as tk

app = tk.Tk()

arr = skimage.data.chelsea()
img = Image.fromarray(arr)
img = ImageTk.PhotoImage(img)

tk.Label(app, image=img).pack()
app.mainloop()
```
k
```shell
$ python chelsea.py
```
z

![chelsea]({{site.url}}{{site.baseurl}}/assets/images/chelsea.png)
