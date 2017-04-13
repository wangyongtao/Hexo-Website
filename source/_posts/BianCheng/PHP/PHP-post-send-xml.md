---
title: PHP如何以post形式发送xml数据 
date: 2013-04-25
tags: 
- PHP
categories:
- PHP
---


内容提示：

PHP如何以POST形式发送XML数据，PHP如何接收XML文件

发送XML: postXml.php

```
$xmlData = "
< xml >ad775b217< /ToUserName >
< FromUserName >tWy3zC3xUgQMR5coXif5SA< /FromUserName >
< CreateTime >1366181013< /CreateTim e>
< MsgType >text< /MsgType >
< Content >我的测试< /Content >
< MsgId >5867702771251151243< /MsgId >
< /xml >";
```

## 第一种发送方式，也是推荐的方式：curl

```
$url = 'http://cnwyt.net/xml/getXml.php';  //接收xml数据的文件
$header[] = "Content-type: text/xml";        //定义content-type为xml,注意是数组
$ch = curl_init ($url);
curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $xmlData);
$response = curl_exec($ch);
if(curl_errno($ch)){
    print curl_error($ch);
}
curl_close($ch);
```

## 第二种发送方式：fsockopen

```
$url = 'http://cnwyt.net/xml/getXml.php';
$header[] = "Content-type: text/xml";//定义content-type为xml
$server ='http://wang.net/';
$contentLength = strlen($xml_data);
$fp = fsockopen('127.0.0.1', 80);
fputs($fp, "POST $url HTTP/1.0\r\n");
fputs($fp, "Host: $server\r\n");
fputs($fp, "Content-Type: text/xml\r\n");
fputs($fp, "Content-Length: $contentLength\r\n");
fputs($fp, "Connection: close\r\n");
fputs($fp, "\r\n");     // all headers sent
fputs($fp, $xmlData );
$result = '';
while (!feof($fp)) {
    $result .= fgets($fp, 128);
}
var_dump($result);
```

接收XML: getXml.php

```
//$xml = $HTTP_RAW_POST_DATA;
$xml = $GLOBALS['HTTP_RAW_POST_DATA'];
//将xml数据写入文本文件"a.txt"中
$handle  = fopen('a.txt','a+'); 
fwrite($handle,$xml);
```

## FAQ

问题：为什么不使用$_POST接收？
解答：由于PHP默认只识别application/x-www.form-urlencoded标准的数据类型，对型如text/xml的内容无法解析为$_POST数组，故保留原型，交给$GLOBALS['HTTP_RAW_POST_DATA'] 来接收。注意，$HTTP_RAW_POST_DATA 对于 enctype="multipart/form-data" 表单数据不可用。  

扩展阅读：

使用PHP CURL的POST数据
http://www.nowamagic.net/librarys/veda/detail/124
$HTTP_RAW_POST_DATA
http://www.cnblogs.com/xwblog/archive/2011/12/23/2299672.html

## 更新记录

* 2013-04-25 新增此文档 (wangyt)  
* 2017-04-12 重新整理本文档 (wangyt)

[END]
