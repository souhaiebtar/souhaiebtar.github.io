---
layout: post
date: 2020-01-14 20:19:09
title: Compile vim with ruby support, install command-t to it
description: >-
  an article about how i compiled vim with ruby support and adding command-t to it
main-class: 'tools'
color: '#7AAB13'
tags:
- tools
twitter_text: >-
  install termite on debian 10
introduction: "how i compiled vim with ruby support and add command-t to it"
---
# History:
i like to test, tweak and customize thing to feet my need, one of this thing is vim, i can't even describe how much this editor is great and how much it's helpful, simply it's stupid not use it (or at least something similar, **emacs** maybe)

# VIM installation
vim is a great tool but it's tricky to make it work when you like to tweak and test new thing plugin included, specially when some plugin either require ruby or python, in my case i installed it with ruby support enabled


1. first check if you have many a ruby version manager (n my case rbenv), make sure to use ruby version set by the system, in my case i used
```shell
rbenv global system
```

2. clone the vim repo
```shell
git clone https://github.com/vim/vim
```
3. change directory, branch and clean things ( the version can be changed to your liking)
```shell
cd vim && git checkout v8.1.0021 && git clean -f
```
4. Configure vim build
```shell
./configure --prefix=/usr/local \
--with-x \
  --disable-nls \
  --disable-netbeans \
  --disable-gui \
  --enable-multibyte \
  --enable-rubyinterp \
  --enable-python3interp \
  --with-features=huge \
  --with-tlib=ncurses \
 --enable-fail-if-missing \
```
5. build vim
```shell
sudo make && sudo make install && sudo make clean
```

now you should have vim installed

# Install command-t

1. install command-t plugin using your favorite plugin manager (in my case *Plugged*), i added
```
Plug 'wincent/command-t'
```
2. change directory to `extconf.rb`, for Plugged
```shell
~/.vim/plugged/command-t/ruby/command-t/ext/command-t
```
3. build command-t
```shell
ruby extconf.rb && make clean && make
```


Now, you should be able to run vim and use command-t plugin without problem,

**N.B:**
 to use command to
use
` <leader> t` (in vim, by default <leader> is the `\` character)
