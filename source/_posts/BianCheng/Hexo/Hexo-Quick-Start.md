---
title: Hexo-快速入门指南
date: 2017-04-12
tags: 
- Hexo
categories:
- Hexo
---

# 什么是 Hexo？

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

Hexo出自台湾大学生 tommy351 之手，是一个基于 Node.js 的静态博客程序.


安装前提

安装 Hexo 相当简单。然而在安装前，您必须检查电脑中是否已安装下列应用程序：

Node.js
Git

如果您的电脑中已经安装上述必备程序，那么恭喜您！接下来只需要使用 npm 即可完成 Hexo 的安装。

$ npm install -g hexo-cli



$ hexo clean            

$ hexo generate 

$ hex server


重启hexo server: 

由于Nodejs服务器不支持热更新，需要使用 Ctrl+C 关闭服务器，再重启: 

```
$ hexo server
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
```


Git deployer plugin for Hexo.

Installation

```
$ npm install hexo-deployer-git --save
```

Options

You can configure this plugin in `_config.yml`.

```
# You can use this:
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
  message: [message]
  name: [git user]
  email: [git email]
  extend_dirs: [extend directory]
  ignore_hidden: false # default is true
```


 


[END]