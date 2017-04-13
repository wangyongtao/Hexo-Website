---
title: Linux-压力测试工具Siege安装与使用
date: 2016-09-08
tags: 
- Linux
- Siege
categories:
- Linux
- Siege
---

Siege 是Linux/Unix下的一个WEB系统的压力测试工具。

Siege is an http load testing and benchmarking utility. 

下载与安装:

下载地址: http://download.joedog.org/siege/   
目前最新版本是 2016-05-20 发布的 siege-4.0.2.tar.gz

```
$ wget http://download.joedog.org/siege/siege-latest.tar.gz
$ tar zxf siege-latest.tar.gz
$ cd siege-4.0.2/
$ ./configure
$ sudo make
$ sudo make install
```

查看是否安装成功:

查看siege安装路径:

```
$ which siege
/usr/local/bin/siege
```

查看siege版本:

```
$ siege -V
SIEGE 4.0.2
```

参数说明:

可以使用"siege -h"命令来查看帮助信息:

```
$ siege -h
SIEGE 4.0.2
Usage: siege [options]
       siege [options] URL
       siege -g URL
Options:
  -V, --version             VERSION, prints the version number.
  -h, --help                HELP, prints this section.
  -C, --config              CONFIGURATION, show the current config.
  -v, --verbose             VERBOSE, prints notification to screen.
  -q, --quiet               QUIET turns verbose off and suppresses output.
  -g, --get                 GET, pull down HTTP headers and display the
                            transaction. Great for application debugging.
  -c, --concurrent=NUM      CONCURRENT users, default is 10
  -r, --reps=NUM            REPS, number of times to run the test.
  -t, --time=NUMm           TIMED testing where "m" is modifier S, M, or H
                            ex: --time=1H, one hour test.
  -d, --delay=NUM           Time DELAY, random delay before each requst
  -b, --benchmark           BENCHMARK: no delays between requests.
  -i, --internet            INTERNET user simulation, hits URLs randomly.
  -f, --file=FILE           FILE, select a specific URLS FILE.
  -R, --rc=FILE             RC, specify an siegerc file
  -l, --log[=FILE]          LOG to FILE. If FILE is not specified, the
                            default is used: PREFIX/var/siege.log
  -m, --mark="text"         MARK, mark the log file with a string.
                            between .001 and NUM. (NOT COUNTED IN STATS)
  -H, --header="text"       Add a header to request (can be many)
  -A, --user-agent="text"   Sets User-Agent in request
  -T, --content-type="text" Sets Content-Type in request
```

查看当前的配置信息

$ siege -C

使用说明:

(1) 直接请求URL:

```
$ siege -c 20 -r 10 http://www.cnwytnet.com
```

参数说明： -c 是并发量，并发数为20人 -r 是重复次数， 重复10次

(2) 随机选取urls.txt中列出所有的网址

在当前目录下创建一个名为"urls-demo.txt"的文件。 
文件里边填写URL地址，可以有多条，每行一条，比如：

```
# URLs:
http://www.sogou.com/web?query=php&from=wang_yong_tao
https://www.baidu.com/
// 执行 $ siege -c 5 -r 10 -f urls-demo.txt $ siege -c 5 -r 10 -f /Users/WangYoungTom/temp/urls-demo.txt
```

参数说明： -c 是并发量，并发数为5人 -r 是重复次数， 重复10次 -f 指定使用文件，urls-demo.txt就是一个文本文件，每行都是一个url，会从里面随机访问的

Siege从Siege-V2.06起支持POST和GET两种请求方式。 如果想模拟POST请求，可以在urls-demo.txt中安装一下格式填写URL:

```
# URL （POST）:
http://wangtest.com/index.php POST UserId=XXX&StartIndex=0&OS=Android&Sign=cff6wyt505wyt4c
http://wangtest.com/articles.php POST UserId=XXX&StartIndex=0&OS=iOS&Sign=cff63w5905wyt4c
```

使用示例:

```
// 请求http://www.cnwytnet.com，并发人数为10，重复5次，每次请求间隔3秒
$ siege --concurrent=10 --reps=5 --delay=3 http://www.cnwytnet.com
$ siege -c 10 -r 5 -d 3 http://www.cnwytnet.com
```

结果说明:

```
Transactions: 153 hits (处理次数，本次处理了153此请求)
Availability: 100.00 % (可用性/成功次数的百分比,比如本次100%成功)
Elapsed time: 17.22 secs （运行时间，本次总消耗17.22秒）
Data transferred: 7.70 MB （数据传送量）
Response time: 0.17 secs （响应时间）
Transaction rate: 8.89 trans/sec (处理请求频率，每秒钟处理8.89次请求）
Throughput: 0.45 MB/sec （吞吐量,传输速度）
Concurrency: 1.54 (实际最高并发连接数)
Successful transactions: 153 (成功的传输次数)
Failed transactions: 0 (失败的传输次数)
Longest transaction: 0.70 (处理传输是所花的最长时间)
Shortest transaction: 0.02 (处理传输是所花的最短时间)
```

使用实例:

```
$ siege -c 5 -r 10 http://www.baidu.com

Transactions:                386 hits
Availability:             100.00 %
Elapsed time:              37.40 secs
Data transferred:          19.47 MB
Response time:              0.43 secs
Transaction rate:          10.32 trans/sec
Throughput:             0.52 MB/sec
Concurrency:                4.45
Successful transactions:         386
Failed transactions:               0
Longest transaction:            2.38
Shortest transaction:           0.02
```

## 参考链接:

- 官网 https://www.joedog.org/

- 文档 https://www.joedog.org/siege-manual/#a01

- http://blog.csdn.net/qingye2008/article/details/34500949

更新记录:

- 20160908 整理本文内容
- 20160909 新增整理POST请求内容

[END]