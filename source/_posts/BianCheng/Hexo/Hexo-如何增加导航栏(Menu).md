---
title: Hexo-如何增加导航栏(Menu)
date: 2017-04-12
tags: Hexo
categories:
- Hexo
---


本文要讲述如何如何增加导航栏(Menu)。


<!-- more -->


## 第一种方法，使用【数据文件】实现

有时您可能需要在主题中使用某些资料，而这些资料并不在文章内，并且是需要重复使用的，那么您可以考虑使用 Hexo 3.0 新增的「数据文件」功能。
此功能会载入 source/_data 内的 YAML 或 JSON 文件，如此一来您便能在网站中复用这些文件了。

举例来说，在 source/_data 文件夹中新建 menu.yml 文件：

```yaml
Home: /
Gallery: /gallery/
Archives: /archives/
```

您就能在模板中使用这些资料：

```html
<% for (var link in site.data.menu) { %>
  <a href="<%= site.data.menu[link] %>"> <%= link %> </a>
<% } %>
```

渲染结果如下 :

```html
<a href="/"> Home </a>
<a href="/gallery/"> Gallery </a>
<a href="/archives/"> Archives </a>
```

详见Hexo 官方文档中有【数据文件】章节


## 第二种方法, 使用主题中的配置

比如，使用默认主题 landscape ，在 theme/landscape/_config.yml 中有如下 Menu 配置:

```
# Header
menu:
  Home: /
  Archives: /archives
```

我们可以打开 `theme/landscape/layout/_partial/header.ejs` 文件, 查看其实现:  

```html
  <nav id="main-nav">
    <a id="main-nav-toggle" class="nav-icon"></a>
    <% for (var i in theme.menu){ %>
      <a class="main-nav-link" href="<%- url_for(theme.menu[i]) %>"><%= i %></a>
    <% } %>
  </nav>
```

跟第一种方法类似，只是使用的变量不同。

## 第三种方法, 使用HTML实现 

这个最简单，当然是直接在模板文件中写 HTML 代码了~
这个肯定是不推荐使用。


我们可以修改以增加菜单导航内容。

## 开发环境

```
$ hexo --version
hexo: 3.3.1
hexo-cli: 1.0.2
os: Darwin 15.6.0 darwin x64
http_parser: 2.7.0
node: 7.8.0
v8: 5.5.372.43
uv: 1.11.0
zlib: 1.2.11
ares: 1.10.1-DEV
modules: 51
openssl: 1.0.2k
icu: 58.2
unicode: 9.0
cldr: 30.0.3
tz: 2016j
```

## 参考链接   

https://hexo.io/zh-cn/docs/data-files.html


## 更新记录

 
[END]