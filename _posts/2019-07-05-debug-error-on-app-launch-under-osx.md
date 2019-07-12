---
layout: post
date: 2019-07-12 11:06:30
title: Debug error on app launch under osx
description: >-
  an article about how i fixed the not launching app
main-class: 'tools'
color: '#7AAB13'
tags:
- tools
- debug
- macos
twitter_text: >-
  debug/fix not launching app under osx
introduction: "degub/fix not launching app under osx"
---
## Introduction

today when i opened my laptop, to start working, one of my preferred productivity app  didn't start, i opened it using `open -a `, from `/Applications` folder using `Finder`, but nothing seemed to work, i returned to an older version, it worked properly; after that i tried to update another app by downloading the dmg than copy/paste under `/Applications` folder, the same error as for the first app happened again, definitely i have to try to find a fix.

after thinking a little, trying opening the apps from the terminal to see error messages, didn't help at all `open -a` or `/Applications/APPNAME.app/contents/MacOS/APPNAME`, unlike linux opening the app from terminal didn't show any helpful error message.

after some googling, i stumbled upon [🔗][1], which give me a hint, the macOS `Console.app`


# How to fix it

shortly, how i proceeded:
  1. i opened the `Console` app
  2. i clicked on `system.log` under `Reports` on the left sidebar of the `Console` app
  3. i typed the name of app in the top `search field` of `Console` app
  4. i opened the app again using `Launchpad` or from `/Applications` folder using `Finder`
  5. read the messages with the timestamp close to when you opened the app

voila, now i get errors  on the `Console` that can give  me a lead on how to fix the problem


```Debug
removing service since it exited with consistent failure - OS_REASON_CODESIGNING | When validating /Applications/APPNAME.app/Contents/MacOS/APPNAME

.... Binary is improperly signed
```

it's a problem with codesignature, it's something that i faced before, normaly codesign the app will resolve the problem and it can be done from terminal using:

```SHELL
sudo codesign --force --deep --sign "/Applications/APPNAME.app/Contents/MacOS/APPNAME"
```

> N.B: some time you need to execute the above command on multiple file because the app has Dependencies that are not properly signed, for that repeat the process described above until all error messages go away.

Just one thing to now/learn, on MacOS `Console.app` is your friend



[1]: https://superuser.com/questions/292341/open-application-from-osx-terminal-with-debug-printouts
