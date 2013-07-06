---
layout: post
title: "クリップボードを有効にしたVimを使う"
date: 2013-07-06 18:26
comments: true
categories: mac vim
---

MacのVimは初期状態でclipboardが有効になっていなくて辛いのでvimからclipboardが使えるようにする
```
vim --version |grep clipboard
```

結果
```
-clientserver -clipboard +cmdline_compl +cmdline_hist +cmdline_info +comments
 -xterm_clipboard -xterm_save
```

現時点ではHomebrewのVimのFormulaはclipboardに対するオプションがないみたいなのでMercurialからソースを持ってきて対応する

## 1. hgコマンドを使えるようにする

```
brew install hg
```

## 2. vimをinstall

```
hg clone https://vim.googlecode.com/hg/ /tmp/vim
cd /tmp/vim
make clean
./configure --prefix=/usr/local --enable-multibyte --enable-xim --enable-fontset --enable-rubyinterp --enable-perlinterp --with-features=huge --disable-selinux
make
make install
```

## 3. 確認

```
/usr/local/vim --version |grep clipboard
```

`+clipboard`が含まれていればOK

configureに与えるものは各自必要なものを指定すること
