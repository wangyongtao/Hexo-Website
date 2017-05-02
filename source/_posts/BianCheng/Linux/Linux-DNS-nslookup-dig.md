---
title: Linux-DNS查询命令nslookup和dig
date: 2017-04-01
tags: 
- Linux
categories:
- Linux
---

# nslookup

nslookup - query Internet name servers interactively

```
nslookup wang123.net
Server:     172.16.76.2
Address:    172.16.76.2#53

Non-authoritative answer:
Name:   wang123.net
Address: 106.14.34.47
```

IP地址: 106.14.34.47 上海市上海市 阿里云


# dig

dig - DNS lookup utility
 
```
$ dig wang123.net
; <<>> DiG 9.8.3-P1 <<>> wang123.net
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 63352
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;wang123.net.           IN  A

;; ANSWER SECTION:
wang123.net.        181 IN  A   106.14.34.47

;; Query time: 38 msec
;; SERVER: 172.16.76.2#53(172.16.76.2)
;; WHEN: Tue May  2 10:29:19 2017
;; MSG SIZE  rcvd: 45
```

# host 

host - DNS lookup utility

```
$ host wang123.net
wang123.net has address 106.14.34.47
wang123.net mail is handled by 5 mxn.mxhichina.com.
wang123.net mail is handled by 10 mxw.mxhichina.com.
```

# ping

ping -- send ICMP ECHO_REQUEST packets to network hosts

```
$ ping wang123.net
PING wang123.net (106.14.34.47): 56 data bytes
64 bytes from 106.14.34.47: icmp_seq=0 ttl=54 time=77.463 ms
64 bytes from 106.14.34.47: icmp_seq=1 ttl=54 time=9.717 ms
64 bytes from 106.14.34.47: icmp_seq=2 ttl=54 time=117.081 ms
^C
--- wang123.net ping statistics ---
3 packets transmitted, 3 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 9.717/68.087/117.081/44.330 ms
```

# 参考

* Linux Man 