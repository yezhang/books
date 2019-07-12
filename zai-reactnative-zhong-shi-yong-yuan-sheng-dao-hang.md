# 在 ReactNative 中使用原生导航

### iOS

核心在于：在多个 RCTRootView 中共享 RCTBridge。

当从 RN 界面中的一个页面，导航到另一个页面时，在不同页面之间共享一个 jsBundle 数据。

样例代码：

Sections/HomePage/controller/PYJHomePageViewController.m

查看其中的 viewDidLoad 函数。首页和票夹页面，使用了独立的 viewDidLoad，其他页面直接使用 ReactRootView 类。

在代码中使用 RCTRootView 的 initialProperties 参数传递启动参数。

RCTRootView\* rootView = \[\[RCTRootView alloc\] initWithBridge:bridge moduleName:@"piaoyouji" **initialProperties**:self.props\];

启动参数设置方式为：

```

```

#### iOS push 方法

原生模块

```objectc
RCT_EXPORT_METHOD(push: (NSString *) screenName
                  coordinator:(NSString *) identifier
                  title:(NSString *) title
                  props: (NSDictionary *) props) {
  RCTLog(@"导航到 %@", screenName);

  dispatch_async(dispatch_get_main_queue(), ^{

    NSDictionary *dic = props ?: @{};
    NSDictionary *info = @{
                           @"initialScreen" : screenName,
                           @"navigator" : title ?: @"",
                           @"coordinator" : identifier,
                           @"screenProps" : dic
                           };
    [[NSNotificationCenter defaultCenter] postNotificationName:@"NAVIGATOR_PUSH" object:nil userInfo:info];
  });
}
```

#### iOS pop 方法

### Android

核心在于：在多个 ReactRootView 对象中共享 ReactInstanceManager。

样例代码：

com.yonyou.einvoice.modules.react.MainReactActivityDelegate.java

其中的 getLaunchOptions 函数，设置了程序的启动参数。启动参数包括如下内容：

```java
props.putString("coordinator", coordinatorName);
props.putString("navigator", title);
props.putString("initialScreen", screenName);
props.putBundle("screenProps", screenProps);
```

在 ReactActivityDelegate.java 内部，会通过调用 ReactRootView.startReactApplication 方法设置启动参数。

或者

com.yonyou.einvoice.modules.react.ReactNativeFragment.java

其中的 mReactRootView.startReactApplication 方法，设置启动参数。

项目代码中，com.yonyou.einvoice.modules.react.ReactNativeFragment 与 react Native 库中的类 com.facebook.react.ReactActivityDelegate 有相似代码。

React

在 App.js 的入口文件中，使用应用程序的 props，获取启动参数。获取方式如下。

```js
render() {
  const initScreen = this.props.initialScreen || 'Home';
  const screenProps = this.props.screenProps || {};
  let { coordinator, title } = this.props;

  const Route = Routes[initScreen];

  return (
    <Provider {...store}>
      <View style={ios ? styles.iosContainer : styles.container}>
        <Route.screen {...this.props} coordinator={coordinator} title={title} />
      </View>
    </Provider>
  );
}
```

根据启动参数不同，调用不同路由界面。

