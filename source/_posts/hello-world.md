---
title: 通过hexo搭建个人博客
tags: hexo
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

1. 在域名

2. 在`/source`下添加名为`CNAME`的文件，无后缀。将你自己的域名放入文件内

```bash
    www.<yoursite>.name
```

## 添加https