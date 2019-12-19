# Chrome DevTools 定制化

### 定制化步骤

1、准备代码

2、初步编译

3、修改代码、编译、调试

Chrome DevTools 的编译，依赖于 Chrome 源码。所以，首先需要将完整的 Chrome 代码下载到本地，并配置编译参数。

### 准备代码

Chrome 源码可以从两个位置获取，一是谷歌官方托管地址，二是 github 镜像。

1、从官方地址获取源码的方法为：[https://www.chromium.org/developers/how-tos/get-the-code](https://www.chromium.org/developers/how-tos/get-the-code)

2、从 github 镜像获取源码的地址为：[https://github.com/chromium/chromium](https://github.com/chromium/chromium)

MacOS 获取 Chrome 源码的官方说明：[https://chromium.googlesource.com/chromium/src/+/master/docs/mac\_build\_instructions.md\#Get-the-code](https://chromium.googlesource.com/chromium/src/+/master/docs/mac_build_instructions.md#Get-the-code)

不克隆历史，使用如下脚本：

```
gclient sync --no-history
```

如果克隆所有历史，那么下载时间会很长。

若在下载过程中出现了错误，重复执行上述命令即可。为了加快下载速度，推荐使用网络代理。

下载过程分为三个步骤：下载主项目代码、下载依赖项、下载构建工具。这三个步骤在可以自动依次执行。当下载中断时，重复执行 gclient sync --no-history 命令即可恢复该流程。

如果在执行 hooks 阶段出现错误，可以通过如下脚本继续执行。

```
env GYP_DEFINES=disable_nacl=1 gclient runhooks
```

当代码下载完成后，Chrome DevTools 工具的代码已经包含在 src 文件夹中。具体位置是：

```
src/third_party/blink/renderer/devtools/front_end
```

另外，在 github 上可以直接查看 Chrome DevTools 源码：

[https://github.com/ChromeDevTools/devtools-frontend](https://github.com/ChromeDevTools/devtools-frontend)

github 上的 DevTools 源码文件结构与 src 目录下的源码结构相同。

### 初步编译

进入 src 目录。

```
cd src
```

在 src 目录执行 gn 命令。

```
gn gen out/Default
```

在编译前，需要调整编译参数。

进入 out/Default 目录。如果 out/Default 目录下没有 args.gn 文件，则需要在 src 目录执行以下命令生成构建参数文件。

```
gn args out/Default
```

为了编译 Chrome DevTools 工具，推荐使用如下构建参数。

    # args.gn 文件, https://gist.github.com/paulirish/2d84a6db1b41b4020685#file-args-gn

    cc_wrapper="ccache"

    # Build arguments for the gn build
    # You can set these with `gn args out/Default`
    #   ( and they're stored in src/out/Default/args.gn )
    # See "gn args out/Default --list" for available build arguments

    # component build, because people love it
    is_component_build = true

    # release build, because its faster
    is_debug = false

    # hardlink'ed devtools frontend. oh yes
    debug_devtools = true

    # no thx
    enable_nacl = false

    # This is default for Release builds, but forced regardless
    dcheck_always_on = false

    # goma only if you're a googler
    use_goma = false

为了加快构建速度，还可以配置好 ccache。

### 修改源码、编译、调试

将 chromium.sh 文件拷贝到 src 父目录\(chromium/\)中。

```
source chromium.sh
```

    # chromium.sh

    # usage:
    # after `git pull`, a full build is now `depsbcr`
    # and after changes.. a `bcr` will recompile and relaunch chrome.
    function deps() {
            env GYP_DEFINES=disable_nacl=1 gclient sync
    }
    function hooks() {
            env GYP_DEFINES=disable_nacl=1 gclient runhooks
    }
    function b() {
            local dir=$(git rev-parse --show-toplevel)/out/xcode
            # autoninja will automatically determine your -j number based on CPU cores
            local cmd="autoninja -C \"$dir\" chrome"
            echo "  > $cmd"
            eval "$cmd"
            if [ $? -eq 0 ]; then
                    printf "\n✅ Chrome build complete!\n"
            fi
    }
    # you can also add any extra args: `cr --user-data-dir=/tmp/lol123"
    function cr() {
            local dir=$(git rev-parse --show-toplevel)/out/xcode
            local cmd="./$dir/Chromium.app/Contents/MacOS/Chromium $argv"
            echo "  > $cmd"
            eval "$cmd"
    }
    function gom() {
            # these probably dont make sense for everyone.
            export GOMAMAILTO=/dev/null
            export GOMA_OAUTH2_CONFIG_FILE=$HOME/.goma_oauth2_config
            export GOMA_ENABLE_REMOTE_LINK=yes
            ~/goma/goma_ctl.py ensure_start
    }
    function bcr() {
            if b; then
                    cr
            fi
    }
    function depsb() {
            if deps; then
                    gom
                    b
            fi
    }
    function depsbcr() {
            if deps; then
                    gom
                    bcr
            fi
    }
    function hooksbcr() {
            if hooks; then
                    gom
                    bcr
            fi
    }

进入 src 目录。执行上述脚本的命令，启动第一次编译。

```
bcr
```

由于我们在编译时设置了 \`debug\_devtools\` 编译选项，所以现在可以直接使用 **third\_party/blink/renderer/devtools/front\_end **中的源代码作为 DevTools 的源码了。当修改该目录下的源码后，直接刷新 DevTools 工具（Alt + R）即可更新最新的变动。

Chrome DevTools 的前端页面结构是：

修改 DevTools 源码后，如何重新编译更新？

下载源码的方法：

\[ \] Getting sources: bullet-proof，[https://medium.com/@aslushnikov/hacking-chrome-devtools-8c8896f5cef3](https://medium.com/@aslushnikov/hacking-chrome-devtools-8c8896f5cef3)

参考资料

* [Chrome DevTools Contribution Guide](https://docs.google.com/document/d/1WNF-KqRSzPLUUfZqQG5AFeU_Ll8TfWYcJasa_XGf7ro/view#)
* 使用自定义 DevTools：[https://medium.com/@aslushnikov/hacking-chrome-devtools-8c8896f5cef3](https://medium.com/@aslushnikov/hacking-chrome-devtools-8c8896f5cef3)



