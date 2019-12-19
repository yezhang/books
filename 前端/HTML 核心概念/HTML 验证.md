# HTML 验证

HTML 验证是指校验 HTML 标签的有效性。HTML 语言有其特有的文法、词汇、句法，使用 HTML 语言书写的文档，需要符合这些规则。然而在编写过程中，HTML 文档可能会遇到拼写错误、语法错误等。HTML 验证便是确认 HTML 文档是否符合这些规则的过程。所使用的工具，称为验证器。如果一个 HTML 文档被成功验证，则称这个文档是有效的。

我们可以使用 W3C 提供的 [Markup Validation Service](https://validator.w3.org/) 验证 HTML 文档的有效性。该验证服务是基于 DTD（文档类型定义）的。除了该服务，我们还可以使用[非 DTD 的标签验证服务](https://validator.w3.org/nu/)。

Markup Validation Service 截图如下：

![](/assets/HTML验证/Markup&#32;Validation&#32;Service&#32;截图.png)

验证结果如下图-2所示。

![](/assets/HTML验证/验证结果.png)

可以在 图-2 的验证结果中，查看页面中的错误。

一些第三方 HTML 验证工具提供了 Firefox、Chrome 插件可以供我们使用，例如 [http://users.skynet.be/mgueury/mozilla/](http://users.skynet.be/mgueury/mozilla/)。


## 扩展阅读

* MDN 上罗列了一些 Web 验证工具，https://developer.mozilla.org/en-US/docs/Tools/Validators