---
layout: post
title: matplotlibのグラフをPILLOW画像へ変換
---

matplotlibで生成した複数のグラフを1枚の画像に落とし込む。

```python
import matplotlib.pyplot as plt
from matplotlib.backends.backend_agg import FigureCanvasAgg as FigureCanvas
from matplotlib.figure import Figure
from PIL import Image

fig = Figure()
canvas = FigureCanvas(fig)
ax = fig.gca()

ax.set_title("sin curve")
x = np.arange(-3, 3, 0.1)
y = np.sin(x)
ax.plot(x, y)

canvas.draw()
arr = np.frombuffer(canvas.tostring_rgb(), dtype='uint8')
arr = arr.reshape(fig.canvas.get_width_height()[::-1] + (3,))
img = Image.fromarray(arr)

img.save("sin_curve.png")

```
