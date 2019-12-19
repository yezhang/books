# 文档类型定义



文档类型定义（Document Type Definition，简称 DTD）的概念缘于 SGML，每一份 SGML 文件，均应有相对应的 DTD。SGML 是指[标准通用标记语言](https://www.w3.org/TR/WD-html40-970708/intro/sgmltut.html)（Standard Generalized Markup Language），是现时常用的超文本格式的最高层次标准，是可以定义标记语言的元语言。我们所熟知的 HTML 是 SGML 的一种应用，XML 则是 SGML 的一个子集（然而按照集合论定义严格说来，XML不是 SGML 子集，参考[这篇文章](https://stackoverflow.com/questions/18463320/is-xhtml-a-subset-of-html)）。


DTD 的作用是定义 XML 文档的合法构建模块。DTD 可被成行地声明于 XML 文档中，也可作为一个外部引用。


DTD 与文档类型声明（Document Type Declaration）相关。在HTML中，文档类型声明是必要的。所有的文档的头部，我们都将会看到"&lt;!DOCTYPE html&gt;" 的身影。DOCTYPE 便是用来声明文档类型和 DTD 规范的，一个用途便是验证文件的合法性。 W3C 推荐的文档类型声明方法，请参考：[https://www.w3.org/QA/2002/04/valid-dtd-list.html](https://www.w3.org/QA/2002/04/valid-dtd-list.html)。



需要注意的是，HTML5 是没有对应的 DTD 的。早期的 HTML 版本（HTML 4.01）是基于 SGML, DTD 的作用在于定义 SGML 文档的文档类型以便于浏览器解析。HTML5 不再基于 SGML, 因此不再需要 DTD，而是简化为&lt;!DOCTYPE html&gt;。这个声明的目的是防止浏览器在渲染文档时，切换到我们称为“怪异模式(兼容模式)”的渲染模式。



HTML 4.01 的 DTD 内容，请参考 [https://www.w3.org/TR/REC-html40/sgml/dtd.html](https://www.w3.org/TR/REC-html40/sgml/dtd.html)。



&lt;a name="DgVcn"&gt;&lt;/a&gt;

#### 扩展阅读

HTML5 没有文档类型定义（DTD）的原因，请参考：[https://stackoverflow.com/questions/4053917/where-is-the-html5-document-type-definition](https://stackoverflow.com/questions/4053917/where-is-the-html5-document-type-definition)





