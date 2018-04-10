# 在 ReactNative 中使用原生导航

iOS

核心在于：在多个 RCTRootView 中共享 RCTBridge。

当从 RN 界面中的一个页面，导航到另一个页面时，在不同页面之间共享一个 jsBundle 数据。

样例代码：

Sections/HomePage/controller/PYJHomePageViewController.m

查看其中的 viewDidLoad 函数。首页和票夹页面，使用了独立的 viewDidLoad，其他页面直接使用 ReactRootView 类。



Android

核心在于：在多个 ReactRootView 对象中共享 ReactInstanceManager。

