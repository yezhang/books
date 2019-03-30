# 使用 SourceMap 调试线上代码

[https://developers.google.com/web/tools/chrome-devtools/javascript/source-maps?hl=zh-cn](https://developers.google.com/web/tools/chrome-devtools/javascript/source-maps?hl=zh-cn)

SourceMap 文件部署：

存放在远程服务器

存放在本地服务器

### 线上调试注意问题：

不同版本的线上前端代码要能够找到对应的 SourceMap 文件夹。



### 使用本地服务器调试线上代码

进入 dist 目录，

启动 SourceMap 本地服务器：http-server ./ -p 8080

