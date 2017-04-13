---
title: PHP-使用CURL抓取网站或调用接口
date: 2013-09-06
tags: 
- PHP
categories:
- PHP
---

[PHP]使用CURL抓取网站或调用接口 

cURL 是一个利用URL语法规定来传输文件和数据的工具，基于libcurl库，是跨平台的，几乎可以所有现存操作系统上使用，功能强大。而其libcurl库也支持几乎所有编程语言，当然也包括本文介绍的PHP语音。
 
cURL是瑞典CURL组织开发的，您可以访问: http://curl.haxx. se/ 获取它的源代码和相关说明,最新版本是7.32.0。
 
PHP支持的由Daniel Stenberg创建的libcurl库允许你与各种的服务器使用各种类型的协议进行连接和通讯。libcurl目前支持http、https、ftp、gopher、telnet、dict、file和ldap协议。libcurl同时也支持HTTPS认证、HTTP POST、HTTP PUT、 FTP 上传(这个也能通过PHP的FTP扩展完成)、HTTP 基于表单的上传、代理、cookies和用户名+密码的认证。这些函数在PHP 4.0.2中被引入。
 
使用cURL的步骤： 
1.    初始化 
2.    设置变量 
3.    执行并获取结果 
4.    释放cURL句柄
 
下面的实例是使用curl请求baidu然后输出请求到的结果，会完整的展现和baidu首页一样的内容，即实现了页面的抓取。
代码实例：

```
   $testurl = ‘www.baidu.com’;  // test url
   $ch = curl_init();  // create curl resource       
   curl_setopt($ch, CURLOPT_URL, $testurl);  // set url $testurl   
   curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); //return the transfer as a string
   curl_setopt($ch, CURLOPT_HEADER, 0);
   $output = curl_exec($ch); // $output contains the output string       
   curl_close($ch); // close curl resource to free up system resources
   echo $output;
```
 
我们可以看到，在PHP中我们使用CURL来抓取网站或者编写网站接口（使用json或xml来传递数据）。
我们用curl_setopt() 来设置一个cURL传输选项，有一长串cURL参数可供设置，它们能指定URL请求的各个细节。由于参数较多，需要大家慢慢掌握，不过我们只要知道一些常用的参数即可，其他的随用随查。 
 
使用POST传递数据的设置：

```
  curl_setopt($ch, CURLOPT_POST, 1); //启用发送常规的POST请求
  curl_setopt($ch, CURLOPT_POSTFIELDS, $postData);  //$postData 是要post的数据
``` 

设置cURL允许执行的最长秒数：

```
  curl_setopt($ch, CURLOPT_TIMEOUT, 10); //执行10s
```

cURL 函数

curl_close — 关闭一个cURL会话
curl_copy_handle — 复制一个cURL句柄和它的所有选项
curl_errno — 返回最后一次的错误号
curl_error — 返回一个保护当前会话最近一次错误的字符串
curl_escape — URL encodes the given string
curl_exec — 执行一个cURL会话
curl_file_create — Create a CURLFile object
curl_getinfo — 获取一个cURL连接资源句柄的信息
curl_init — 初始化一个cURL会话
curl_multi_add_handle — 向curl批处理会话中添加单独的curl句柄
curl_multi_close — 关闭一组cURL句柄
curl_multi_exec — 运行当前 cURL 句柄的子连接
curl_multi_getcontent — 如果设置了CURLOPT_RETURNTRANSFER，则返回获取的输出的文本流
curl_multi_info_read — 获取当前解析的cURL的相关传输信息
curl_multi_init — 返回一个新cURL批处理句柄
curl_multi_remove_handle — 移除curl批处理句柄资源中的某个句柄资源
curl_multi_select — 等待所有cURL批处理中的活动连接
curl_multi_setopt — Set an option for the cURL multi handle
curl_multi_strerror — Return string describing error code
curl_pause — Pause and unpause a connection
curl_reset — Reset all options of a libcurl session handle
curl_setopt_array — 为cURL传输会话批量设置选项
curl_setopt — 设置一个cURL传输选项
curl_share_close — Close a cURL share handle
curl_share_init — Initialize a cURL share handle
curl_share_setopt — Set an option for a cURL share handle.
curl_strerror — Return string describing the given error code
curl_ — Decodes the given URL encoded string
curl_version — 获取cURL版本信息
 
【参考阅读】

基于PHP的cURL快速入门
http://bbs.blueidea.com/forum.php?mod=viewthread&tid=2966700  
http//net.tutsplus.com/tutorials/php/techniques-and-resources-for-mastering-curl/
 
PHP手册CURL部分
http://cn2.php.net/manual/zh/book.curl.php
 
PHP curl新浪微博发信接口
http://www.chinaz.com/program/2009/1107/97271.shtml