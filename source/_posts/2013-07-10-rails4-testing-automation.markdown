---
layout: post
title: "Rails4でのRSpec自動実行環境の作成"
date: 2013-07-10 00:15
comments: true
categories: rails
---

Rails4アプリでファイルの変更を検知し、RSpecを実行するようにする。
テストの結果はGrowlにて通知するようにする

## 環境
- Ruby 2.0.0
- Rails 4.0.0
- Mac OS X 10.8


## 利用するもの
- Rspec
 - BDDフレームワーク
- Guard
 - 監視・実行の管理
- Growl
 - 通知
- Spring
 - 事前にアプリを立て、コマンドの実行を高速化する

## 準備
### Gemfileの更新

```ruby
group :development, :test do
  gem 'rspec-rails'
  gem 'spring'
  gem 'guard'
  gem 'guard-rspec'
  gem 'growl'
end
```

`bundle install`

### rspec:install
```
spring g rspec:install
```

`spec/spec_helper.rb`などが作成される

### guard init
```
gurad init
```

`Guardfile`というGuardの設定を記述するファイルが生成される

### guard rspecでspringを使うようにする

`guard :rspec do`という記述を`guard :rspec, spring: true do`に変更する
これによってguardでrspecが動く場合にspringで立てたテスト用のプロセスで実行されるようになる

基本的に作業はこれだけ。
あとはファイルを更新してテストが走ったり、通知がいくことを確認できれば問題なし。


かなり簡単に自動でテストが回る環境が作れた。
無意識にテストが実行されフィードバックが返ってくるのはとてもよい。

Rails4が出たということで`database_cleaner`を始め開発環境を再度整えて行きたい
