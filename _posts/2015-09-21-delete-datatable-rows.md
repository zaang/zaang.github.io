---
layout: post
category: windows
title: ---
layout: post
category: windows
title: 删除 DataTable 的多行
tagline: 2015-09-21
tags: [windows]
---

笔记回顾，删除 DataTable 的多行。

<!--more-->

调用 DataRow 对象的 Delete() 方法后，行对象还未实际删除，需要调用 DataTable 的 AccepteChanges() 方法接受变更才真正删除。在 AccepteChanges() 之前可以通过 RejectChanges() 回滚，使该行取消删除。

删除 DataTable 中已有的 DataRow，是把 DataRow 的 RowState 改为 DataRowState.Deleted。

** 但是 **，如果 DataRow 是刚刚添加的，RowState 是 DataRowState.Added 时，这时候 Delete() 方法会把 DataRow 从行集合中移除。

假如我们这么删除全部的行，如果没有新行，看不出问题。但是如果有 RowState 是 DataRowState.Added 的行，每删除一次这样的行，DataTable.Rows.Count 就会减去 1。最终结果就会删除不完全。

    for (var i = 0; i < datatable.Rows.Count; i++)
    {
        if (datatable.Rows[i].RowState != DataRowState.Deleted)
            datatable.Rows[i].Delete();
    }

正确的方法应该采用倒序循环删除：

    for (var i = datatable.Rows.Count - 1; i >= 0; i--)
    {
        if (datatable.Rows[i].RowState != DataRowState.Deleted)
            datatable.Rows[i].Delete();
    }
