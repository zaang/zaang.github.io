---
layout: post
category: android
title: Fix VS Reference Conflict
tagline: 2015-10-29
tags: [csharp]
---

VS2013 项目中遇到警告"发现同一依赖程序集的不同版本间存在无法解决的冲突"的解决过程。

<!--more-->

1. 通过菜单 工具->选项 的窗口中找到 项目和解决方案->生成并运行，修改“MSBuild 项目生成输出详细信息”的选项为详细。
2. 通过菜单 视图->输出 显示输出窗口。
3. 重新生成项目，在输出窗口中检索“冲突”，找到引发警告的地方，就知道原因了。

> 请考虑使用 app.config 将程序集“System.Data.SQLite, Culture=neutral, PublicKeyToken=db937bc2d44ff139”从版本“1.0.94.0”[]重新映射到版本“1.0.98.0”[E:\DotNET\TBIM2015\Client\bin\System.Data.SQLite.dll]，以解决冲突并消除警告。
