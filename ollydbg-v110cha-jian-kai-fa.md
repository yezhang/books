# OllyDbg v1.10 插件开发

## 开发环境

* Windows 7
* Visual Studio 2013

## 基础知识准备

OllyDbg插件生命周期

采用静态链接的方式，使得开发的插件只有一个dll，避免对于多种dll环境的依赖。

## 创建项目

1、使用Win32空项目，配置项目属性为dll。

2、为项目添加MFC资源。

![](/assets/resource.png)

## 样例代码说明

编写入口点函数

```cpp
BOOL APIENTRY DllMain(HMODULE hModule,DWORD  ul_reason_for_call, LPVOID lpReserved)
```

官方插件文档中所说的入口点函数 DllEntryPoint 经过试验无法生效。

## 遇到的问题

键盘事件无效：DLL中的MFC窗口是可以正确建立自己的消息循环的，如果重载 DefWindowProc 函数，可以发现该函数被多次调用。在普通的MFC应用中，PreTranslateMessage可以用于处理快捷键消息。但是，在DLL中PreTranslateMessage函数不会被调用。

OD事件传递：在MainFrame中定义【自定义消息】或者根据[官网](https://docs.microsoft.com/zh-cn/cpp/mfc/tn011-using-mfc-as-part-of-a-dll#winmain---dllmain "dllmain")介绍，调用 CWinApp::PreTranslateMessage。

## 调试OllyDBG插件

在VS的项目属性页，设置 【调试】--&gt;【命令】为 &lt;OllyDBG.exe&gt; 的路径。如下图所示。

![](/assets/vs-project-properties.png)

之后，点击 F5 执行即可。

如果出现以下窗口，点击【是】继续调试。

![](/assets/debug-warning.png)

本设置参考资料是：[https://msdn.microsoft.com/zh-cn/library/c91k1xcf.aspx](https://msdn.microsoft.com/zh-cn/library/c91k1xcf.aspx)

## 常见问题

问题1：在运行过程中，如果出现断言错误，如下：

```cpp
ENSURE(str.LoadString(IDS_AFXBARRES_CLOSEBAR));
m_btnClose.SetTooltip(str);

ENSURE(str.LoadString(IDP_AFXBARRES_SCROLL_LEFT));
m_btnScrollLeft.SetTooltip(str);

ENSURE(str.LoadString(IDP_AFXBARRES_SCROLL_RIGHT));
m_btnScrollRight.SetTooltip(str);
```

解决方案：[https://social.msdn.microsoft.com/Forums/vstudio/en-US/5d84c08f-fbb6-4233-98f1-53adb8cbc50b/loadstringids-cause-exception-in-vc-2008-with-featured-pack-for-upgraded-project?forum=vcgeneral](https://social.msdn.microsoft.com/Forums/vstudio/en-US/5d84c08f-fbb6-4233-98f1-53adb8cbc50b/loadstringids-cause-exception-in-vc-2008-with-featured-pack-for-upgraded-project?forum=vcgeneral)

> it's a known problem for statically linked projects using the feature pack.  You have to include afxribbon.rc in your resource file.  See [http://forums.msdn.microsoft.com/en-US/vcgeneral/thread/7245ee72-ffd5-4167-b690-c2edc10fb88e/](http://forums.msdn.microsoft.com/en-US/vcgeneral/thread/7245ee72-ffd5-4167-b690-c2edc10fb88e/) for more info.

在资源文件中，添加如下指令：

```
#if !defined(_AFXDLL)
#include "afxribbon.rc"              // MFC ribbon and control bar resources
#endif
```

问题2：OllyDBG的插件有哪些？

> [https://github.com/Hack-with-Github/Powerful-Plugins/blob/master/OllyDbg.md](https://github.com/Hack-with-Github/Powerful-Plugins/blob/master/OllyDbg.md)

## 附录

### MFC类型继承结构

### ![](/assets/class-inherit.png)

### 

### 

### 

## 参考资料

1. 在 Win32 DLL 中使用MFC，[http://www.cnblogs.com/dcai/archive/2011/10/12/2208052.html](http://www.cnblogs.com/dcai/archive/2011/10/12/2208052.html)
2. 将MFC作为DLL的一部分，[https://msdn.microsoft.com/en-us/library/zfz4xb9a.aspx](https://msdn.microsoft.com/en-us/library/zfz4xb9a.aspx)
3. MFC作为DLL的样例代码，[https://github.com/Microsoft/VCSamples/tree/master/VC2010Samples/MFC/advanced/DllScreenCap](https://github.com/Microsoft/VCSamples/tree/master/VC2010Samples/MFC/advanced/DllScreenCap)



