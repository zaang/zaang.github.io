---
layout: post
category: windows
title: ---
layout: post
category: windows
title: A Csharp Interview Question
tagline: 2015-10-20
tags: [windows, mysql, asp.net]
---

一道关于 csharp try 的笔试问题

<!--more-->

大概是这样的：

    void Function()
    {
        try
        {
            return;
        }
        finally
        {
            Console.WriteLine("Hello World!");
        }
    }

- A. 编译报错，因为没有 catch 任何异常
- B. 运行时报错
- C. 未输出任何结果
- D. 输出 Hello World!

------

<br>
<br>
答案 D

