# 使用 JaCoCo 测试 Java 生产代码的覆盖度

场景描述：在多团队合作开发中，有时无法获取其他团队提供的 jar 文件源代码，此时如果希望对 jar 进行单元测试并生产代码覆盖度报告，现有工具都不能直接提供。本文整理了一个方法，用于解决该问题。

本文整理的方案可用于：单元测试、发现生产环境中不用的遗留代码。

优点：便于调试，查看覆盖度。


## 方案描述

使用 JaCoCo 的离线模式，提前注入相关测试代码。同时将 jacocoagent.jar 放入 classpath 中。

1、进入 jacoco 目录（包含 jacococli.jar），使用控制台命令手动注入代码：

```js
java -jar jacococli.jar instrument ../../src/main/libs/formulaPUB.jar --dest ../../src/main/libs/formulaPUB.instr.jar
```

2、在 IDEA 中运行 JUnit 4 单元测试。运行后，在项目目录下生产 jacoco.exec 文件。

3、在控制台中输入一下命令，生成覆盖度报告：

```js
java -jar jacococli.jar report ../../jacoco.exec --classfiles ../../src/main/libs/formulaPUB.jar --html ../../coverage-report
```

注意，上面的 classfiles 指的是未处理的原始 jar 文件。

如果需要在报告中显示源代码的位置，可以使用 --sourcefiles 参数指定。例如，假设源码目录是 /Users/zhangye/Documents/code/yes_yonyou/FormulaUtilTest/src/main/java。那么使用如下命令：

```js
java -jar jacococli.jar report ../../jacoco.exec --classfiles ../../src/main/libs/formulaPUB.jar --html ../../coverage-report --sourcefiles /Users/zhangye/Documents/code/yes_yonyou/FormulaUtilTest/src/main/java
```

4、在项目的 coverage-report 目录下，打开 index.html 文件即可查看代码覆盖度报告。

最终效果是：使用 IDEA，不使用 Maven，执行 JUnit4，在 IDEA 中查看代码覆盖度报告。

```
如果使用了本文介绍的手工注入方法，那么在 IDEA 中执行测试时，则不能使用 Run XXX with Coverage 选项了。因为使用该选项可能会导致重复注入，因而出错。
```

## JaCoCo 代码覆盖度报告解释


## 参考资料

jacoco 控制台参数说明：https://www.jacoco.org/jacoco/trunk/doc/cli.html

1、https://carlosbecker.com/posts/production-code-coverage-jacoco/

2、手动注入 https://automationrhapsody.com/code-coverage-with-jacoco-offline-instrumentation-with-maven/