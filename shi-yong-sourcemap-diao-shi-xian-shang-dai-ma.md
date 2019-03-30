# 使用 SourceMap 调试线上代码

[https://developers.google.com/web/tools/chrome-devtools/javascript/source-maps?hl=zh-cn](https://developers.google.com/web/tools/chrome-devtools/javascript/source-maps?hl=zh-cn)

[https://itnext.io/using-sourcemaps-on-production-without-revealing-the-source-code-️-d41e78e20c89](https://itnext.io/using-sourcemaps-on-production-without-revealing-the-source-code-️-d41e78e20c89)

SourceMap 文件部署：

存放在远程服务器

存放在本地服务器

### 线上调试注意问题：

不同版本的线上前端代码要能够找到对应的 SourceMap 文件夹。

### 使用本地服务器调试线上代码

进入 dist 目录，

启动 SourceMap 本地服务器：http-server ./ -p 8080

线上调试方案1（Fiddler 代理）

方法1：在本地切换到线上环境对应的源码，找到源码后，直接使用 Fiddler 将线上代码的 index.html 映射到源码文件中。

该方法前提：源码可以直接运行。

方法2：在本地切换到线上环境对应的源码，启动本地开发服务器，直接使用 Fiddler 将线上 index.html 映射到本地开发服务器的 URL 地址。

该方法的限制：线上环境是 HTTPS，Fiddler 将线上 URL 映射到本地开发服务器的 URL 时，会无法访问资源。本地开发服务器为 HTTP。



SourceMap 文件中可能包含源码内容也可以不包含，如果不包含源码内容，则可以用来映射客户端上的堆栈。

