---
layout: post
title: "Rails4でアプリケーションを作る"
date: 2013-07-07 01:29
comments: true
categories: rails
---

6/25 [Rails4.0.0がリリース](http://weblog.rubyonrails.org/2013/6/25/Rails-4-0-final/)されました。

ということで早速Rails4でプロジェクトを作成。

- Ruby 2.0.0-p247
- Rails 4.0.0
- Mac OS X 10.8.7


```
gem install rails
```

## プロジェクトの作成

```
rails new your_project_name -B -T -d mysql
```

- rails new後のbundle installがとても嫌いなのでskip-bundleをしたいので`-B`オプションを付与
- test-unitではなくRspecを使いたいので`-T`でTest::Unitのファイルが作成されるのを回避
- 今回はDBをMySQLにしたかったので`-d mysql`
 - デフォルトはsqlite3

### tree
作られたファイルの確認

```
.
├── Gemfile
├── README.rdoc
├── Rakefile
├── app
│   ├── assets
│   │   ├── images
│   │   ├── javascripts
│   │   │   └── application.js
│   │   └── stylesheets
│   │       └── application.css
│   ├── controllers
│   │   ├── application_controller.rb
│   │   └── concerns
│   ├── helpers
│   │   └── application_helper.rb
│   ├── mailers
│   ├── models
│   │   └── concerns
│   └── views
│       └── layouts
│           └── application.html.erb
├── bin
│   ├── bundle
│   ├── rails
│   └── rake
├── config
│   ├── application.rb
│   ├── boot.rb
│   ├── database.yml
│   ├── environment.rb
│   ├── environments
│   │   ├── development.rb
│   │   ├── production.rb
│   │   └── test.rb
│   ├── initializers
│   │   ├── backtrace_silencers.rb
│   │   ├── filter_parameter_logging.rb
│   │   ├── inflections.rb
│   │   ├── mime_types.rb
│   │   ├── secret_token.rb
│   │   ├── session_store.rb
│   │   └── wrap_parameters.rb
│   ├── locales
│   │   └── en.yml
│   └── routes.rb
├── config.ru
├── db
│   └── seeds.rb
├── lib
│   ├── assets
│   └── tasks
├── log
├── public
│   ├── 404.html
│   ├── 422.html
│   ├── 500.html
│   ├── favicon.ico
│   └── robots.txt
├── tmp
│   └── cache
│       └── assets
└── vendor
    └── assets
        ├── javascripts
        └── stylesheets

31 directories, 34 files
```

binやapp/models/concernsなどが増えていますね!

## rspec-railsの導入
[rspec/rspec-rails](https://github.com/rspec/rspec-rails)に従って

```
# Gemfileに追加
group :development, :test do
  gem 'rspec-rails', '~> 2.0'
end
```

```
bundle
```

```
rails g rspec:install
```

## db:create
```
rake db:crate
```

## server start
```
rails s
```

そんな訳でとりあえず起動した。

rspecのくだりは別にいらなかったね。
