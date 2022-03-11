---
layout: post
title: Jekyllの空プロジェクト
---

Bundlerを利用してJekyllをインストールする。そしてテーマ作成のベースとして、最小構成の新規プロジェクト、いわゆる空プロジェクトを導入する。

rubyの環境構築が必要な場合、Jekyll公式の[Ruby基礎](http://jekyllrb-ja.github.io/docs/ruby-101/)、[インストール](http://jekyllrb-ja.github.io/docs/installation/)を参考に。

### Bundler
***

基本的に、JeykllはBundlerでインストールする。BundlerはRubyのGemパッケージ管理システムで、Ruby2.6（Dec 2018）から標準Gemになっている。

```shell
$ bundler --version
#-> Bundler version x.x.xx
```

Bundlerをはじめて使う場合、Gemをインストールする場所 `vendor/bundle` を設定する。Bunderの設定ファイル`config`は、ユーザディレクトリの .bundle の中にある。

```shell
$ bundle config path vendor/bundle
$ cd .bundle
$ cat config
#-> BUNDLE_PATH: "vendor/bundle"
```

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

空プロジェクトは以下のディレクトリ構成に展開される。<br/>

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

