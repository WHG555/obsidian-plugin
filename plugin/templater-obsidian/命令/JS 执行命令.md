## JS 执行命令

这种类型的命令允许我们执行 JavaScript 代码。

使用 JavaScript 执行命令，我们几乎可以做 JavaScript 允许我们做的所有事情。下面给出了一些例子。

我们仍然可以从这种类型的命令访问 `tp` 对象和所有内部变量/函数。

> TIP
>
> JavaScript 执行命令允许您访问全局命名空间变量。这意味着您可以访问诸如“app”或“moment”之类的内容。

##### 

> INFO
>
> 一些内部函数是异步的。在 JavaScript 执行命令中调用此类函数时，如有必要，请不要忘记使用 `await` 关键字。

## 如何从 JavaScript 执行命令输出值？

有时，您可能希望在使用 JS 执行命令时输出一些内容。尽管原始显示/插值命令更可取，但这是可能的。

当 [Eta](https://eta.js.org/) 模板引擎使用我们所有的命令结果生成替换字符串时，它会存储在名为 `tR` 的变量中。这是将包含已处理文件内容的字符串。您可以从 JS 执行命令访问该变量。

这意味着，要从 JS 执行命令输出某些内容，您只需要将要输出的内容附加到该 `tR` 字符串变量中。

例如，以下命令：`<%* tR += "test" %>` 将输出 `test`。

## 示例

以下是一些您可以使用 JavaScript 执行命令执行的操作示例：

```js
<%* if (tp.file.title.startsWith("Hello")) { %>
This is a hello file !
<%* } else { %>
This is a normal file !
<%* } %>
    
<%* if (tp.frontmatter.type === "seedling") { %>
This is a seedling file !
<%* } else { %>
This is a normal file !
<%* } %>
    
<%* if (tp.file.tags.contains("#todo")) { %>
This is a todo file !
<%* } else { %>
This is a finished file !
<%* } %>

<%*
function log(msg) {
    console.log(msg);
}
%>
<%* log("Title: " + tp.file.title) %>
    
<%* tR += tp.file.content.replace(/stuff/, "things"); %>
```

上一节： [概述](概述.md)下一节：[动态命令](动态命令.md)