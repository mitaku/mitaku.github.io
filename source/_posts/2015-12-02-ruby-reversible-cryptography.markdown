---
layout: post
title: "Rubyで可逆暗号"
date: 2015-12-02 01:00:00 +0900
comments: true
categories: ruby gem advent_calendar
---

## はじめに

これは [【その2】ドリコム Advent Calendar 2015](http://www.adventar.org/calendars/1044) 2日目の記事です

1日目の記事はarihhさんの「[カンバンの管理に改善を加えたら加速した話 - arihhのブログ](http://arihh.hatenablog.jp/entry/2015/12/01/005948)」です

[【その1】ドリコム Advent Calendar 2015 - Adventar](http://www.adventar.org/calendars/1043) もあります!

めっちゃブログ書くのが久しぶりで、このブログの更新の仕方を忘れてたりしました。

**あと、モンハンやりたい。モンハンやりたい、モンハンやりたい**

_※エンジニア向けの記事です_


## 本題 - 「Rubyで可逆暗号-その情報を知りたくない僕らは」

生データとして扱いたくない情報を難読化する話をします!

_※エンジニア向けの記事です_

### (エンジニアの自分が)生データとして扱いたくない情報
 * 何かのアカウント(ID/PW)
 * 自分のものじゃない秘密鍵
 * ユニークなギフトコード
 * etc...

などなど。思い当たるものはないでしょうか？


---


最近、ドリコムではAWSの活用事例が増えてきました。

AWSを便利に活用させていただいているのですが、必然的にアクセスキーやシークレットキーを取り扱う必要がでてきます。

アクセスキーとシークレットキーが漏れたりすると何が起こるかわかりません。

**情報漏えいはシステムよりも人間が原因になることのほうが多い**と教わってきたので

個人的には知らなくてよければ知らないまま過ごしたい情報です。

なので、少しでも心を穏やかにするために、生のデータを扱うの避けて、一工夫して運用しています。

### Rubyで可逆暗号
#### ActiveSupport::MessageEncryptor
みんなだいすき`ActiveSupport`

それ、`ActiveSupport::MessageEncryptor`でできるよ!!

[Railsで簡単可逆暗号(ActiveSupport::MessageEncryptor)](http://qiita.com/kengos@github/items/e8ea8f71c47852fde48b)

```ruby
secret = SecureRandom::hex(128)
#=> "13f3bab71cc735eea473e8fd225bb04232d23eadf194bd066179e09871fdf9244b454c38ebd6715e03b903d595b8ac5d75488dff2d9d48f3d2eb5e9a026ebbb4ef799e9596376f63a49640e9336f9b011fa8972a763a6d1fe13b5d4d096a34cdeba91636c86b70e9a88fab56f2a4f6b19eee801ac0d1e3415bb17b8f92f0133b"
encryptor = ::ActiveSupport::MessageEncryptor.new(secret, cipher: 'aes-256-cbc')
encrypt_message = encryptor.encrypt_and_sign("target_message")
#=> "QjlkVndyeERrV3BUcW1paVVkTDJQTWhzV3R5OEV3N3JsR2FnV0VxRjdCTT0tLUJFSmdLTUNFbHdmZHhWcjZUQllUR0E9PQ==--6f6d897b52cfad56d9a31f8a19d44481e5343f18"
encryptor.decrypt_and_verify(encrypt_message) == "target_message"
#=> true
```

便利ですね。
これだけだと芸がないので、ドリコムでの事例を紹介します!

#### ReversibleCryptography
[reversible_cryptography](https://github.com/mitaku/reversible_cryptography)

という自作gemを使ってます。

READMEより

```ruby
secret = "password"
encrypted_message = ReversibleCryptography::Message.encrypt("target_message", secret)
#=> "md5:388eeae24576572f946e9043a2118b2d:salt:161-225-182-109-143-90-1-28:aes-256-cfb:DHY6DF3+iFzH36FMbeI="
ReversibleCryptography::Message.decrypt(encrypted_message, secret) == "target_message"
#=> true
```

簡単ですね。

* *※上記例とは暗号化方式等,諸々違うため堅牢度合いは違います*
* *※暗号化するものが簡単な英単語だったりする場合,MD5から逆引きされる可能性があります*
* *※パスワードの強度は高いものを利用しています*

### もう一工夫
Railsに限った話ではないですがアプリでの利用方法も記載します

各種設定はyamlファイルに記載することが多く、
このようにYAMLのプライベートタイプを追加し環境変数を利用するようにしています。

```ruby
class ReversibleEncryptedString < BasicObject
  def initialize(str)
    @str = str
  end

  def decrypted_string
    @raw ||= ::ReversibleCryptography::Message.decrypt(@str, ::ENV["REVERSIBLE_CRYPTOGRAPY_SECRET"])
  end

  alias_method :to_s, :decrypted_string

  def method_missing(method, *args)
    decrypted_string.__send__(method, *args)
  end
end

YAML.add_private_type("Encrypted") do |_type, val|
  ReversibleEncryptedString.new(val)
end
```

```yaml
aws:
  endpoint: "ec2.ap-northeast-1.amazonaws.com"
  access_key_id: !x-private:Encrypted "md5:109a42207275ce753e4923575ace3e12:salt:255-105-253-88-5-107-47-24:aes-256-cfb:4n++p1w8WZrjzmjna8W1mqh6PSA="
  secret_access_key: !x-private:Encrypted "md5:7844e3da7a807eb915207f7a36d4087b:salt:54-109-31-32-93-207-203-85:aes-256-cfb:l1OeNofj0C+vlsWfPfrTwQ=="
```

環境変数の設定には[Dotenv](https://github.com/bkeepers/dotenv)を利用しているところもあります。

### ReversibleCryptographyの活用プロダクト
弊社sue445さんのgemでも利用されています!

 * [itamae-plugin-resource-encrypted_remote_file gem](https://github.com/sue445/itamae-plugin-resource-encrypted_remote_file)
  * [itamae-plugin-resource-encrypted_remote_file を作った](http://sue445.hatenablog.com/entry/2015/05/09/185807)

## おわりに
 * **情報漏えいは人が原因のほうが多い!**
  * 意識をしつつ、健全な開発をしましょう!
  * 知りたくない情報は暗号化してからもらいましょう!
 * 可逆暗号ができる[ReversibleCryptography gem](https://github.com/mitaku/reversible_cryptography)の紹介をしました
  * 気が向いたら使ってみてもらえれば幸いです!


ということで次はnakajiさんです!
