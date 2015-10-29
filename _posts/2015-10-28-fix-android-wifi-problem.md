---
layout: post
category: android
title: Fix Android 5.1 WiFi Problem
tagline: 2015-10-28
tags: [android]
---

手机升级到 Android 5.1 之后也遇到了连接 WiFi 时发热耗电的问题。在这里记录一下解决过程。

<!--more-->

这里 [http://www.noisyfox.cn/45.html](http://www.noisyfox.cn/45.html) 介绍了这个问题的产生原因与傻瓜方式的解决办法。

但是由于我不想 root 系统，因此需要自行用 adb 命令进行解决。

到这里 [http://www.androiddevtools.cn/](http://www.androiddevtools.cn/) 下载了 Android SDK 并安装。

在安装目录下找到 adb.exe，等等就可以用它执行 adb shell 了。可以添加到环境变量，或自行编写 bat 脚本。

在手机上打开开发者模式，并打开 USB 调试。

将手机连接电脑后，我用的 Sony Z3 自行弹出询问是否安装 PC 套件。点击安装，厂家的 PC 套件会包含 adb 驱动。如果没有也可以自行上网下载安装。

在命令行下执行 adb.exe，我先测试了一下 adb shell df，可以正常看到手机的磁盘信息。

然后执行 adb shell "settings put global captive_portal_detection_enabled 0"。

重启手机，连上 WiFi，感叹号消失，搞定！

