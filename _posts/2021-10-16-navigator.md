---
layout: post
title: ナビゲーション
---

もにょもにょ

### 記事ページのアイコン

heroiconsは、CSSフレームワーク[tailwindcss](https://tailwindcss.com/)が提供するアイコン集。次の手順でアイコンファイルを作成する。

1. _includeディレクトリ下に _iconsディレクトリを作成する。
2. _iconsディレクトリ下に、chevron-left.svg、chevron-right.svgの空ファイルを作成する。
3. [heroicons](https://heroicons.com/)へアクセスし、右のSolidアイコンからchevron-leftを選択。
4. アイコンにマウスを当て、Copy SVGの表示をクリックし、ソースをコピーする。
5. 作成したchevron-left.svgへソースを貼り付ける。
6. 同様にchevron-right.svgへコピーしたソースを貼り付ける。


### Navigation

もにょもにょ

_include/nav.html
```html
<nav>
    {% raw %}{% if page.previous %}
    <div>{%- include icons/arrow-sm-left.svg -%}</div>
    <a href="{{ page.previous.url | relative_url }}" title="Previous Post: {{page.previous.title}}">
      PREV
    </a>
  {% endif %}
  <div class="blank"></div>
  {% if page.next %}
    <a href="{{ page.next.url | relative_url }}" title="Next Post: {{page.next.title}}">
      NEXT
    </a>
    <div>{%- include icons/arrow-sm-right.svg -%}</div>
  {% endif %}{% endraw %}
</nav>

```

