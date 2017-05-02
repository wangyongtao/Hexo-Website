---
title: Hexo-在文章后边增加版权信息尾巴
date: 2017-04-10 09:41:14
tags: 
- Hexo
categories:
- Hexo
---


```
hexo.extend.filter.register('before_post_render', function(data){
    return data;
});
```

AddTail.js

```
// Filename: AddTail.js
// Author: Colin
// Date: 2016/06/02
// Based on the script by KUANG Qi: http://kuangqi.me/tricks/append-a-copyright-info-after-every-post/

var fs = require('fs');

hexo.extend.filter.register('before_post_render', function(data){
    if(data.copyright == false) return data;
    
    // Add seperate line
    data.content += '\n___\n';
    
    // Try to read tail.md
    try {
        var file_content = fs.readFileSync('post-tail.md');
        if(file_content && data.content.length > 50) {
            data.content += file_content;
        }
    } catch (err) {
        if (err.code !== 'ENOENT'){
            throw err;
        } 
        // No process for ENOENT error
    }

    // 添加具体文章链接 
    var permalink = '\n 本文链接：' + data.permalink+'\n ';
    data.content += permalink;

    return data;
});
```

post-tail.md

```
欢迎转载，转载请注明来源于本站，并保持转载后文章内容的完整性。
```

``
$ hero clean

$ hexo generate

$ hexo server
```

[END]
