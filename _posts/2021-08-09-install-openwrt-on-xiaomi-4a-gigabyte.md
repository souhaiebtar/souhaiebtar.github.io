---
layout: post
date: 2021-08-09 19:01:09
title: install openwrt on xiaomi 4a gigabyte
description: >-
  an article about how i installed openwrt on xiaomi 4A gigabyte
main-class: 'tools'
color: '#7AAB13'
tags:
- tools
twitter_text: >-
  openwrt Xiaomi 4A Gigabyte
introduction: "How i installed openwrt Xiaomi 4A Gigabyte"
---

## Introduction

i had my eyes on openWrt for quite some years now but because import is either diffucult or  prone to theft, i had to wait until now to get a Router that support openwrt that is in retail,



## How to proceed

for the method and instruction, i used the instruction in `https://github.com/acecilia/OpenWRTInvasion`

for the firmware i downloaded the one from this repo `https://gitlab.com/db260179/xiaomi-m4a/-/releases` that have the name `Minor update v1.5.2-stable - Compatible with official repos and fixes`, you will find the file in the link with the name 'Built images, imagebuilder and SDK with checksum'[file](https://workupload.com/archive/fzuCpEVX)

>> N.B: the name of the file i used is `openwrt-19.07.7-ramips-mt7621-xiaomi_mir4ag-squashfs-sysupgrade.bin`

you can copy the file using ftp client like `filezilla` or `cyberduck`, copy it to `/tmp` ( because you have write permission) and rename to `firmware.bin` (to make it easier) than juste run

```BASH
mtd -e OS1 -r write firmware.bin OS1
```

>> N.B: be patient and juste wait, go eat something


### Resources
[1]:  https://github.com/acecilia/OpenWRTInvasion
[2]:  https://openwrt.org/inbox/toh/xiaomi/xiaomi_mi_router_4a_gigabit_edition
[3]:  https://forum.openwrt.org/t/xiaomi-mi-router-4a-gigabit-edition-r4ag-r4a-gigabit-fully-supported-and-flashable-with-openwrtinvasion/36685/643
