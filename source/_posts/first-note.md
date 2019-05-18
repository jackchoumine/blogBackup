---
title: 使用hexo + github搭建个人主页
date: 2019-05-18 02:30:28
tags: hexo github
---

## 预备知识：

- npm 命令；
- git 命令
- github 常见操作

环境要求：
- node
- git

我的环境：
```bash
$ git version
git version 2.15.1.windows.2
$ node -v
v8.11.1
$ npm -v
6.4.0
```
## 安装 hexo
```bash
npm i -g hexo-cli 
```
在某个文件夹内初始化 hexo 博客所需要的文件
```bash
mkdir myBlog  # /e/HexoPages 新建一个文件夹
cd myBlog
npm i # 安装npm 依赖
```
得到如下目录：
```bash
├── _config.yml # 网站的配置信息，您可以在此配置大部分的参数。 
├── package.json
├── scaffolds # 模版文件夹
├── source  # 资源文件夹，除 _posts 文件，其他以下划线_开头的文件或者文件夹不会被编译打包到public文件夹
|   ├── _drafts # 草稿文件
|   └── _posts # 文章Markdowm文件 
└── themes  # 主题文件夹
```
本地预览博客：
```bash
hexo s
```
打开`http://localhost:4000`即可看到效果。

![hexo默认主题](https://github.com/JackZhouMine/jack-picture/blob/master/hexo%E9%BB%98%E8%AE%A4%E4%B8%BB%E9%A2%98.png "hexo默认主题")

## 创建托管博客的仓库

仓库名字必须用`用户名.github.io`，需要公开。

## 部署本地博客到 gitbub

1. 修改`_config.yml`

打开 _config.yml ，将 deploy 修改如下**注意空格**
```bash
deploy:
  type: git # 版本管理工具
  repo: # 仓库信息
    github: https://github.com/JackZhouMine/jackzhoumine.github.io
  branch: master # 使用分支
```
其他配置也可以修改，比如我将站点信息修改如下：
```bash
# Site
title: 周其军的个人博客
subtitle:
description:
keywords:
author: 周其军
language:
timezone:
```
2. 安装 hexo-deployer-git

```bash
npm i -S hexo-deployer-git
```
3. 部署
```bash
hexo g -d
```
打开我的主页链接 `https://jackzhoumine.github.io`，看到页面就部署成功了。

![部署成功](https://github.com/JackZhouMine/jack-picture/blob/master/myblog.png "部署成功的页面")

## 创建文章

1. 创建文章

执行`hexo new '文章标题'`，会在source/_posts文件夹内新建一个md文件，就可在里面写文章了，当然也可以手动创建。
```bash
$ hexo new  first-note
INFO  Created: E:\HexoPages\myBlog\source\_posts\first-note.md
```

2. 预览效果

创建完成，执行以下命令,在本地预览效果：
```bash
hexo g
hexo s
```
3. 部署到线上

```bash
hexo clean # 清除缓存文件（db.json）和静态文件。更改后不生效，就需要运行该命令。
hexo g -d # 部署到线上
```
4. 创建草稿

可先创建草稿，想发布时，在发布。
```bash
hexo new draft "文章标题" # 会在 /source/-drafts 里生成草稿
hexo publish filename
```
