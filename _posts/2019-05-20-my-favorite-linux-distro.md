---
layout: post
date: 2019-05-20 11:21:09
title: My favorite linux for Development
description: >-
  an article about my fovrite linux for development
main-class: 'misc'
color: '#7AAB13'
tags:
- linux
- arch
- manjaro
twitter_text: >-
  my favorite linux distro
introduction: "How arch/manjaro made my life easier/funier."
---
## Introduction 

Today post is my very first post in my new blog after changing the design of it, it will be about one of my favorite linux distro Arch/Manjaro.

I'm a distro hobbyist, i'm always in the quest of finding the perfect distro, it's a never ending quest, in this quest i always emphesize on speed,for many month know, i'm using and also contributing to ArchLinux more precisely Manjaro, Manjaro with openbox.

Manjaro openbox is so cool, it's light, come with many tweak that make life easier, and it doesn't alter the way i use computer (like i3 does), the thing about openbox is that it's very light weight but it also come with pretty much nothing, manjaro openbox try to fill the gappe by adding tint2 (with a cool settings oob), also polybar and many other cool stuff.

## How i come to contribute

the very first time i contributed to arch aur was from inside a VM running Manjaro xfce using VirtualBox from inside a Hackintosh (a fully working one), it was by updating a package called [goterminal](https://aur.archlinux.org/packages/goterminal/).

it was a very pleasant experience to contribute(even with little something), also it come with advantages like learning how build work, and learning new command and tool, after my first contribution.

## How to ?

mainly when i'm contributing, i try to update packages to do that this steps are required

1. clone the repo 
```SHELL
git clone https://aur.archlinux.org/stacer-bin.git 
cd stacer-bin
```
2. change to PKGBUILD or any other file (let say by updating the pkgver )
3. generate update ckecksum
```
makepkg -g -f -p PKGBUILD
```
4. copy new ckecksum in `PKGBUILD` file
5. generate `.SRCINFO` file
```
makepkg --printsrcinfo > .SRCINFO
```
6. create and install
```
makepkg -si
```
N.B: you can skip integrity check using `--skipinteg`
```
makepkg --skipinteg -si
```

in the end, if it work properly try to push those changes to arch aur or at least create a github repo and push to it like my [pkgbuilds](https://github.com/souhaiebtar/pkgbuilds)