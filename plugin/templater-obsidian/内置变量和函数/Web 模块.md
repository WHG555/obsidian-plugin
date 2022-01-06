# Web 模块

该模块包含与网络相关的每个内部变量/函数（使用网络请求）。

默认情况下，[[../Templater/Templater]]不转义字符。在执行 Web 请求时，转义危险字符可能很有用。您可以使用 `<%~` 开始标记转义命令的响应字符。更多信息在[这里](../命令/概述)。

## 文档

> 函数文档使用特定的语法。更多信息 [函数文档语法](../Templater/语法.md#函数文档语法)

|                     内部变量/函数                      |                             参数                             |                      说明                      | 输出 |
| :----------------------------------------------------: | :----------------------------------------------------------: | :--------------------------------------------: | :--: |
|                 `tp.web.daily_quote()`                 |                             None                             | 从 API 检索和解析每日名言 https://quotes.rest/ |  略  |
| `tp.web.random_picture(size?: string, query?: string)` | \- `size`: 格式中的图像大小`<width>x<height>`.<br/>\- `query`:将选择限制为与搜索词匹配的照片。多个搜索词可以用逗号`,`分隔 |    从  https://unsplash.com/ 中获取随机图像    |  略  |

## 示例

```js
Web Daily quote:  
<% tp.web.daily_quote() %>

Web Random picture: 
<% tp.web.random_picture() %>

Web Random picture with size: 
<% tp.web.random_picture("200x200") %>

Web random picture with size + query: 
<% tp.web.random_picture("200x200", "landscape,water") %>
```

上一节： [系统模块](系统模块.md)下一节：[贡献](贡献.md)