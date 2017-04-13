---
title: PHP-如何不使用临时变量来交换两个数值变量？
date: 2012-06-01
tags: 
- PHP
categories:
- PHP
---

PHP-如何不使用临时变量来交换两个数值变量？

在PHP面试题目中，关于变量交换的出现了很多次，现在总结一下！
 
[题目] 如何在PHP中不使用临时变量来交换两个数值变量？

[解析]

正常是交换两个变量的值应该使用中间变量：

```
function swap($a, $b){
   $temp = $a;
   $a = $b;
   $b = $temp;
}
```
 
1.这个方法很容易想到，但是只限于交换数值类型的变量：

```
function swap (&$a,&$b){
    $a = $a+$b;
    $b = $a-$b;
    $a = $a-$b;
}
```

2.这方法是语言结构,想法很奇妙：

```
    list($a, $b) = array($b, $a);
```

 注：list — 把数组中的值赋给一些变量

3.通过数组函数 array_reverse

```
    $arr=array($a,$b);
    $arr=array_reverse($arr);
    $a=$arr[0];
    $b=$arr[1];
```

  注：array_reverse — 返回一个单元顺序相反的数组
 
4.直接使用数组操作：

```
 $a = "aaa";
 $b = "bbb";
 $b = array($a, $b);
 $a = $b[1];
 $b = $b[0];
```

## 更新记录

* 2012-06-01 新增此文档 (wangyt)  
* 2017-04-12 重新整理本文档 (wangyt)

[END]