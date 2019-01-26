主要功能如下：
1. 使connecter 和 container 权责更加清晰，通过在初始化页面进行配置
2. 权责更加清晰，也更加好管理
3. connecter 分得更加清晰
4. http 解析更加明确，清晰
5. 性能更加高效


why

```$xslt
为什么 await 需要使用一个本地变量(socket)而不是返回实例的 socket 变量呢?因为这样 一来，在当前 socket 被完全处理之前，实例的 socket 变量可以赋给下一个前来的 socket。
while (!available) { 
     wait(); 
    }
}
Socket socket = this.socket;
 available = false; 
 notifyAll();
return socket; // to the run

```

keepAlive 需要再短时间内发起多个请求才行（处理完一个请求，接着处理另一个请求） ，否则会报错，断开连接
```$xslt
如果keepAlive 是 true 的话，while 循环将会在开头就启动。因为在前 面的解析过程中和容器的 invoke 方法中没有出现错误，或者 HttpProcessor 实例没有被停止。 否则，shutdownInput 方法将会调用，而套接字将被关闭。
try {
shutdownInput(input);
    socket.close();
}
...
shutdownInput 方法检查是否有未读取的字节。如果有的话，跳过那些字节。

```