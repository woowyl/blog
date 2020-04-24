---
title: 通过hexo搭建个人博客
tags: hexo
date: 2016-09-21 10:00:05
categories: front-end
---

## 新建一个hexo博客

### 安装hexo

```bash
$ npm install -g hexo
```

### 初始化

```bash
$ cd yourblogfold
$ hexo init

```
<!-- more -->
## 常用命令

### 生成一个新文章

``` bash

// [layout] 为布局，可选项为 `post`、`page`、`draft`，这将决定文章所在文件路径。
// <title> 为文章标题

$ hexo new [] "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### 启动服务器

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### 生成静态文件

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### 部署

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)


## 配合github page

1. 在github新建一个仓库，仓库名必须为`<user-name>.github.io`。`user-name`是github的昵称。

2. 修改 _config.yml 配置

```bash
    # Deployment
    ## Docs: https://hexo.io/docs/deployment.html
    deploy:
        type: git
        repo: <你的仓库地址> # https://github.com/<user-name>/<user-name>.github.io
        branch: master
```

3. 部署代码

``` bash
$ hexo deploy
```

4. 查看效果

## 更换主题

```bash
# 下载到themes文件夹下
$ git clone https://github.com/KevinOfNeu/hexo-theme-yourtheme yourtheme

# 修改 _config.yml 配置
$ theme: yourtheme

```

## 绑定自己的域名

1. 修改GitHub Pages中的Custom domain选择

  > Setting=>  GitHub Pages => Custom domain

2. 在`/source`下添加名为`CNAME`的文件，无后缀。将你自己的域名放入文件内

```bash
    www.<yoursite>.name
```

3. 添加域名解析

在你的域名管理后台（eg:万网），修改你的域名解析记录。  
添加两个A记录，用得到的IP，一个主机记录为：“www”，一个为“@”，这样通过[yoursitename].com和www.[yoursitename].com都能访问到你的博客了。

详见(github官方配置文档)[https://help.github.com/en/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site]

## 添加https

自 2018 年 5 月 1 日，Github 支持自定义域名的 HTTPS 请求了。

配置也相当简单：

1. 更新 DNS 配置里的 A 记录，将其指向以下4个 IP 地址中的至少一个。

    - 185.199.108.153
    - 185.199.109.153
    - 185.199.110.153
    - 185.199.111.153

2. GiHub Pages仓库的设置里勾选 'Enforce HTTPS'。
  
  > Setting=>  GitHub Pages => Custom domain

## 添加评论

  可以使用gitalk插件，[传送门](https://github.com/gitalk/gitalk)。具体配置就不写在这里了。  
  推荐已经集成好的主题，[concise](https://github.com/sanonz/hexo-theme-concise)

## 最佳实践

  - 路径名包括文章的文件名，最好不要用中文