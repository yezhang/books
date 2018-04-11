# 在 ReactNative 中使用原生导航

### iOS

核心在于：在多个 RCTRootView 中共享 RCTBridge。

当从 RN 界面中的一个页面，导航到另一个页面时，在不同页面之间共享一个 jsBundle 数据。

样例代码：

Sections/HomePage/controller/PYJHomePageViewController.m

查看其中的 viewDidLoad 函数。首页和票夹页面，使用了独立的 viewDidLoad，其他页面直接使用 ReactRootView 类。

在代码中使用 RCTRootView 的 initialProperties 参数传递启动参数。

RCTRootView\* rootView = \[\[RCTRootView alloc\] initWithBridge:bridge moduleName:@"piaoyouji" **initialProperties**:self.props\];

### Android

核心在于：在多个 ReactRootView 对象中共享 ReactInstanceManager。

样例代码：

.com.yonyou.einvoice.modules.react.MainReactActivityDelegate.java

其中的 getLaunchOptions 函数，设置了程序的启动参数。

