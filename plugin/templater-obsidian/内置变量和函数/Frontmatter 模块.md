# Frontmatter 模块

该模块将文件的所有 frontmatter 变量公开为内部变量。

## 文档

> 函数文档使用特定的语法。更多信息 [函数文档语法](../Templater/语法.md#函数文档语法)

|                内部变量/函数                 | 参数 |              说明               |  输出   |
| :------------------------------------------: | :--: | :-----------------------------: | :-----: |
| `tp.frontmatter.<frontmatter_variable_name>` | None | 检索文件的 frontmatter 变量值。 | `value` |

> - 如果您的 frontmatter 变量名称包含空格，您可以使用括号表示法引用它，如下所示：
>
>   `<% tp.frontmatter["variable name with spaces"] %>`

## 示例

假设您有以下文件：

```markdown
---
alias: myfile
note type: seedling
---

file content
```

然后您可以使用以下模板：

```js
File's metadata alias: <% tp.frontmatter.alias %>
Note's type: <% tp.frontmatter["note type"] %>
```

上一节：[系统模块](系统模块.md)下一节：[Obsidian 模块](Obsidian%20模块.md)