---
layout: post
category: Windows
title: Redirect CMD Output
tagline: 2015-01-23
tags: [windows, .net]
---

今天遇到一个进程调用控制台程序阻塞的问题。

<!--more-->

在程序中调用7z解压文件，今天解压一个大文件时，发现总是解压时卡住。

    var process = new Process();
    process.StartInfo.FileName = fileName;
    process.StartInfo.Arguments = arguments;
    process.StartInfo.CreateNoWindow = createNoWindow;
    if (createNoWindow)
    {
        process.StartInfo.UseShellExecute = false;
        process.StartInfo.RedirectStandardInput = true;
        process.StartInfo.RedirectStandardOutput = true;
        process.StartInfo.RedirectStandardError = true;
    }
    process.Start();
    process.WaitForExit();

但是不隐藏控制台窗口时，程序是顺利执行的。查询了相关资料，控制台重定向输出时，是通过管道实现的。

当管道数据达到上限时，会等待数据被读取，在数据被读取之前，是无法继续写入的，程序因此阻塞。考虑到这里我不关心输出结果，于是将重定向都改为false解决。

    process.StartInfo.RedirectStandardInput = false;
    process.StartInfo.RedirectStandardOutput = false;
    process.StartInfo.RedirectStandardError = false;

