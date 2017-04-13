---
title: PHP如何判断接收到的是否为正确的图片二进制数据
date: 2013-03-22
tags: 
- PHP
categories:
- PHP
---


PHP如何判断接收到的是否为正确的图片二进制数据


(一)、如果存在GD库，可以使用imagecreatefromstring ()函数：

格式：resource imagecreatefromstring ( string $image )
imagecreatefromstring() 返回一个图像标识符，其表达了从给定字符串得来的图像。图像格式将自动检测，只要 PHP 支持：JPEG，PNG，GIF，WBMP 和 GD2。
返回值：成功则返回图像资源，如果图像格式不支持，数据不是认可的格式，或者图像已损坏则返回 FALSE。
代码示例：

```
<?php代码开始
$imgUrl = "http://www.baidu.com/img/shouye_b5486898c692066bd2cbaeda86d74448.gif";
$data = file_get_contents($imgUrl);
//echo ($data);
$im = imagecreatefromstring($data);
if($im != false){
    echo '<p>图片正常...</p>';
}else{
    echo '<p>图片已损坏...</p>';
}
代码结束?>
```

```
<?php代码开始
$data = 'iVBORw0KGgoAAAANSUhEUgAAABwAAAASCAMAAAB/2U7WAAAABl'
       . 'BMVEUAAAD///+l2Z/dAAAASUlEQVR4XqWQUQoAIAxC2/0vXZDr'
       . 'EX4IJTRkb7lobNUStXsB0jIXIAMSsQnWlsV+wULF4Avk9fLq2r'
       . '8a5HSE35Q3eO2XP1A1wQkZSgETvDtKdQAAAABJRU5ErkJggg==';
$data = base64_decode($data);
$im = imagecreatefromstring($data);
if ($im !== false) {
    header('Content-Type: image/png');
    imagepng($im);
} else {
    echo 'An error occured.';
}
代码结束?>
```

（二）、如果没有GD库可以使用下边的方法：

正常的JPG文件都是以FFD8开头，FFD9结尾的，如果丢失了文件尾部，JPG仍然可以被识别，但是就会丢失部分图像数据。

代码如下：

```
    function check_img_by_source($source) {
        switch(bin2hex(substr($source,0,2))){
            case 'ffd8' : return 'ffd9' === bin2hex(substr($source,-2));
            case '8950' : return '6082' === bin2hex(substr($source,-2));
            case '4749' : return '003b' === bin2hex(substr($source,-2));
            default : return false;
        }
    }
var_dump(check_img_by_source(file_get_contents('11.gif'));
```

大概是这个样子的吧，只针对了jpg,png,gif做了判断。
想加其他的按照以上规则增加即可。
不过上边这个判断不够严谨，别人可以根据以上判断规则构造一个假数据。

（三）、使用 getimagesize 函数

getimagesize() 函数将测定任何 GIF，JPG，PNG，SWF，SWC，PSD，TIFF，BMP，IFF，JP2，JPX，JB2，JPC，XBM 或 WBMP 图像文件的大小并返回图像的尺寸以及文件类型和一个可以用于普通 HTML 文件中 IMG 标记中的 height/width 文本字符串。

如果不能访问 filename 指定的图像或者其不是有效的图像，getimagesize() 将返回 FALSE 并产生一条 E_WARNING 级的错误。


函数拓展：

imagecreatefromjpeg() - 从 JPEG 文件或 URL 新建一图像
imagecreatefrompng() - 从 PNG 文件或 URL 新建一图像
imagecreatefromgif() - 从 GIF 文件或 URL 新建一图像
imagecreatetruecolor() - 新建一个真彩色图像
exif_read_data() — 从 JPEG 或 TIFF 文件中读取 EXIF 头信息（别名：read_exif_data ）
file_get_contents() — 将整个文件读入一个字符串
base64_decode() — 对使用 MIME base64 编码的数据进行解码
bin2hex() — 将二进制数据转换成十六进制表示

参考链接：
德问：http://www.dewen.org/q/2643

## 更新记录

* 2013-03-22 新增此文档 (wangyt)  
* 2017-04-12 重新整理本文档 (wangyt)

[END]