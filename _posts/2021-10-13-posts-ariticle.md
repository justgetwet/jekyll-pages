---
layout: post
title: POSTSとARTICLE 
render_with_liquid: false
---

もにょもにょ

### 投稿ページのテンプレート
***

`_layouts`下に、投稿記事のテンプレート`post.html`を作成する。

**_layout/post.html**

```html
---
layout: default
---

<main>
  <h3>ARTICLE</h3>
  <article>
    <h2>{{ page.title }}</h2>
    <hr/>
    <p>{{ page.date | date: "%b %d, %Y" }}</p>
    {{ content }}
  </article>
</main>
```

### index.md
***

`index.md`の中身は、次のように書き換える。

index.md
```html
---
layout: default
title: Top Page
---

<main>
  <h3>POSTS</h3>
  {% for post in site.posts %}
    <aside>
      <h3>
        <span>{{ post.date | date: "%b %d, %y"}}</span>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </h3>
    </aside>  
  {% endfor %}
</main>
```



### サンプルの投稿記事
***

`_posts`下に、`2021-12-01-first-post.md`というファイルを作成する。

- index.mdの内容をコピーペースト
- front matterの1行目、`layout: default`を`layout: post`へ変更
- front matterの2行目、`title: "Happy Jekylling!"`はコメントアウト

**_posts/2021-12-01-first-post.md**
```markdown
---
layout: post
title: "Happy Jekylling!"
---

## You're ready to go!

Start developing your Jekyll website.

```

### スタイリング
***

もにょもにょ

_sass/main.scss
```scss
$blue: #092237;

body {
  margin: 0;
}

header {
  height: 20rem;
  background: $blue;
  h1 {
    margin: 0 8rem;
    line-height: 20rem;
    font-size: 3rem;
    color: $backgroundColor;
  }
}

main, footer {
  margin: 0 8rem;
}
```

### ローカルサーバで確認
***

<br/>
![ready to go](../../../../jekyll-blog/assets/images/top-page2.jpg)

<br/>
![ready to go](../../../../jekyll-blog/assets/images/article-page1.jpg)


### 現時点のディレクトリ構成
***

```shell
├── _include
│    ├── footer.html
│    └── header.html
├── _layout
│    ├── default.html
│    └── post.html
├── _posts
│    └── 2021-12-01-first-post.md
├── _sass
│    └──  main.sass
 _config.yml
 index.md
```

