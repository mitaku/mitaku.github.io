---
layout: post
title: "HomebrewでRictyをインストール"
date: 2013-07-08 19:01
comments: true
categories:
---

個人的にとても見やすいフォントのRictyをHomebrewで手軽にインストールできるみたいですね。

- [プログラムに最適なフォント『Ricty』を超簡単にインストール[Mac限定]](http://morizyun.github.io/blog/ricty-font-homebrew-mac/)

こちらのとおりに

```
brew tap sanemat/font
brew install ricty
```

しばらくするとインストールが終わるので、表示されるメッセージに従ってコマンドを実行

```
***************************************************
Generated files:
  /usr/local/Cellar/ricty/3.2.1/share/fonts/Ricty-Bold.ttf
  /usr/local/Cellar/ricty/3.2.1/share/fonts/Ricty-Regular.ttf
  /usr/local/Cellar/ricty/3.2.1/share/fonts/RictyDiscord-Bold.ttf
  /usr/local/Cellar/ricty/3.2.1/share/fonts/RictyDiscord-Regular.ttf
***************************************************
To install Ricty:
  $ cp -f /usr/local/Cellar/ricty/3.2.1/share/fonts/Ricty*.ttf ~/Library/Fonts/
  $ fc-cache -vf
***************************************************
```

こんなメッセージが出ていました。

```
brew info ricty
```

で再度見れます。

便利便利
