---
layout: post
title: "RubyKaigi2014で発表した"
date: 2014-09-22 22:42:12 +0900
comments: true
categories: ruby rubykaigi
---

RubyKaigi 2014めっちゃいいKaigiだった。

## 初めての発表
今回初めてSpeakerとしてRubyKaigiに参加した。

[発表者情報](http://rubykaigi.org/2014/presentation/S-TakumiMiura)

### 感想
めっちゃ緊張した。

でも会議っぽい(?)写真取りたかったので、こんなことをしてみたり

![photo](http://photos-d.ak.instagram.com/hphotos-ak-xfa1/10654988_1524824864402355_142010473_n.jpg)

セミインターナショナルなKaigiということで発表自体は日本語だったけれどもスライドは英語にしようと思ってせっせと準備をしました。


結構なスライドの枚数になってしまい通訳の方が大変だったんじゃないかとすごく思う。
また、RubyKaigiのスタッフの方々がスライドチェックなどをしてくれて少しはまともな資料になりました！

通訳の方、スタッフのみなさんありがとうございました!

### スライド

<script async class="speakerdeck-embed" data-id="ed2e4fa0221e0132318076af556e37c5" data-ratio="1.33333333333333" src="//speakerdeck.com/assets/embed.js"></script>


## "Gem of this Week" - building culture and making gem
というタイトルで発表をした。

内容は僕が転職をして1年かけてカジュアルにgemを作るチームを作ってきた話。

**今週のgem**というコーナーで毎週のようにgemが更新されたり作成されていく環境を見せることができるようになったのでgemを作ることが**特別**じゃなくしました。

その結果チームメンバーがカジュアルにgemを作るようになった。

#### 想い
今週のgemを初めた時の想いとしては

- もっと楽したい。
- 楽しいことをしていたい。
- 同じことを繰り返したくない。

だった。

発表することになった時に
同じように共通化して社内gemみたいなの作って楽になる人たちはいっぱいいるんじゃないかと思った。
僕のとったアプローチの紹介をすることによっていろんな人の生活が良くなればいいなぁなんて想いながら発表準備をしてました。

### アプローチのまとめ
#### privateなgemserverを用意する
- 弊社は[geminabox](https://github.com/geminabox/geminabox)を使ってる
- privateなのでどんなgemをアップしても大丈夫
- メンテされていないgemへの辛いモンキーパッチはforkしてgem化できる

※deployの観点からgemにしているほうが気楽だった

※Gemfileでgitのsourceを指定するという手段もある

#### 自由にgitリポジトリを作れるようにする
- 弊社はGitLabを使っている。
- メンバーは自由に他のプロジェクトを見ることができる
- メンバーは自由にプロジェクトを作ることができる

#### コミュニケーションできる場を作る
- 作ったgemのアナウンスをしたり、理想の開発とか語ったり
- 弊社は週に1回各チームのメインエンジニアが集まるミーティングがあり、そこでアナウンスをしたりしていた。(今週のgem)

#### +αとしてgemを作る障壁を下げていく
- gemとはカジュアルに作るものであるというイメージ化 `今週のgem`
- gemを簡単に作り、簡単にデプロイできるgemを作る `drecom_gem`
- 新卒の子にも作ってもらった
- 多くのgemを作っていくことによって、参考例をたくさん作った

### 雑記
読み原稿的なのも一緒にアップすればよかったな...

別の記事で書きたいと思います!

![speaker](http://rubykaigi.org/2014/images/badge-for-speaker.png)
![sponsor](http://rubykaigi.org/2014/images/badge-for-official-sponsor.png)
