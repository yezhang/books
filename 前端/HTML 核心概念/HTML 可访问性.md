# HTML 可访问性

提高可访问性（Accessibility）是指让我们的网站被尽可能多的人使用的做法。既包括传统上的残障人士，又包括移动设备的人群，还包括网络访问缓慢的人群。实际上，可访问性是关乎每一个人的，无论人们的环境或能力如何。每个人都可以从提高可访问性的做法中收益。



#### 基本内容

HTML 的可访问性与其语义化息息相关。良好的页面语义是可访问性的重要基础，我们应尽可能使用正确的 HTML 标签表达正确的意图。一个具有标题、段落、列表的良好结构的页面，对于屏幕阅读器用户来说是非常有意义的。同时，语义化的 HTML 提高了搜索引擎排名，使得我们的网站更容易被人们获得。

传统上的残障人士包括有视觉障碍的人（辅助方法：利用屏幕阅读器/读屏软件）、有听力障碍的人（暂时没有辅助技术）、有行动障碍的人（辅助方法：使用键盘控制、使用 Tab 移动**焦点**）、有认知障碍的人（辅助方法：页面风格一致、逻辑清晰、语言简单、重点突出、错误明显）等。

常见的可访问性问题可以参考这篇[文章]([https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility)。文中除了总结常见问题外，还介绍了一些可访问性测试工具（键盘导航、颜色对比度检查、页面审查工具、读屏软件、语音合成器）。](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility%29。文中除了总结常见问题外，还介绍了一些可访问性测试工具（键盘导航、颜色对比度检查、页面审查工具、读屏软件、语音合成器）。)



#### 工作清单

关注网站的可访问性可以将「访问性测试」做为起点。可以通过下面这个清单，测试我们网站的可访问性：

* [ ] 1、确保 HTML 页面是尽可能的语义正确。使用[验证工具]([https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/HTML_and_CSS#Validation)、审查工具来做到这一点。

* [ ] 2、在 CSS 样式禁用时，保证站点内容有意义。

* [ ] 3、保证功能是键盘可访问的，例如测试 Tab、Enter 按键的功能。

* [ ] 4、确保非文本内容（如图片、视频）具有[替代文本]([https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML#Text_alternatives)（还可以阅读这篇[文章](https://developers.google.com/web/fundamentals/accessibility/semantics-builtin/text-alternatives-for-images?hl=zh-cn)）。

* [ ] 5、检查网站颜色的对比度。比如使用这个[工具]([https://webaim.org/resources/contrastchecker/)来检查，在 MacOS 系统中还可以使用 [Colour Contrast Analyser](https://developer.paciellogroup.com/resources/contrastanalyser/) App，或是这个[工具](https://usecontrast.com)。

* [ ] 6、确保被隐藏的内容在屏幕阅读器下是可见的。

* [ ] 7、在任何可能的位置，确保没有 JavaScript 时，功能仍然可用。

* [ ] 8、在合适的位置，使用 [ARIA]([https://developer.mozilla.org/en-US/docs/Learn/Accessibility/WAI-ARIA_basics](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/WAI-ARIA_basics)) 技术增强可访问性。

* [ ] 9、通过[审查工具](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility#Auditing_tools)(例如，[Chrome 插件 aXe](https://chrome.google.com/webstore/detail/axe/lhdoppojpmngadmnindnejefpokejbdd))测试整个站点。

* [ ] 10、使用读屏软件测试站点。

* [ ] 11、在站点中说明可访问性的策略或声明，来告知用户本站所支持的可访问性内容。

最后需要说明的是，我们应在项目一开始就关注可访问性，并尽早进行可访问性测试。



#### 扩展阅读

1. 可访问性的介绍性文章：[https://developer.mozilla.org/zh-CN/docs/Learn/Accessibility/What_is_accessibility](https://developer.mozilla.org/zh-CN/docs/Learn/Accessibility/What_is_accessibility)

2. MDN 可访问性：[https://developer.mozilla.org/zh-CN/docs/Learn/Accessibility](https://developer.mozilla.org/zh-CN/docs/Learn/Accessibility)

3. 可访问性的诊断可以参考这篇文章，[https://developer.mozilla.org/en-US/docs/Learn/Accessibility/Accessibility_troubleshooting](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/Accessibility_troubleshooting)

4. 阅读有关“可访问性”（或“无障碍”）的方方面面：[https://developer.mozilla.org/en-US/docs/Web/Accessibility](https://developer.mozilla.org/en-US/docs/Web/Accessibility)

5. Google Web Fundamental 中有关「无障碍」的一系列文档：[https://developers.google.com/web/fundamentals/accessibility/?hl=zh-cn](https://developers.google.com/web/fundamentals/accessibility/?hl=zh-cn)



