# OllyDbg v1.10 插件开发

## 开发环境

* Windows 7
* Visual Studio 2013

## 基础知识准备

OllyDbg插件生命周期

## 样例说明

编写入口点函数

```cpp
BOOL APIENTRY DllMain(    HMODULE hModule,DWORD  ul_reason_for_call, LPVOID lpReserved)
```

官方插件文档中所说的入口点函数 DllEntryPoint 经过试验无法生效。

## 调试OllyDBG插件

在VS的项目属性页，设置 【调试】--&gt;【命令】为 &lt;OllyDBG.exe&gt; 的路径。如下图所示。

![](/assets/vs-project-properties.png)

之后，点击 F5 执行即可。

本设置参考资料是：https://msdn.microsoft.com/zh-cn/library/c91k1xcf.aspx



