---
layout: post
title: "Rails寺子屋 x kosenconfを開催した"
date: 2013-03-27 22:38
comments: true
categories: event
---

2013/03/23に[Rails寺子屋](http://rails.terakoya.io/)というイベントを開催し、講師という立場で参加した。

午前10時という時間から開始ということで、寝坊だったり、遠方からの参加者は朝から東京に投げ出され大変そうだった印象。

あと、鉄道のICカード統一で駅が大変なことになっていた。速い人は5時くらいから並んでいるとか…

さて、寺子屋ですが

@RooandQoo ちゃんと一緒に1グループ担当しました。この日のために服装を揃えました（嘘です）

<a href="http://www.flickr.com/photos/sora_h/8583674262/" title="P3233335 by sora_h, on Flickr"><img src="http://farm9.staticflickr.com/8509/8583674262_aab196bc06_z.jpg" width="640" height="480" alt="P3233335"></a>


### 午前
午前中は環境構築をする時間として設けていて環境構築をしつつ、終わったメンバーと対談したりRubyで簡単なプログラムを書いてみたりしてました。

- RubyでFizzBuzzしてみたり

```ruby
puts 100.times.map { |i| (s = ((i % 3).zero? ? 'Fizz' : '') + ((i % 5).zero? ? 'Buzz' : '')).empty? ? i : s }
```
- 与えた文字をランダムで利用して140文字の文字列を作る遊びなど (下の例ではsを与える文字にしてます)

```ruby
s = "みうらたくみ"
puts 140.times.map { s.chars.sample }.join
```

### 午後
ワークショップのメインということでRailsを使って簡単なアプリケーションを作ってみようというコーナーでした
ここでは[Rails Girls](http://railsgirls-jp.github.com/)というイベントの教材を使って、[Heroku](http://www.heroku.com/)にアプリケーションをデプロイするところまでやりました。

まずは、この教材の出来がとてもよい。

反日でRailsアプリを1つ作り、Herokuにデプロイし1サービスの提供者になれる。

基本的に教材にそってやっていき、都度必要な説明を講師陣で加えていくという形で行なって行きました。

無事全員がHerokuにデプロイするところまで行きました。素敵

### 懇親会
みんなでピザを頬張り、ワイワイしてました。

### 感想
Rails Girlsの教材はとてもよい。

Railsの手軽さは体験してもらうことはできたと思う。

ただし、学習コストが高いRailsなのでアフターサポート的なものがあるとよいのかなぁと思いました。

気軽に[@mitaku](https://twitter.com/mitaku)までどうぞ！

参加者のみなさん、講師の皆さん、たくさんの関係者のみなさんありがとうございました！

*楽しいRailsライフを!!*
