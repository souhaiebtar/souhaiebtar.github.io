---
layout: post
date: 2023-10-22 11:48:09
title: install python 3.11 using pyenv on ubuntu
description: >-
  an article for testing
main-class: 'tools'
color: '#7AAB13'
tags:
- tools
twitter_text: >-
  how i did install python 3.11 on pyenv
introduction: "How i installed python 3.11 on pyenv"
---
## Introduction

as usual i use pyenv to install whatever python version i want, yesterday when i tried to install python 3.11 using `pyenv install 3.11`,
the command caused a lot of error, it seem to be related to `tcl-tk` and one of error log showed `ModuleNotFoundError: No module named '_tkinter'`



after some googling, there was 3 main articles (the one below in resources),
the main article that i used is the one in `medium.com`, with some adpatation for `Ubuntu` i'm using

## How to proceed

basically

```BASH
brew install pyenv
brew install tcl-tk
brew install pyenv-virtualenv
```

then after that you add to `.zshrc` or `.bashrc` (it depend on what you are using)

```BASH
if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi

export LDFLAGS="-L$(brew --prefix tcl-tk):$LDFLAGS"
export CPPFLAGS="-L$(brew --prefix tcl-tk)/include:$CPPFLAGS"
export PKG_CONFIG_PATH="-L$(brew --prefix tcl-tk)/lib/pkgconfig:$PKG_CONFIG_PATH"

export PYTHON_CONFIGURE_OPTS="--with-tcltk-includes='-I$(brew --prefix tcl-tk)/include' --with-tcltk-libs='-L$(brew --prefix tcl-tk)/lib -ltcl8.6 -ltk8.6':$PYTHON_CONFIGURE_OPTS"
```

then run `exec $0` (or to simply `exec zsh` or `exec bash`, it depend on what you are using)


### Resources

https://medium.com/@azuryn/install-python-by-pyenv-w-tcl-tk-on-macos-10-14-6-mojave-14fde5351f53

https://stackoverflow.com/questions/76878713/tkinter-extension-was-not-compiled-and-gui-subsystem-has-been-detected-missing

https://stackoverflow.com/questions/75096114/problems-with-installing-python-3-11-1-using-pyenv