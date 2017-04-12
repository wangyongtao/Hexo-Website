---
title: PHP去除字符串中的最后一个字符 
date: 2012-09-05
tags: 
- PHP
categories:
- PHP
---



```
<?php
//PHP去除字符串中的最后一个字符

$str="aaaa,bbb,ccc,ddd,eee,";

echo rtrim($str,','); //第一种方法 trim($str,$chsrlist)去除两边的

echo substr($str,0,strlen($str)-1); //第二种方法

echo substr($str,0,-1); //第三种方法

echo $str{strlen($str)-1} == ',' ? substr($str, 0, -1) : $str; //第四种方法

?>
```

我觉得使用rtrim()函数还是比较好的,推荐使用！

如去除右边的逗号：

```
$new_str = rtrim( trim($str), ',' );
```

去除多个字符：

```
$new_str = rtrim( trim($str),',.;' );
```

拓展阅读：

代码中用到的函数：

rtrim — 删除字符串末端的空白字符（或者其他字符）
string rtrim ( string $str [, string $charlist ] )
该函数删除 str 末端的空白字符并返回。
string rtrim ( string $str [, string $charlist ] )
通过指定 charlist，可以指定想要删除的字符列表。简单地列出你想要删除的全部字符。使用 .. 格式，可以指定一个范围。

substr — 返回字符串的子串
string substr ( string $string , int $start [, int $length ] )
返回字符串 string 由 start 和 length 参数指定的子字符串。

strlen — 获取字符串长度
int strlen ( string $string )
返回给定的字符串 string 的长度。

[END]
