---
title: Setup up reactive native platform
date: 2019-03-03 21:14:12
tags:
---

## Major step

I follow the guide in react offical website, major step is as follow

1. Install Java sdk, python and node.js
2. Install Android studio
3. Install Android SDK
4. Set user variables in environment variables
5. Set Path in environment variables
6. Create Android Virtual Device

I have met one issue, when installing Android Studio, it stunk at install HAXM intel X86 emulator and then whne I try to launch emulator, an error related HAXM happens, I solved the issue using below solution

>  Had the same problem in windows 10, which was solved by disabling Hyper-v and reinstalling HAXM via SDK Manager>SDK Tools>Intel x86 Emulator Accelerator

