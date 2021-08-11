---
layout: post
date: 2021-08-11 23:36:09
title: Update my lenovo Y510P hackintosh to Big sur
description: >-
  an article about how i updated my lenovo y510P hackintosh to Big Sur
main-class: 'tools'
color: '#7AAB13'
tags:
- tools
twitter_text: >-
  update y510p hackintosh to big sur
introduction: "How i update my y510p to big sur"
---
## Introduction

i'm using MacOs on my y510P from 2014-2015, the first OSX version i used was Yosemite, i was very lucky to get a laptop that was fairly well supported (it was not in my mind when i bought it, but Alhamdulillah 🤲), i always update my laptop to the next version fairly late (letting things become more stable before i make the jump, because it's my main system that we are talking about) and i think in 2018-2019 i started making a full clone of my drive (using `Carbon copy cloner` and copy the `EFI` partition content manually before and after every update) until Catatlina come out  where i decided that i will keep using Mojave because it seemed stable enough and didn't want to give my self a headeck by updating and figuring out how to fix problems that come out every update because the change apple make and because the hardware is not obviously officialy supported.


## How to proceed

1. you need download big sur update from `App Store`
2. copy the `EFI` folder from `https://github.com/souhaiebtar/y510p-OpenCore` to your `EFI` partition, and make sure to open `EFI/config.plist` and generate `MLB`, `ROM`, `SystemSerialNumber` and `SystemUUID` under `PlatformInfo->Generic`
3. Start Install, it will reboot many time, after each restart select entry that have the name `MacOs installer` (or the entry that have `installer` in it's name), until it dispear

> N.B: it's also can be used to create a macos installer for the y510p, also my
y510p screen is 1366*768

### Resources
* https://github.com/Z39/Lenovo-Y510p-OS-X-Clover-OpenCore-Hotpatch
* https://dortania.github.io/OpenCore-Install-Guide/
* https://www.dognmonkey.com/techs/how-to-fix-kernel-panic-kp-reboot-after-sleep-wake-catalina-10-15-4-on-haswell-hd4600.html
* https://github.com/acidanthera/Lilu/blob/master/KnownPlugins.md
* https://dortania.github.io/OpenCore-Install-Guide/extras/big-sur/#cannot-update-to-newer-versions-of-big-sur
* https://dortania.github.io/OpenCore-Post-Install/universal/security/applesecureboot.html#securebootmodel
* https://dortania.github.io/hackintosh/updates/2020/11/12/bigsur-new.html
* https://www.macworld.com/article/347666/the-best-ways-to-back-up-your-big-sur-mac.html
