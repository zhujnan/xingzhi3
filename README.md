# xingzhi3
test
# 网络编程

### 一、网络编程概述

​		Java是 Internet 上的语言，它从语言级上提供了对网络应用程序的支持，程序员能够很容易开发常见的网络应用程序。
​		Java提供的网络类库，可以实现无痛的网络连接，联网的底层细节被隐藏在 Java 的本机安装系统里，由 JVM 进行控制。并且 Java 实现了一个跨平台的网络库，程序员面对的是一个统一的网络编程环境。

### 1.1TCP和UDP的差异

​		TCP是面向连接的协议，在正式收发数据前，必须和对方建立可靠的连接，所以速度会慢；UDP是面向无连接的协议，不与对方建立连接，而是直接就发送数据包，相对速度快；

​		TCP提供IP环境下的数据可靠传输，保证数据无差错的、按照顺序的进行传输；UDP的传输是不可靠的，不保证数据正确，不保证顺序等，也可能丢包；
​		TCP使用字节流模式发送数据，UDP使用数据报模式; 

​		TCP适用对可靠性要求高的应用环境；UDP适用于一次只传送少量数据、对可靠性要求不高的应用环境；

### 1.2什么是Socket

​		大部分计算机都已经连接到互联网，在此基础上考虑如何编写<font color='red'>数据传输程序。</font>操作系统已经提供了Socket，

不需要对网络数据传输原理很熟悉，也能通过<font color='red'>socket("插座")</font>来编程，socket被翻译为<font color='red'>“套接字”</font>。socket是计算机

之间通信的一种约定或一一种方式，一台pc可以接收其他pc的数据，也可向其他pc发送数据。

​		例如把插头插到插座上就可以从电网中获得电力供应，同样与远程计算机数据传输，需要连接到因特网，而socket就是用来连接到因特网的工具。

​       **典型应用： web服务器、浏览器；浏览器获取用户输入的URL,向服务器发送请求，服务器分析接收到的url,将对应的网页内容返回给浏览器，浏览器再经过解析和渲染。将文字、图片、视频等元素呈现给用户。**

​	**学习Socket就是学习计算机之间如何通信，编写出使用的程序。**



## 二、案例实现

2.1客户端与服务端通信

​	服务端代码：

```java
		//1.建立服务端Socket服务，监听一个端口号（最大值为65535）
		ServerSocket server = new ServerSocket(10086);
		//2.获取连接过来的客户对象
		Socket client = server.accept();
		System.out.println("ip"+client.getInetAddress().getHostAddress());
		//3.使用客户端对象的读取流来读取客户端发送的数据。
		InputStream in = client.getInputStream();
		byte[] buf = new byte[1024];
		int len = in.read(buf);
		System.out.println(new String(buf,0,len));
		client.close();
		
```

​	客户端代码：

```java
		//1，创建客户端的socket服务，指定目的主机和端口。
		Socket s = new Socket("127.0.0.1",10086);
		//2.获取Socket流中的输出流发送数据。
		OutputStream out = s.getOutputStream();
		out.write("hello,world！".getBytes());
		s.close();
```

