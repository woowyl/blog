---
title: 如何在命令行添加一条命令
date: 2020-09-02 17:31:46
tags: 计算机通识 
categories: language
---
在使用node的时候，经常会好奇，为什么在命令行输入了一个`npm install`这样的命令，会自动执行那么多操作? 电脑是如何识别`npm`的? 为什么可以识别`npm`却不能识别`ilovewyl`呢(其实注册了这个命令之后是可以执行的)？

如果想要让命令行知道你的命令，你需要完成两步操作
1. 通过安装将这个命令注册在bin文件夹内
2. 确保这个bin文件夹路径在/etc/paths中（可以通过``` echo $PATH```查看当前路径）  
<!-- more -->
第一步其实在安装软件的时候会自动完成，但是我们需要对`bin`目录有一个更加理性的认识，这样在出现一些问题的时候，我们才不会不知道如何下手。下面就对`bin`目录做一个简单的介绍。

`Bin`目录是众多`Linux`目录中的一个（文末有其他重要的目录），是存放可执行文件的目录，可分为用户可执行文件和系统可执行文件.

## 1. 用户可执行文件
包括 `/bin` 、`/usr/bin`、 `/usr/local/bin`
`/usr/bin`下面的都是系统预装的可执行程序，会随着系统升级而改变。
`/usr/local/bin`目录是用户放置自己的可执行程序的地方，不会被系统升级而覆盖同名文件。
###  /bin
`bin`为binary的简写，主要放置一些系统的必备执行档， `/bin`是系统的一些指令。比如
- cat 
- cp
- dd 
- launchctl
- test
- df
- pwd 
- link 
- unlink
- rm 
- echo
- ln 
- rmdir
- mkdir
- mv
- wait4path
- chmod
- ed
- ls
- expr 
- sleep
- hostname
- stty
- kill
- ps
- sync
- pax
- data
- shell相关
    - bash
    - sh
    - zsh
    - csh
    - dash
    - ksh
    - tchs

### /usr/bin
是你在后期安装的一些软件的运行脚本。主要放置一些应用软体工具的必备执行档，`usr` 指 `Unix System Resource`，而不是`User`，比如列举一下我们常见的
- git 
- sudo
- vim
- zip
- ssh
- c++
- php
- python
- pip
- ...

### /usr/local/bin
`/usr/local/bin` 用于普通用户可以运行的程序，`/usr/local`层次结构供系统管理员在本地安装软件时使用,不会被系统升级而覆盖同名文件。本地安装的软件必须放在`/usr/local`而不是`/usr`中，除非要安装它来替换或升级/usr中的软件。比如
- node
- npm
- pyhton3.8 ..

## 系统可执行文件
系统可执行文件：/sbin、/usr/sbin

### /sbin
 `/sbin`一般是指超级用户指令。（system binary）主要放置一些系统管理的必备程式例如
 
 - cfdisk
 - dump
 - shutdown
 - ifconfig
 - ping
 - reboot
 - md5
 - ...
### /usr/sbin
`/usr/sbin`   放置一些用户安装的系统管理的必备程式
- dhcpd
- httpd
- imap
- samba
- ...

## 简单归纳：
/bin目录（binary）是二进制执行文件目录，主要用于具体应用
/sbin目录（system binary）是系统管理员专用的二进制代码存放目录，主要用于系统管理

## 其他重要的目录
- 主目录：/root、/home/username
- 用户可执行文件：/bin、/usr/bin、/usr/local/bin
- 系统可执行文件：/sbin、/usr/sbin、/usr/local/sbin
- 其他挂载点：/media、/mnt
- 配置：/etc
   - paths就保存在这里通过 `echo $PATH`命令可以看到path配置
- 临时文件：/tmp
- 内核和Bootloader：/boot
- 服务器数据：/var、/srv
- 系统信息：/proc、/sys
- 共享库：/lib、/usr/lib、/usr/local/lib

## Reference
[Linux 基础知识 /bin,/sbin,/usr/sbin,/usr/bin 目录 区别详解](https://blog.51cto.com/14551658/2440488)