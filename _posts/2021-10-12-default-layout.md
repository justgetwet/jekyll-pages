---
layout: post
title: デフォルトレイアウト
---

ヘッダーファイルとフッターファイルを作成し、基本レイアウトに組み込む。そしてスタイルを当てる。<br/><br/>
ここにYAMLデータとLiquidテンプレートの利用、Sassによるスタイリングの一連の流れを見ることが出来る。

### _config.ymlへサイト名を記述
***

ルートの`_config.yml`は、サイト全体の情報を管理するファイル。titleに、サイト名"Jekyll Pages"を記述する。

_config.yml
```yml
url: ""
baseurl: "" 
title: "Jekyll Pages"
```

サイト名は、他のファイルから `{% raw %}{{ site.title }}{% endraw %}` でアクセスできる。

### ヘッダー
***

 _includeディレクトリ下に`header.html`を作成し、h1タグでサイト名を表示させる。

_include/header.html
```html
<header>
  <h1>{% raw %}{{ site.title }}{% endraw %}</h1>
</header>
```

### フッター
***

_include/footer.html
```html
<footer>
  &copy; to me
</footer>
```

### デフォルトのレイアウト
***

DFAULTレイアウトのテンプレート`default.html`の`<body>..</body>`内に`header.html`と`footer.html`を組み込む。

_layouts/default.html
```html
<!DOCTYPE html>
<html lang="{% raw %}{{ site.lang | default: 'en-US' }}{% endraw %}">
  <head>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta charset="utf-8">
    <title>{% raw %}{{ page.title }}{% endraw %} - {% raw %}{{ site.title }}{% endraw %}</title>
    <link rel="stylesheet" href="{{ "/assets/css/main.css" | relative_url }}">
  </head>
  <body>
    {% raw %}{% include header.html %}
    
    {{ content }}
    
    {% include footer.html %}{% endraw %} 
  </body>
</html>

```

### スタイリング
***

`main.scss`へ追記する。利用しているSassの記法は、変数とネスト。

_sass/main.scss
```scss
$blue: #092237;

body {
  margin: 0;
  text-align: center;
}

header {
  height: 20rem;
  background: $blue;
  h1 {
    margin: 0;
    line-height: 20rem;
    font-size: 3rem;
    color: $backgroundColor;
  }
}
```

### ローカルサーバをリスタート
***

`_config.yml`の変更を反映させるためリスタートする

![ready to go]({{site.url}}{{site.baseurl}}/assets/images/top-page1.jpg)


