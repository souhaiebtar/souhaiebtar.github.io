---
layout: post
date: 2019-07-07 10:14:09
title: install termite on debian 10
description: >-
  an article about how i installed termite on debian 10
main-class: 'tools'
color: '#7AAB13'
tags:
- tools
- termite
- debian10
twitter_text: >-
  install termite on debian 10
introduction: "how i installed termite on debian10"
---
## Introduction

like i said before, i really like to try and test new things, linux distro tools are one of those things, i was waiting for the stable release of debian 10 for some time now, 6 july was the day of release, in my localtime(GMT+1) 6th of july was yesterday, i was opening debian website multiple time but nothing to be found, it was 6th july US localtime(i don't now which local time that is).



i used the `net install` to install it, and i choose the `gnome desktop` and i disabled the `print server` on the window prompt to install software,
all things went ok without hassle,

after that i used:
  ```SHELL
  su -
  ```

> you are prompted to enter your password than after login succefully

```SHELL
VISUAL=vi visudo
```

> i dont now how to used nano, this is why i'm adding `VISUAL=vi`

than i added
```SHELL
tunknwon ALL=(ALL:ALL) ALL
```
> i saved and quit


after install the ram usage was about **850mB**, way below the **1050mB** of POP os 1804, even after install 3 gnome extension (arc menu, dash to panel and  services systemd) and `open-vm-tools-desktop`

running `free -m` using `termite` terminal report 857/858 mB, installing termite was not straight forward, it ended compiling it with the help the error messages and some googling

## How i nstalled it [🔗][1] [🔗][2]

i will keep it short by copy the step cli command i used:

```SHELL
sudo apt install -y build-essential
sudo apt-get install -y git g++ libgtk-3-dev gtk-doc-tools gnutls-bin valac intltool libpcre2-dev libglib3.0-cil-dev libgnutls28-dev libgirepository1.0-dev libxml2-utils gperf libtool
cd ~
git clone https://github.com/thestinger/vte-ng.git
echo export LIBRARY_PATH="/usr/include/gtk-3.0:$LIBRARY_PATH"
cd vte-ng
git checkout 0.56.2.a
sh autogen.sh
sudo make && sudo make install
cd ~
git clone --recursive https://github.com/thestinger/termite.git
cd termite
sudo make && sudo make install
sudo ldconfig
```

> i think there is some unneeded tools but sorry i don't have time to make it perfect

[1]: https://computingforgeeks.com/install-termite-terminal-on-ubuntu-18-04-ubuntu-16-04-lts/
[2]: https://github.com/thestinger/termite/issues/536#issuecomment-343577161
