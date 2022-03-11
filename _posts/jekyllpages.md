# Jekyll Pages

## 人気SSGからJekyllを選ぶ

静的サイトジェネレータ(SSG)は、Webサイトを静的なファイルとして生成するツール。[Site Generators](https://jamstack.org/generators/)というサイトを見ると、Reactベースのフレームワーク、GatsbyとNextが人気で、Go言語のHugoがそれに並ぶ。

次に人気のSSGが、ruby製のJekyll。Github Pagesのバックエンドに採用されているため、広く普及している。

### Jekyllの良さ

人気のReactベースSSGは、（ポエム）

Jekyllはシンプルで書き易く、Github Pagesを使えばシンプルに運用できる。rubyの設計思想なのか、少しずつ機能を足していくのが楽しい。

### このサイトは

Jekyllでシンプルなブログテーマを作成し、Github Pagesで運用する手順を記録したもの。

動作確認は、mac BigSur と windows10。

>Matz: So Ruby is designed to make programmers happy.
>[The Philosophy of Ruby](https://www.artima.com/articles/the-philosophy-of-ruby)


## インストールとプロジェクトの作成

Jekyllをインストールしてプロジェクトを導入する。rubyの環境構築が必要な場合は、[Ruby基礎](http://jekyllrb-ja.github.io/docs/ruby-101/)、[インストール](http://jekyllrb-ja.github.io/docs/installation/)などを参考に。

### Bundler
***

基本的に、JeykllはBundlerでインストールする。BundlerはRubyのGemパッケージ管理システムで、Ruby2.6（Dec 2018）から標準Gemになっている。

```shell
$ bundler --version
#-> Bundler version x.x.xx
```

Bundlerを初めて使う場合、Gemをインストールする場所 `vendor/bundle` を設定する。

```shell
$ bundle config path vendor/bundle
$ cd .bundle
$ cat config
#-> BUNDLE_PATH: "vendor/bundle"
```

Bunderの設定ファイル`config`は、ユーザディレクトリの .bundle の中に出来る。

### Jekyllのインストール
***

プロジェクトのディレクトリを作成し、`bundle init`コマンドでGemfileを生成する。

```shell
$ mkdir mysite
$ cd mysite
$ bundle init
```

Gemfileに、`gem "jekyll"` を追記して保存する。

&emsp;./Gemfile
```ruby
source "https://rubygems.org"

git_source(:github) { |repo_name| "https://github.com/#{repo_name}" }

gem "jekyll"
```

Gemfileの編集後、`bundle install`コマンドを実行する。

```shell
$ bundle install
```

### 空プロジェクトの作成
***

`bundle exec jekyll new`コマンドで新規プロジェクトを作成。

```shell
$ bundle exec jekyll new . --force --blank
```
- . \--force : 既存ディレクトリにソースを展開
- \--blank : 空プロジェクトを指定

空プロジェクトは以下のディレクトリ構成に展開される。

```shell
├── _data
├── _drafts
├── _include
├── _layout
│    └── default.html
├── _posts
├── _sass
│    └──  main.sass
├── _site
├── .jekyll-chache
├── assets
├── vendor
│
 _config.yml
 Gemfile
 Gemfile.lock
 index.md
```

### ローカルサーバの起動
***

`bundle exec jekyll server` を実行し、ローカル環境にjekyllを立ち上げる。

```shell
$ bundle exec jekyll server
#-> Server address: localhost:4000
#-> Server running... press ctrl-c to stop.
```

ブラウザのアドレスバーに`localhost:4000`を入力する。

![ready to go]({{site.url}}{{site.baseurl}}/assets/images/top-page0.jpg)



## デフォルトのレイアウト

ヘッダーファイルとフッターファイルを作成し、基本レイアウトに組み込む。そしてスタイルを当てる。<br/><br/>
ここにYAMLデータとLiquidテンプレートの利用、Sassによるスタイリングの一連の流れを見ることが出来る。

<!-- ### _config.ymlへサイト名を記述 -->
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
<br/><br/>
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

テンプレート`default.html`の`<body>..</body>`内に`header.html`と`footer.html`をliquidでincludeする。

<!-- _layouts/default.html -->
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

<!-- _sass/main.scss -->
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



