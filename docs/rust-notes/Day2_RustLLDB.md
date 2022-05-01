# Rust Debug With LLDB
Rust 使用rust-lldb 进行调试，rust-lldb提供cli 和 terminal gui，还算是比较方便。 有兴趣的话也可以试着定制一下vsc，用vsc+lldb来debug应该会有更好的图形画交互体验。
## 安装
rust-lldb工具是在安装rust的时候自动安装的，但是lldb需要自行安装。OSX可以使用brew，ubuntu可以使用apt，直接装就行。
## 示例程序
本文将使用上一篇中的hello_world程序来简单记录一下lldb的命令使用。
## lldb REPL

```bash
$ rust-lldb taget/debug/hello_world
```

这个会用rust REPL加载hello_world。
> **_NOTES:_** 使用debug模式构建包，不然会丢失符号表。

## 指令

### 1. ``b`` 设置断点

例子：
```bash
breakpoint set -n <main> # 方法开始设置断点
breakpoint set -f <file> --line <number> # 行号断点
```
![set breakpoint](/images/breakpoint_set.png)

### 2. ``r`` 开始运行

![run executable](/images/lldb_run.png)

### 3. ``gui`` 进入图形界面

![run executable](/images/lldb_gui.png)

### 4. 单步调试
* ``s`` step-in 单步调试
* ``n`` step-over 单步，越过子函数

### 5. ``c`` 继续运行
继续运行到下一个断点

## 其他Debug方式

基本这些功能可以满足需要，但是gui毕竟是terminal gui，和代码的交互并不是那么的方便。

喜欢定制VSCode的话可以参考[How to debug rust with visual studio code](https://www.forrestthewoods.com/blog/how-to-debug-rust-with-visual-studio-code/)

其次，JetBrains也发布了他们IntelliJ Rust，可以体验所有IDEA全家桶里拥有的功能，而且IDEA全家桶也都支持联调Rust了，推荐体验。[IntelliJ Rust](https://intellij-rust.github.io)