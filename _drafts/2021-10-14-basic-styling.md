---
layout: post
title: "基本のスタイリング"
render_with_liquid: false
---

ヘッダーとフッターを追加して基本レイアウトを作成する。

ディレクトリ _layoutsにある

基本レイアウトを作成する必要なディレクトリ、ファイルは次のとおり。

```shell
|-_includes
|-_layouts
  |-default.html
|-_sass
  |-main.scss
|
index.md
```

index.mdのfrotmatterに、layout: defaultが指定されている。

```markdown
---
layout: default
title: "Happy Jekylling!"
---

## You're ready to go!

Start developing your Jekyll website.
```

### 1. default.htmlの編集

rubyのテンプレートエンジンLiqidで、bodyタグ内へheader.htmlとfooter.htmlを組み込む。langもja-JPに書き換える。

```html
<!DOCTYPE html>
<html lang="{{ site.lang | default: "ja-JP" }}"> ♯ en-US -> ja-JP
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta charset="utf-8">
    <title>{{ page.title }} - {{ site.title }}</title>
    <link rel="stylesheet" href="{{ "/assets/css/main.css" | relative_url }}">
  </head>
  <body>
    {%- include header.html -%} # 追記

    {{ content }}
    
    {%- include footer.html -%} # 追記
  </body>
</html>
```

### 2. header.htmlの作成

monyomonyo

```html
<header>
  <h1>Jekyll Starter Blog</h1>
</header>
```

### 3. footer.htmlの作成

gekogeko

```html
<footer>
  <hr />
  <p>Powered by Jekyll</p>
</footer>
```

### 4. main.sassに追記

mknk

```sass
// main.sass
body {
  background: $backgroundColor;
  color: $bodyColor;
  font-family: $bodyFont;
  margin: 4rem; // 追記
  max-width: 650px; // 追記
}
```

### 5. dore

```html

      <div>{%- include_relative assets/icons/calendar.svg -%}</div>

```

