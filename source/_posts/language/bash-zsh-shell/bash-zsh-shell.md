---
title: shell 以及他的命令行环境
date: 2020-09-01 17:46:29
tags: 计算机通识 
categories: language
---
苹果Macos 从Catalina版本开始使用zsh作为默认的登录shell 和 交互shell。之前默认的是bash,这个转变是什么意思呢？这要从shell开始说起。
## shell
学习 Bash，首先需要理解 Shell 是什么。Shell 这个单词的原意是“外壳”，跟 kernel（内核）相对应，比喻内核外面的一层，即用户跟内核交互的对话界面。
具体来说，Shell 这个词有多种含义。
首先，Shell 是一个程序，提供一个与用户对话的环境。这个环境只有一个命令提示符，让用户从键盘输入命令，所以又称为命令行环境（commandline，简写为 CLI）。Shell 接收到用户输入的命令，将命令送入操作系统执行，并将结果返回给用户。本书中，除非特别指明，Shell 指的就是命令行环境。
其次，Shell 是一个命令解释器，解释用户输入的命令。它支持变量、条件判断、循环操作等语法，所以用户可以用 Shell 命令写出各种小程序，又称为脚本（script）。这些脚本都通过 Shell 的解释执行，而不通过编译。
最后，Shell 是一个工具箱，提供了各种小工具，供用户方便地使用操作系统的功能。
<!-- more -->

##  bash
Bash 是 Unix 系统和 Linux 系统的一种 Shell（命令行环境），是目前绝大多数 Linux 发行版的默认 Shell。Mac 从Catalina版本开始默认采用zsh。
Zsh??

shell的种类很多，只要能给用户提供命令行环境的程序，都可以看作是Shell。常见的shell有
* Bourne Shell（sh）
* Bourne Again shell（bash）
* C Shell（csh）
* TENEX C Shell（tcsh）
* Korn shell（ksh）
* Z Shell（zsh）
* Friendly Interactive Shell（fish）
查看当前运行的Shell
$ echo $SHELL 

## bash 和 zsh的不同
- zsh性能更好
- 配置文件不同  bash  `.bashrc`   和 zsh的`.zshrc`
- zsh有更强的定制能力


## .bash_profile 和 .bashrc
通过这两个文件可以个性化定制你的shell环境。
`.bash_profile` and `.bashrc` are files containing shell commands that are run when Bash is invoked. `.bash_profile` is read and executed on interactive login shells, while `.bashrc` on non-login shells.

### Interactive Login and Non-Login Shell
当启动bash时，bash会从一组启动文件中读取和执行命令。具体去读哪些文件取决于shell是交互式登录shell还是非登录shell。shell可以是交互式或者内交互式的。
简而言之，交互式Shell是一个读写用户终端的Shell，就是有用户输入有屏幕输出，而非交互式Shell是一个与终端交互的Shell，例如执行脚本时。交互式Shell程序可以是登录Shell，也可以是非登录Shell。

当用户通过ssh远程登录到终端或在本地登录终端时，或者使用--login选项启动Bash时，都会调用登录Shell。从登录Shell调用交互式非登录Shell，例如在Shell提示符下键入bash或打开新的Gnome终端选项卡时。

### Bash启动文件
当作为交互式登录shell调用时，Bash查找/etc/profile文件，如果该文件存在，它将运行文件中列出的命令。然后Bash按照列出的顺序搜索〜/.bash_profile，〜/.bash_login和〜/.profile文件，并从找到的第一个可读文件中执行命令。

当Bash作为交互式非登录外壳程序被调用时，它从〜/.bashrc读取并执行命令（如果该文件存在并且可读）。
 
## shell 和 bash的历史
Shell 伴随着 Unix 系统的诞生而诞生。
1969年，Ken Thompson 和 Dennis Ritchie 开发了第一版的 Unix。
1971年，Ken Thompson 编写了最初的 Shell，称为 Thompson shell，程序名是sh，方便用户使用 Unix。
1973年至1975年间，John R. Mashey 扩展了最初的 Thompson shell，添加了编程功能，使得 Shell 成为一种编程语言。这个版本的 Shell 称为 Mashey shell。
1976年，Stephen Bourne 结合 Mashey shell 的功能，重写一个新的 Shell，称为 Bourne shell。
1978年，加州大学伯克利分校的 Bill Joy 开发了 C shell，为 Shell 提供 C 语言的语法，程序名是csh。它是第一个真正替代sh的 UNIX shell，被合并到 Berkeley UNIX 的 2BSD 版本中。
1979年，UNIX 第七版发布，内置了 Bourne Shell，导致它成为 Unix 的默认 Shell。注意，Thompson shell、Mashey shell 和 Bourne shell 都是贝尔实验室的产品，程序名都是sh。对于用户来说，它们是同一个东西，只是底层代码不同而已。
1983年，David Korn 开发了Korn shell，程序名是ksh。
1985年，Richard Stallman 成立了自由软件基金会（FSF），由于 Shell 的版权属于贝尔公司，所以他决定写一个自由版权的、使用 GNU 许可证的 Shell 程序，避免 Unix 的版权争议。
1988年，自由软件基金会的第一个付薪程序员 Brian Fox 写了一个 Shell，功能基本上是 Bourne shell 的克隆，叫做 Bourne-Again SHell，简称 Bash，程序名为bash，任何人都可以免费使用。后来，它逐渐成为 Linux 系统的标准 Shell。
1989年，Bash 发布1.0版。
1996年，Bash 发布2.0版。
2004年，Bash 发布3.0版。
2009年，Bash 发布4.0版。
2019年，Bash 发布5.0版。
用户可以通过bash命令的--version参数或者环境变量$BASH_VERSION，查看本机的 Bash 版本。


## Reference
[.bashrc vs .bash_profile](https://linuxize.com/post/bashrc-vs-bash-profile/)