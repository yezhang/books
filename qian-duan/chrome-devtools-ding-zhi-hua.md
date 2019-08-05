# Chrome DevTools 定制化

### 定制化步骤

1、准备代码

2、初步编译

3、修改代码、编译、调试

Chrome DevTools 的编译，依赖于 Chrome 源码。所以，首先需要将完整的 Chrome 代码下载到本地，并配置编译参数。

准备代码

Chrome 源码可以从两个位置获取，一是谷歌官方托管地址，二是 github 镜像。

1、从官方地址获取源码的方法为：https://www.chromium.org/developers/how-tos/get-the-code

2、从 github 镜像获取源码的地址为：https://github.com/chromium/chromium

MacOS 获取 Chrome 源码的官方说明：https://chromium.googlesource.com/chromium/src/+/master/docs/mac\_build\_instructions.md\#Get-the-code



Chrome DevTools 源码位置：

[https://github.com/ChromeDevTools/devtools-frontend](https://github.com/ChromeDevTools/devtools-frontend)



修改 DevTools 源码后，如何重新编译更新？

1、将前端 UI 的代码拷贝放置到 Chrome 代码库下：third\_party/blink/renderer/devtools/

设置构建参数：

[https://gist.github.com/paulirish/2d84a6db1b41b4020685\#file-args-gn](https://gist.github.com/paulirish/2d84a6db1b41b4020685#file-args-gn)

在 src 目录执行 gn 命令。

推荐的编译选项：https://gist.github.com/paulirish/2d84a6db1b41b4020685\#file-args-gn



下载源码的方法：

\[ \] Getting sources: bullet-proof，[https://medium.com/@aslushnikov/hacking-chrome-devtools-8c8896f5cef3](https://medium.com/@aslushnikov/hacking-chrome-devtools-8c8896f5cef3)

参考资料

* [Chrome DevTools Contribution Guide](https://docs.google.com/document/d/1WNF-KqRSzPLUUfZqQG5AFeU_Ll8TfWYcJasa_XGf7ro/view#)



