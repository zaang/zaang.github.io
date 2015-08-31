---
layout: post
category: windows
title: Devexpress Chart Note
tagline: 2015-08-24
tags: [windows, .net]
---

关于 Devexpress 中 Chart 的一些记录。

<!--more-->

版本：13.2

### 1. 运行时修改坐标轴最大值

直接修改属性运行时报错，需要调用下面的接口

    XYDiagram.AxisX.VisualRange.SetMinMaxValues(object min, object max);
    XYDiagram.AxisX.WholeRange.SetMinMaxValues(object min, object max);

如果还有问题，那就是没把自动取消

    xyDiagram1.AxisX.VisualRange.Auto = false;
    xyDiagram1.AxisX.WholeRange.Auto = false;

### 2. 坐标轴单位

如修改 Y 轴单位为“万元”时

    xyDiagram1.AxisY.Label.EndText = "万元";

### 3. 坐标轴精度

如X轴是日期类型，需要只显示月份，但是精度又是为天时

    xyDiagram.AxisX.DateTimeScaleOptions.MeasureUnit = DateTimeMeasureUnit.Day;
    xyDiagram.AxisX.DateTimeScaleOptions.GridAlignment = DateTimeGridAlignment.Month;

### 4. 坐标轴刻度文本交错显示问题

修改 AllowStagger 属性

    xyDiagram1.AxisX.Label.ResolveOverlappingOptions.AllowStagger = false;
