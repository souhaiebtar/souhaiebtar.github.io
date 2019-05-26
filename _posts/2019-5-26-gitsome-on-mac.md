---
layout: post
date: 2019-05-20 11:21:09
title: install gitsome on MacOS
description: >-
  an article about how i installed gitsome on MacOs
main-class: 'tools'
color: '#7AAB13'
tags:
- python
- git
- cli
twitter_text: >-
  gitsome osx macos
introduction: "how i finally installed gitsome on osx"
---
## Introduction 

i'm really fun of every thing cli related, also i like github, i try to do everything i can inside the terminal, it's in thins context that i tried to reinstall gitsome, the things is that the default command `pip3 install gitsome` work properly on linux without the need to search/install a fix, know i tried to run the same command on macOS, install finish properly but when i try to run `xonsh`, i get:

```SHELL
... /site-packages/xonsh/main.py", line 404, in main ...
```


i tried many thing:
 * install [dircolor](https://github.com/gibbling/dircolors), install `coreutils` add `eval $(gdircolors -b $HOME/.dircolors)
 * brew install zsh-syntax-highlighting
 * manually add `zsh-syntax-highlighting-filetypes.zsh`

but nothing work, after all of that and reading the error, i concluded that it should be in error on `xonsh` which is a dependency for gitsome.
## How i resolve it

as i concluded that it must be an error on `xonsh`, i googled `xonsh macos mojave` ang i got a [link](https://qiita.com/dsafdsnaendf/items/1d5d15cd112f8609f8ce#mac-%E3%81%AE%E7%92%B0%E5%A2%83) that helped me resolve the problem, the command to fix 

```SHELL
pip3 install xonsh gnureadline prompt-toolkit
```

also for sake of convenience, i run `brew install bash-complete2` after running `brew uninstall bash-complete`