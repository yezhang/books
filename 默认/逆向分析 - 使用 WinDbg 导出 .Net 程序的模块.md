## 逆向分析 - 使用 WinDbg 导出 .Net 程序的模块 {#activity-name}

**0x00 背景描述**

在对 .Net 程序做逆向分析过程中，有时候需要分析使用 System.Reflection.Assembly.Load 方法动态加载的第三方库，这些动态加载的 dll 在 WinDbg -&gt; Debug -&gt; Modules 中是无法查看的。此时，需要使用本文介绍的方法，查看并导出这些 dll。

  


**0x01 工具准备**

在开始之前，请在 Windows 系统中安装以下工具。为了方便演示，这里以 x86 环境为例，安装这些工具的 x86 版本。

1. WinDbg，https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/debugger-download-tools

2. sosex.dll 扩展，http://www.stevestechspot.com

3. psscor4.dll 扩展（psscor4 是 sos 扩展的超集），https://www.microsoft.com/en-us/download/details.aspx?id=21255  

  


**0.02 导出步骤**

!dumpdomain

!savemodule

