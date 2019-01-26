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

#注意点

* HTTP 请求对象由实现了 javax.servlet.http.HttpServletRequest 的 HttpRequest 类来代表。一个 HttpRequest对象将会给转换为一个HttpServletRequest实例并传递给被调用 的 servlet 的 service 方法。因此，每个 HttpRequest 实例必须适当增加字段，以便 servlet 可以使用它们。值需要赋给 HttpRequest 对象，包括 URI，查询字符串，参数，cookies 和其他 的头部等等。因为连接器并不知道被调用的 servlet 需要哪个值，所以连接器必须从 HTTP 请求 中解析所有可获得的值。

*  解析一个 HTTP 请求牵涉昂贵的字符串和其他操作，假如只是解 析 servlet 需要的值的话，连接器就能节省许多 CPU 周期。例如，假如 servlet 不 解析任何一 个 请 求 参 数 ( 例 如 不 调 用 javax.servlet.http.HttpServletRequest 的 getParameter, getParameterMap,getParameterNames 或者 getParameterValues 方法)，连接器就不需要从查询 字符串或者 HTTP 请求内容中解析这些参数。Tomcat 的默认连接器(和本章应用程序的连接器) 试图不解析参数直到 servlet 真正需要它的时候，通过这样来获得更高效率。

* Tomcat 的默认连接器和我们的连接器使用 SocketInputStream 类来从套接字的 InputStream 中读取字节流。一个 SocketInputStream 实例对从套接字的 getInputStream 方法中返回的 java.io.InputStream 实例进行包装。 SocketInputStream 类提供了两个重要的方法: readRequestLine 和 readHeader。readRequestLine 返回一个 HTTP 请求的第一行。例如，这行 包括了 URI，方法和 HTTP 版本。因为从套接字的输入流中处理字节流意味着只读取一次，从第 一个字节到最后一个字节(并且不回退)，因此 readHeader 被调用之前，readRequestLine 必须 只被调用一次。readHeader 每次被调用来获得一个头部的名/值对，并且应该被重复的调用知道 所有的头部被读取到。readRequestLine 的返回值是一个 HttpRequestLine 的实例，而 readHeader 的返回值是一个 HttpHeader 对象