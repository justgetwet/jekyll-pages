---
layout: post
title: ヘッダーとSNSアイコン
---

もにょもにょ

### ヘッダーのアイコン

もにょもにょ



### mo

```md
---
layout: page
title: "404"
permalink: /404.html
---

### Page not found! :(
```

mo

```html
---
layout: default
---
<main>
  <div class="caption">
    <h3>{% raw %}{{ page.title }}</h3>
  </div>
  <article>
    {{ content }}{% endraw %}
  </article>

</main>
```