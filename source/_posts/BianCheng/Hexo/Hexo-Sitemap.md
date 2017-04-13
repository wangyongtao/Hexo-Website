---
title: Hexo-Sitemap
date: 2017-04-12
tags: 
- Hexo
- Sitemap
categories:
- Hexo
---

hexo-generator-sitemap

Github: https://github.com/hexojs/hexo-generator-sitemap

Generate sitemap.

Install

```
$ npm install hexo-generator-sitemap --save
```

Example:

```
npm install hexo-generator-sitemap --save
hexo-site@0.0.0 /Users/WangTom/Code/Hexo/Hexo-Website
└── hexo-generator-sitemap@1.1.2
```
 
Options

You can configure this plugin in `_config.yml`.

```
sitemap:
    path: sitemap.xml
    template: ./sitemap_template.xml
```


path - Sitemap path. (Default: sitemap.xml)

template - Custom template path. This file will be used to generate sitemap.xml (See default template)


Excluding Posts

Add sitemap: false to the post's front matter.

## 参考链接：

https://github.com/hexojs/hexo-generator-sitemap 