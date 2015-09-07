---
layout: post
category: windows
title: Revit Base Point
tagline: 2015-09-07
tags: [windows, .net, revit]
---

获取 Revit 中的项目基点。

<!--more-->


### 1. 在 Revit 中显示项目基点

点击菜单 '视图' -> '可见性/图形' 或使用快捷键 'VV'，在弹出的对话框中的「模型类别」标签页下的过滤器列表中找到“场地”节点下的“项目基点”与“测量点”。，打勾并应用退出。

> 测量点：项目在世界坐标系中实际测量定位的参考坐标原点。
> 项目基点：项目在用户坐标系中测量定位的相对参考坐标原点。

### 2. 从数据库查看

下载 RevitLookup 插件，把“RevitLookup.addin”与“RevitLookup.dll”放到 Revit 的插件目录下，我这里是“C:\ProgramData\Autodesk\Revit\Addins\2014”。

然后在 Revit 的附加模块中就能看到 Revit Lookup 了。从菜单 'Snoop DB...' -> 'BasePoint' 就看到项目基点了。

### 3. 获取项目基点

在插件中获取项目基点的代码：

    ElementCategoryFilter siteCategoryfilter = new ElementCategoryFilter(BuiltInCategory.OST_ProjectBasePoint);
    FilteredElementCollector collector = new FilteredElementCollector(doc);
    IList<Element> siteElements = collector.WherePasses(siteCategoryfilter).ToElements();

    foreach (Element ele in siteElements)
	{
        double x = ele.get_Parameter(BuiltInParameter.BASEPOINT_EASTWEST_PARAM).AsDouble();
        double y = ele.get_Parameter(BuiltInParameter.BASEPOINT_NORTHSOUTH_PARAM).AsDouble();
        double elev = ele.get_Parameter(BuiltInParameter.BASEPOINT_ELEVATION_PARAM).AsDouble();
        double angle = ele.get_Parameter(BuiltInParameter.BASEPOINT_ANGLETON_PARAM).AsDouble();
	}

项目基点除了有 XYZ 的偏移，还有角度的。

设Revit中的项目基点为(a, b, c)，角度为angle。将Revit中坐标按项目基点为(x, y, z)变换为按测量点的坐标时，要先根据角度angle对XY坐标进行变换：

    double newx = (x * Math.Cos(angle)) - (y * Math.Sin(angle));
    double newy = (x * Math.Sin(angle)) + (y * Math.Cos(angle));

然后对项目基点进行偏移，最终偏移后的坐标为：

    var result = new XYZ(newx + a, newy + b, z + c);

> 这里获取的项目基点坐标单位是英寸，最终结果是需要根据实际单位换算的。

