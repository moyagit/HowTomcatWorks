主要做了以下几个工作
1. 在第一章的基础上添加了container的容器，开始使用单独的Classloader(URLClassLoader)
2. 开始继承和实现javax 规范的类，请求和响应
3. 开始使用servlet 类
4. 在server2 中使用了Facade 类来包装
5. 在书中介绍了javax 相关类的使用方法

servlet 的作用

* 当第一次调用 servlet 的时候，加载该 servlet 类并调用 servlet 的 init 方法(仅仅一 次)。
* 对每次请求，构造一个 javax.servlet.ServletRequest 实例和一个 javax.servlet.ServletResponse 实例。
* 调用 servlet 的 service 方法，同时传递 ServletRequest 和 ServletResponse 对象。
* 当 servlet 类被关闭的时候，调用 servlet 的 destroy 方法并卸载 servlet 类。


Facade 类的作用

*  防止应用开发者调用对象改变tomcat 内部类的状态
* 避免出现攻击行为