# 介绍

[Templater](https://github.com/SilentVoid13/Templater) 允许你给笔记插入 **变量** 和 **函数** ，同时它允许你使用 JavaScript 代码操作 **变量** 和 **函数**。

通过 [Templater](https://github.com/SilentVoid13/Templater)，你可以创建强大的模板来自动管理任务。

## 快速示例

下面是一个使用 [Template](https://github.com/SilentVoid13/Templater) 语法的模板文件。

```js
---
创建时间: <% tp.file.creation_date() %>
修改时间: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
---
# 显示当前时间 前一天 | 后一天
<< [[<% tp.date.now("YYYY-MM-DD", -1) %>]] | [[<% tp.date.now("YYYY-MM-DD", 1) %>]] >>
# 显示文件名
<% tp.file.title %>
# 给日记插入一条随机名言
<% tp.web.daily_quote() %>
```

当插入后会显示下面的结果：

```js
---
creation date: 2021-01-07 17:20
modification date: Thursday 7th January 2021 17:20:43
---

<< [[2021-04-08]] | [[2021-04-10]] >>

# Test Test

> Do the best you can until you know better. Then when you know better, do better.
> &mdash; <cite>Maya Angelou</cite>
```

下一节 [安装](安装.md)