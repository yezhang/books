## **react-native命令分析** {#react-native%E5%91%BD%E4%BB%A4%E5%88%86%E6%9E%90}

当在 npm script 中执行 react-native run-android 命令时，命令的解析过程如下：

**1. 分析入口**

进入 node\_modules/react-native 目录。 在该目录下具有入口脚本 cli.js。 cli.js 文件调用 cliEntry.js。 命令的解析和执行过程，都在 cliEntry.js 文件中。

**2. 可以支持的命令**

cliEntry.js 文件通过以下代码添加所有可以支持的命令。

```js
144 commands.forEach(cmd => addCommand(cmd, config));
```

commands 变量是从 cliEntry.js 同级目录下的 commands.js 文件引入的。

```js
25 const commands = require('./commands');
```

具体命令的添加过程在 addCommand 函数中。

```js
const addCommand = (command: CommandT, cfg: RNConfig) => {
const options = command.options || [];

const cmd = commander
.command(command.name, undefined, {
    noHelp: !command.description,
    }
)
.description(command.description)
.action(function runAction() {
    //......
});

//......
}
```

**3. 执行 run-android**打开 commands.js 文件，可以看到对于 runAndroid 文件的引用。

```js
41  require('./runAndroid/runAndroid'),
```

根据上述引用的目录，打开`./runAndroid/runAndroid.js`文件。 在文件的最后，查看`module.exports`，可以看到导出了一个自定义的对象。

接着，查看其中的 runAndroid 函数，该函数包含`react-native run-android`命令的执行过程。 在函数的最后，出现`buildAndRun`函数，该函数包含代码的构建和启动过程。 之后，经过几次跟踪，找到 installAndLaunchOnDevice 函数。 函数中使用如下代码启动 apk。

```js
192  tryLaunchAppOnDevice(selectedDevice, packageNameWithSuffix, packageName, adbPath, args.mainActivity);
```

可以看到，最后一个参数 args.mainActivity 指定了启动时的 Activity。 在 tryLaunchAppOnDevice 函数中，设置了 adb 的执行脚本，代码如下：

```js
const adbArgs = ['-s', device, 'shell', 'am', 'start', '-n', packageNameWithSuffix + '/' + packageName + '.' + mainActivity];
//......
child_process.spawnSync(adbPath, adbArgs, {stdio: 'inherit'});
```

如果希望修改启动时的 MainActivity，只需要在启动 runAndroid 时指定命令行参数即可。 即，传递`--main-activity [string]`。 最终的 npm 命令为`react-native run-android --main-activity project.MainActivity`。 如果希望恢复默认的指令，直接删除`--main-activity project.MainActivity`即可。

