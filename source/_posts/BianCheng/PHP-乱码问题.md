---
title: PHP开发中一些乱码问题
date: 2017-04-10
tags: 
- PHP
- Utf8
categories:
- PHP
---

PHP乱码的一些问题



有时候，在PHP开发中会出现乱码，一般是由于文件、数据库、浏览器等各处编码格式不同造成的。 

所以，请在所有涉及到编码格式的地方，统一使用 `UTF-8`.

## 将所有文件保存为 UTF8 格式

请将 PHP 文件格式保存为 UTF8。
请将 HTML、CSS、JavaScript等文件也要保存成UTF8格式。

Window环境可以使用 `Notepad++` 打开文件，选择[格式(M)] > [转为UTF8无BOM编码格式]，然后保存即可.

PHP与MySQL的数据库的交互时，一定要保证双方的编码一致。


## 在HTML页面中声明 UTF8 编码：

在页面< head >< /head >里面增加meta信息：

```
<meta charset="UTF-8">
<meta http-equiv="Content-Type" content="text/html;charset=UTF-8">
```


## 在PHP文件中使用 UTF8 编码：

* 在输出HTML模板时，指定UTF8编码: 

```
header("Content-Type:text/html; charset=utf-8");
```

* 数据库连接时使用 UTF8 编码:

创建数据库的时候，MySQL字符集选择'UTF8'，MySQL连接校对选择utf8_general_ci

```
$mysqli->query("SET character set 'utf8'");//读库 
$mysqli->query("SET NAMES 'utf8'");//写库 
```

* 使用多字节处理函数

所有的字符串处理函数尽量换成多字节处理函数。  
即把 substr 之类的函数改成 mb_substr，这可能需要安装mbstring扩展。

参见PHP文档：http://php.net/manual/zh/ref.mbstring.php


## PHP 生成 CSV 文件增加BOM头: 

在使用 PHP 生成 CSV 文件时，增加BOM头， 保证在Windows下打开不乱码, 代码如下:

```
//生成bom头
fputs($fp, $bom =( chr(0xEF) . chr(0xBB) . chr(0xBF) ));
```

一个生成并下载CSV文件的函数示例:

```
/**
 * @param array $csvTitle 标题
 * @param array $csvArray 数据
 * @param string $fileName 文件名
 */
protected function downloadAsCsvFile(array &$csvTitle, array &$csvArray, $fileName='') {
    if (empty($fileName)) {
      $fileName = 'download_'.date('Ymd_His');
    }
    header('Content-type: application/csv');
    header('Content-Transfer-Encoding: binary; charset=utf-8');
    header('Content-Disposition: attachment; filename='.$fileName.'.csv');
    $fp = fopen("php://output", 'w');
    //生成bom头
    fputs($fp, $bom =( chr(0xEF) . chr(0xBB) . chr(0xBF) ));
    //生成标题栏
    fputcsv($fp, $csvTitle);
    foreach ($csvArray as $row) {
        fputcsv($fp, $row);
    }
    exit;
}
```

## 查看文件格式: 

在Vim中可以直接查看文件编码

```
// 查看文件编码
:set fileencoding

// 将文件转换成utf-8格式
:set fileencoding=utf-8
```

在Unix/Linux下，可以使用 file 命令查看文件是否包含BOM头：

* file - 该命令用来识别文件类型，也可用来辨别一些文件的编码格式。

```
$ file public/index.php
public/index.php: PHP script text

$ file wangtest.csv
wangtest.csv: UTF-8 Unicode (with BOM) text
```

## 问题1：在Linux下执行PHP文件时错误：Could not open input file

解决：  
如果出现这个，可能就是文件格式的问题：
使用Vim命令：在Linux上查看文档格式 

```
$ vi test.php  
:set ff //查看文件格式
    fileformat=dos  //显示为doc
:set ff=unix //设置格式为unix  
:set ff //再次查看 
    fileformat=unix //已经转换为unix格式了
```

变成了unix格式的，重试执行PHP文件，正常。

在Windows下，使用Notepad++编辑器也可以改变格式：

```
[编辑(E)] > [档案格式转换] > [转换为UNINX格式]
```

## PHP中有关编码的函数

* iconv — 字符串按要求的字符编码来转换

 格式：string iconv ( string $in_charset , string $out_charset , string $str )
 说明：将字符串 str 从 in_charset 转换编码到 out_charset。 

* urlencode — 编码 URL 字符串

 格式：string urlencode ( string $str )
 说明：此函数便于将字符串编码并将其用于 URL 的请求部分，同时它还便于将变量传递给下一页。 

* urldecode — 解码已编码的 URL 字符串

 格式：string urldecode ( string $str )
 说明：解码给出的已编码字符串中的任何 %##。 加号（'+'）被解码成一个空格字符。

* rawurlencode() - 按照 RFC 1738 对 URL 进行编码

* rawurldecode() - 对已编码的 URL 字符串进行解码

* json_encode — 对变量进行 JSON 编码

* json_decode — 对 JSON 格式的字符串进行编码

* serialize — 产生一个可存储的值的表示 

* unserialize — 从已存储的表示中创建 PHP 的值

* session_encode — 将当前会话数据编码为一个字符串

* session_decode() - Decodes session data from a session encoded string

### 更新记录

1. 20161216 新增此文档 (wangyt)
2. 20170411 更新文档，完善内容，调整格式 (wangyt)

[END]
