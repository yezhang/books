\# HTML 语义化



HTML 的语义是指元素、属性、属性值的在规范中的特定含义。一个建议是：在恰当的需求下使用恰当的HTML元素。为了能够使用恰当的 HTML 元素，可以这样做：在选择 HTML 元素时，询问自己一个问题“哪个（哪些）元素可以最恰当的表达我要生成的数据？”。



&lt;a name="SVmuK"&gt;&lt;/a&gt;

\#\#\#\# 元素选择

判断 HTML 元素是否恰当的标准是：在一个页面中，HTML 元素正确传达了 HTML 规范中固有含义。在 HTML 规范中，使用『\[represent\]\(https://www.w3.org/TR/html52/dom.html\#represent\)（表达）』关键词描述一个元素的固有含义，也就是我们所说的语义。

&gt; 例：

&gt; 一个 &lt;ol&gt; 元素『表达』了一个有序列表。





为了更好的使用元素，首先需要对 HTML 规范中定义的元素有一个全面了解。规范中，有关语义化的章节有：3.2.5 \[全局属性\]\(https://www.w3.org/TR/html52/dom.html\#global-attributes\)、4.2 \[文档元数据\]\(https://www.w3.org/TR/html52/document-metadata.html\#document-metadata\)、4.3 \[区块\]\(https://www.w3.org/TR/html52/sections.html\#sections\)、4.4 \[分组内容\]\(https://www.w3.org/TR/html52/grouping-content.html\#grouping-content\)、4.5 \[文本级语义\]\(https://www.w3.org/TR/html52/textlevel-semantics.html\#textlevel-semantics\)、4.6 \[更改记录\]\(https://www.w3.org/TR/html52/edits.html\#edits\)、4.7 \[嵌入内容\]\(https://www.w3.org/TR/html52/semantics-embedded-content.html\#semantics-embedded-content\)、4.8 \[链接\]\(https://www.w3.org/TR/html52/links.html\#links\)、4.9 \[表格\]\(https://www.w3.org/TR/html52/tabular-data.html\#tabular-data\)、4.10 \[表单\]\(https://www.w3.org/TR/html52/sec-forms.html\#sec-forms\)。



使用语义化标签具有一些好处（\[https://developer.mozilla.org/en-US/docs/Glossary/Semantics\]\(https://developer.mozilla.org/en-US/docs/Glossary/Semantics\)）：



- \[SEO\]\(https://developer.mozilla.org/en-US/docs/Glossary/SEO\)：搜索引擎会把其内容作为重要的关键词，进而影响页面搜索排名。

- 可访问性：读屏软件可以把其内容作为一个关键标记，方便视觉障碍的用户导航一个页面内容。

- 开发者友好：搜索语义化的代码块会比搜索没有具体含义的 div 更容易。

- 开发者友好：向开发者提示页面中所需要生成数据的类型。

- 开发者友好：语义化命名可以反映出自定义的元素/组件命名。



常见的语义化元素有：



- \[&lt;article&gt;\]\(https://www.w3.org/TR/html52/sections.html\#the-article-element\)

- &lt;aside&gt;

- &lt;details&gt;

- &lt;figcaption&gt;

- &lt;figure&gt;

- &lt;footer&gt;

- &lt;header&gt;

- &lt;main&gt;

- &lt;mark&gt;

- &lt;nav&gt;

- &lt;section&gt;

- &lt;summary&gt;

- &lt;time&gt;



同时，需要注意避免错误的使用 HTML 标签（参考\[这篇文章\]\(https://www.lifewire.com/why-use-semantic-html-3468271\)）：有些开发者错误地使用\`blockquote\`、\`&lt;p&gt;&nbsp;&lt;/p&gt;\`、\`ul\`来添加文本缩进，在没有「标题」语义的文本中，错误地使用 h1–h6 改变字体大小。当我们需要添加文本缩进时，应考虑使用 CSS 中的 margin、padding。当需要修改文字大小时，考虑使用 font-weight、font-size。



&lt;a name="kUsXS"&gt;&lt;/a&gt;

\#\#\#\# 语义的扩展性

John Allsopp 在 2009 年的一篇\[文章\]\(http://alistapart.com/article/semanticsinhtml5/\)中讨论了通过增加新的元素扩展现有 HTML 语义的做法。 作者认为，一个可扩展的语义化机制，需要满足两个约束：一是向后兼容，能够在老旧的浏览器中正确渲染页面；二是向前兼容，面向未来，这个扩展机制下的页面需要能够在未来的浏览器中正常工作。这两个约束合在一起，带来巨大的挑战。



HTML5 通过\*\*添加新元素\*\*来增强语义化能力的做法，不能满足上述两个约束。既不能保证新元素在老旧浏览器中正确渲染，也没有提供在未来添加新的语义的机制。



一直以来，开发者使用 id 属性、class 属性作为扩展语义的方法。此外，\*\*添加新的属性\*\*（attribute）也是一种可以考虑的方法。添加新属性的方法在「向后兼容」的问题上可以做的更好，然而，该方法也会面临“词汇选择”（使用哪些词汇表达属性）、“属性数量”（选用多少个属性）、“术语冲突”（不同的词汇表达相同的意思）等问题。



另外一篇\[文章\]\(http://html5doctor.com/microdata/\)介绍了使用 \*\*Microdata\*\* 来扩展 HTML5 中的语义。这种方法在最新的规范中已经被废弃。



\[\*\*Microformat\*\*\]\(http://microformats.org/wiki/Main\_Page\) （微格式，有时缩写为μF）提供了 HTML 标记实体的一组约定。利用微格式，可以标记的实体包括人、组织、事件、地点、博客、产品、评论、简历、食谱等。常见的微格式样例，可以参考这篇\[文章\]\(https://developer.mozilla.org/en-US/docs/Web/HTML/microformats\)。



使用 \*\*「data-\*」 属性\*\*也是扩展语义的方法，开发者可以通过该属性添加自定义数据。每个 HTML 元素都可以拥有任意数量的自定义数据属性以及任意的值。需要注意，自定义数据属性\[不应该\]\(http://html5doctor.com/html5-custom-data-attributes/\)用于 CSS 样式。



&lt;a name="z87zn"&gt;&lt;/a&gt;

\#\#\#\# 扩展阅读



1. 除了 HTML 语义，还有 CSS 语义、JavaScript 语义等方面：\[https://developer.mozilla.org/en-US/docs/Glossary/Semantics\]\(https://developer.mozilla.org/en-US/docs/Glossary/Semantics\)

1. 一个拥有良好语义化文本的示例，\[https://mdn.github.io/learning-area/accessibility/html/good-semantics.html\]\(https://mdn.github.io/learning-area/accessibility/html/good-semantics.html\)





