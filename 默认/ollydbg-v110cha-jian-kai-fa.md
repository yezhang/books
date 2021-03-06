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

在 PluginApp 中加载快捷键资源。经过测试，重载 CMDIFrameWndEx::WindowProc 方法，在 WM\_CREATE 消息中添加系统快捷键可以成功响应键盘事件。此方法添加的是操作系统级别的快捷键，添加代码如下。

```cpp
LRESULT CMainFrame::WindowProc(UINT message, WPARAM wParam, LPARAM lParam)
{

    switch (message)
    {
    case WM_CREATE:
        RegisterHotKey(
            this->GetSafeHwnd(),   // 注册快捷键的窗口句柄
            1,      // 热键标识符避免热键冲突
            MOD_CONTROL | MOD_NOREPEAT, // Ctrl 键  No Repeat 不重复发送
            'A'     // A
            );
        break;
    default:
        break;
    }
}
```

这种方法注册的系统级别快捷键，无论按下快捷键的时候OD是否激活、本插件是否激活，都会触发 WM\_HOTKEY 消息。在程序设计上，不推荐使用。

手动接受OD的快捷键，并执行消息转换。手动构造 TranslateAccelerator 需要的参数。

wParam 控制虚拟按键，[https://msdn.microsoft.com/en-us/library/windows/desktop/dd375731\(v=vs.85\).aspx](https://msdn.microsoft.com/en-us/library/windows/desktop/dd375731%28v=vs.85%29.aspx)

虚拟按键包括Control、Shift、Alt、英文字母等。

【已验证】在 OllyDBG 插件回调函数中，可以将键盘事件发送到插件主窗口。

```
extc int _export cdecl ODBG_Pluginshortcut(
    int origin, int ctrl, int alt, int shift, int key, void *item) {

    ::PostMessage(hwtrace, WM_KEYDOWN, 0x45, MapVirtualKey(0x45, MAPVK_VK_TO_VSC));

    return 0;  // 0 表示快捷键未识别；返回 0 以便其它插件继续处理。                    
};
```

Windows 虚拟按键表：[https://msdn.microsoft.com/zh-cn/library/windows/desktop/dd375731\(v=vs.85\).aspx](https://msdn.microsoft.com/zh-cn/library/windows/desktop/dd375731%28v=vs.85%29.aspx)

Windows 系统消息列表：https://wiki.winehq.org/List\_Of\_Windows\_Messages

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



