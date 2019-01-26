主要有以下功能
1. 区分开了connect 和 container 了
2. connect 主要专注于http 协议解析，填充 http method, protocol 等
3. container 不变

connect 

* 主要是解析http 协议，这个应该不是最终版，看起来好繁琐
* 大部分解析http方法能做到这样已经很不错了

compare

用第二章的代码打印请求头
```
GET /servlet/PrimitiveServlet HTTP/1.1
Host: 127.0.0.1:8081
User-Agent: curl/7.54.0
Accept: */*
```

修改baidu 的请求

```
GET /servlet/PrimitiveServlet?num=8&indextype=manht&_req_seqid=0xb493bdf900111fec&asyn=1&t=1548508445305&sid=26523_1437_21088_18560_28328 HTTP/1.1
Host: 127.0.0.1:8081
Cookie: BD_UPN=123253; PSTM=1514209316; BIDUPSID=0F112D9249B47B20636A2D88530F4715; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; BAIDUID=00DF41F86AB27005B1DC64C7CAEA2BE8:FG=1; BDUSS=0lQdWFpaENiNFpYZGZnRkhKSWlQc2xXWklSen55ZzRIdXk3aXE1WHJFNE9BRXRjQVFBQUFBJCQAAAAAAAAAAAEAAADcQ5YXbXkyMDExMTM0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA5zI1wOcyNcb; MCITY=-%3A; ispeed_lsm=0; BDSFRCVID=UckOJeC62AjHFHQ9s_3wJR6gh-TsAlcTH6aoq10xZrBCIDYJZPyQEG0PjM8g0KAbJmfpogKK0mOTHUuF_2uxOjjg8UtVJeC6EG0P3J; H_BDCLCKID_SF=tJ4q_IPMJK_3qR5gMJ5q-n3HKUrL5t_XbI6y3JjOHJOoDDvs-nOcy4LdjG5CKl3BaaC8Qh6vBhcCMR3dDlnpKM_73-Aq54RA2g7Oof5CbfjUolcLQloKQfbQ0M6uqP-jW5TaaJ6D-n7JOpkxhfnxyhLfQRPH-Rv92DQMVU52QqcqEIQHQT3mDUThDG8HJj0tfnFsL-35HJcEHJvphPOHKPktqxby26PO-Jn9aJ5nJDoCHn5u5j_BKUT-Q2cp05cu2D7X_x58QpP-HJAl5RDhjMKI-4QeW4kq3N7GKl0MLPjWbb0xynoDM5tghxnMBMPjamOnaPLE3fAKftnOM46JehL3346-35543bRTohFLtDt-MKPxjTK3K4LOMq5-5b0X-K5L3JD8bnjoHRjvq4bohjPA-UR9BtQmJJrCBqnIWUDBqUAR5U6Cj4-JqJOe3472Qg-q3R7htCJWo4otLUrUWfIl0hrI0x-jLIQuVn0MWhjDOR6IK-nJyUnQhtnnBpQt3H8HL4nv2JcJbM5m3x6qLTKkQN3TJMIEK5r2SC-yJIKa3e; H_PS_PSSID=26523_1437_21088_18560_28328; delPer=0; BD_CK_SAM=1; PSINO=1; BD_HOME=1; BDRCVFR[S4-dAuiWMmn]=I67x6TjHwwYf0; sug=3; sugstore=0; ORIGIN=0; bdime=0
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36
Accept: text/plain, */*; q=0.01
Referer: https://www.baidu.com/
X-Requested-With: XMLHttpRequest
Connection: keep-alive
java.lang.ClassNotFoundException: PrimitiveServlet?num=8&indextype=manht&_req_seqid=0xb493bdf900111fec&asyn=1&t=1548508445305&sid
```