# OllyDbg v1.10 插件开发



## 开发环境

Windows 7

Visual Studio 2013



编写入口点函数

```cpp
BOOL APIENTRY DllMain(	HMODULE hModule,DWORD  ul_reason_for_call, LPVOID lpReserved)
```

官方插件文档中所说的入口点函数 DllEntryPoint 经过试验无法生效。

