# 一、HTTP协议

## 1. HTTP简介

### 1.1 HTTP概念

- HTTP协议，即Hyper Text Transfer Protocol（超文本传输协议），是一种详细规定了 **浏览器和万维网（www）服务器之间** 互相通信的规则，通过因特网传送万维网文档的数据传送协议；

- 用于从万维网（WWW: World Wide Web）服务器传输超文本到本地浏览器的传送协议；
- HTTP是一个**基于TCP/IP通信协议**，通过**请求与响应**，**无状态的**，**应用层协议** 来传输数据（HTML文件，图片文件，查询结果等）
- 网络层：IP、ICMP、ARP、RARP、BOOTP
- 传输层：TCP、UDP
- 应用层：FTP、HTTP、SMTP、DNS、TELENT



### 1.2 HTTP工作原理

- HTTP协议工作于客户端-服务端架构上。浏览器作为HTTP客户端通过URL向HTTP服务端即WEB服务器发送所有请求。

- WEB服务器有：Apache服务器，IIS服务器（Internet Information Services）等。

- WEB服务器根据接收到的请求后，向客户端发送响应信息。

- HTTP默认端口为80，也可以改为8080或其他端口。

- **HTTP三点注意事项**：

  1. **HTTP是无连接**：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应答后，即断开连接。采用这种方式可以节省传输时间。
  2. **HTTP是媒体独立的**：这意味着，只要客户端和服务器知道如何处理的数据内容，任何类型的数据都可以通过HTTP发送。客户端和服务器指定使用适合的MIME-type内容类型。
  3. **HTTP是无状态**：HTTP协议是无状态协议。**无状态是指协议对于事务处理没有记忆能力**。缺少状态意味着如果后续处理需要前面的信息，则必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。

- **HTTP协议通信流程**：

  ![cgiarch](https://www.runoob.com/wp-content/uploads/2013/11/cgiarch.gif)

  - 客户端发送一个HTTP请求，说明客户端想要访问的资源和请求的动作；
  - 服务端收到请求后，服务端开始处理请求，并根据请求做相应的动作访问服务器资源；
  - 最后通过发送HTTP响应把结果返回给客户端。

  > 其中一个请求的开始到一个请求的结束称为事务，当一个事务结束后还会在服务端添加一条日志条目。



## 2. HTTP消息结构

- HTTP是基于客户端/服务端（C/S）的架构模型，通过一个可靠的连接来交换信息，是一个无状态的请求/响应协议。
- 一个**HTTP“客户端”**是一个应用程序（web浏览器或其他任何客户端），通过连接服务器达到向服务器发送一个或多个HTTP请求的目的。
- 一个**HTTP"服务器"**也是一个应用程序（通常是一个web服务，如Apache web服务器或IIS服务器等），通过接收客户端的请求并向客户端发送HTTP响应数据。
- HTTP使用统一资源标识符（Uniform Resource Identifiers, URI）来传输数据和建立连接。

### 2.1 客户端请求消息

- 客户端发送一个HTTP请求到服务器，告知服务器自己的要求，请求消息包括以下格式：

  - **请求行（request line）**：包括请求方式Method（详细见第3）、资源路径URL、协议版本Version;
  - **请求头部（header）**：包括一些访问的域名、用户代理、Cookie等消息；
  - **空行**
  - **请求正文**

- **HTTP请求报文**：

  ![blob.png](https://s1.51cto.com/images/20180426/1524747772856125.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)
  - 请求报文的起始由 **请求行** 构成，用来说明该请求想要做什么，由<Method>、<URL>、<Version>三个字段组成，每个字段之间有一个空格。
  - **首部** 部分由多个请求头构成，首部字段名有如下：
    - Accept：指定客户端能够接收的内容格式类型
    - Accept-Language：指定客户端能够接收的语言类型
    - Accept-Ecoding：指定客户端能够接收的编码类型
    - User-Agent：用户代理，向服务器说明自己的操作系统、浏览器等信息
    - Connection：是否开启持久连接（keepalive）
    - Host：服务器域名
    - ...
  - **主体部分**就是报文的具体数据



### 2.2 服务器响应消息

- 服务器收到了客户端发来的HTTP请求后，根据HTTP请求中的动作要求，服务端做出具体的动作，将结果返回给客户端，称为HTTP响应。

- HTTP响应也由四个部分组成：
  - **状态行**：包括协议版本Version、状态码Status Code、回应短语；
  - **消息报头**：包括搭建服务器的软件，发送响应的时间，回应数据的格式等信息；
  - **空行**
  - **响应正文** 

- **HTTP响应报文**：

  ![blob.png](https://s1.51cto.com/images/20180426/1524748488887423.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=)

  - 响应报文的起始由 **状态行** 构成，用来说明服务器做了什么，由<Version>、<Status-Code>、<Phrase>三个字段组成
  - **首部** 由多个响应头组成，首部字段名有如下：
    - Allow：服务器支持哪些请求方法（如GET、POST等）
    - Server：服务器软件名，Apache、Nginx
    - Date：服务器发出响应报文的时间
    - Last-Modified：请求资源的最后的修改时间
    - Content-Encoding：文档的编码方法
    - Content-Length：表示内容长度
    - Content-Type：表示后面的文档属于什么MIME类型
    - ...
  - **主体部分** 是响应报文的具体数据

- 响应报文实例：

  ```http
  HTTP/1.1 200 OK	<!--状态行-->
  Date:Sat,31 Dec 2005 23:59:59 GMT	<!--消息报头-->
  Content-Type:text/html;charset=ISO-8859-1	<!--消息报头-->
  Content-Length:122	<!--消息报头-->
  <!--空行-->
  <html>	<!--响应正文-->
      <head></head>
      <body></body>
  </html>
  ```

> 备注：我们主要关心并且能够在 **客户端浏览器** 看得到的是三位数的 **状态码**，不同的状态码代表不同的含义，其中：
>
> - 1xx：表示HTTP请求已经接受，继续处理请求
> - 2xx：表示HTTP请求已经处理完成
> - 3xx：表示把请求访问的URL重定向到其他目录
> - 4xx：表示客户端出现错误
> - 5xx：表示服务端出现错误



### 2.3 请求/响应实例

- 客户端请求：

  ```http
  GET /hello.txt HTTP/1.1
  User-Agent:curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.71 zlib/1.2.3
  Host:www.example.com
  Accept-Language:en,mi
  ```

- 服务端响应：

  ```http
  HTTP/1.1 200 OK
  Date:Mon,27 Jul 2009 12:28:53 GMT
  Server:Apache
  Last-Modified:Wed,22 Jul 2009 29:15:56 GMT
  ETag:"34aa387-d-1568eb00"
  Accept-Ranges: bytes
  Content-Length: 51
  Vary: Accept-Encoding
  Content-Type: text/plain
  ```



### 2.4 常见状态码含义

- 200：OK，请求已经正常处理完毕
- 301：请求永久重定向
- 302：请求临时重定向
- 304：请求被重定向到客户端本地缓存
- 400：客户端请求存在语法错误
- 401：客户端请求没有经过授权
- 403：客户端的请求被服务器拒绝，一般为客户端没有访问权限
- 404：客户端请求的URL在服务端不存在
- 500：服务端永久错误
- 503：服务端发生临时错误



## 3. HTTP请求方法

- 根据HTTP标准，HTTP请求可以使用多种请求方法。
- HTTP1.0定义了三种请求方法：GET,POST和HEAD方法
- HTTP1.1新增了五种请求方法：OPTIONS,PUT,DELETE,TRACE和CONNECT

| 序号 | 方法    | 描述                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| 1    | GET     | 请求指定的页面信息，并返回实体主体                           |
| 2    | HEAD    | 类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头 |
| 3    | POST    | 向指定资源提交数据进行请求处理（例如提交表单或者上传文件）。数据被包含在请求体中。POST请求可能会导致新的资源的建立和/或已有资源的修改 |
| 4    | PUT     | 从客户端向服务器传送的数据取代指定的文档的内容               |
| 5    | DELETE  | 请求服务器删除指定的页面                                     |
| 6    | CONNECT | HTTP/1.1协议中预留给能够将连续改为管道方式的代理服务器       |
| 7    | OPTIONS | 允许客户端查看服务器的性能                                   |
| 8    | TRACE   | 回显服务器收到的请求，主要用于测试或诊断                     |



## 4. HTTP协议版本更替

### 4.1 HTTP/0.9

- HTTP协议的最初版本，功能简陋，仅支持请求方法 GET，并且仅能请求访问HTML格式的资源。



### 4.2 HTTP/1.0

- 在0.9版本上做了改进，增加了请求方式POST和HEAD；
- 不在局限于HTML格式，根据Content-Type可以支持多种数据格式，即MIME多用途互联网邮件扩展，例如text/html、image/jpeg等；
- 同时也开始支持cache，就是当客户端在规定时间内访问统一网站，直接访问cache即可。
- 但是1.0版本的工作方式是**每次TCP连接只能发送一个请求**，当服务器响应后就会关闭这次连接，下一个请求需要再次建立TCP连接，就是不支持keepalive。



### 4.3 HTTP/1.1

- 解决了1.0版本的keepalive问题，1.1版本加入了持久连接，**一个TCP连接可以允许多个HTTP请求**；
- 加入了管道机制，**一个TCP连接同时允许多个请求同时发送**，增加了并发性；
- 增加了请求方式PUT、PATCH、DELETE等
- 存在问题：
  - 服务端是 **按队列顺序处理请求**的，假如一个请求处理时间很长，则会导致后边的请求无法处理，这样就造成了**队头阻塞**的问题；
  - 同时HTTP是无状态的连接，因此每次请求都 **需要添加重复的字段**，降低了宽带的利用率。



### 4.4 HTTP/2.0

- 为了解决1.1版本利用率不高的问题，提出了HTTP/2.0版本；
- 增加双工模式，即不仅 **客户端能够同时发送多个请求**，**服务端也能同时处理多个请求**，解决了队头阻塞的问题；
- HTTP请求和响应中，**请求行**、**状态行**和**请求头/响应头**都是些信息字段，并没有真正的数据，因此在2.0版本中将所有的信息字段建立一张表，为表中的每个字段建立索引，客户端和服务端共同使用这个表，它们之间就以索引号来表示信息字段，这样就避免了1.0旧版本的重复繁琐的字段，并以压缩的方式传输，提高利用率；
- 增加服务器推送的功能，即不经请求服务端主动向客户端发送数据。



## 5. HTTP和HTTPS

- 资料：<https://blog.csdn.net/xiaoming100001/article/details/81109617>

### 5.1 什么是HTTPS

- 《图解HTTP》这本书中曾提过HTTPS是身披SSL外壳的HTTP。HTTPS是一种通过计算机网络进行安全通信的传输协议，经由HTTP进行通信，利用SSL/TLS建立全信道，加密数据包。HTTPS使用的主要目的是 **提供对网站服务器的身份认证，同时保护交换数据的隐私与完整性**。

  > PS: TLS是传输层的加密协议，前身是SSL协议



### 5.2 HTTP

- **HTTP 特点**：
  1. **无状态**：协议对客户端没有状态储存，**对事物处理没有记忆能力**，比如访问一个网站需要反复进行登录操作；
  2. **无连接**：HTTP/1.1之前，由于无状态特点，每次请求需要通过TCP三次握手+四次挥手，和服务器重新建立连接。比如某个客户机在短时间多次请求同一个资源，服务器并不能区别是否响应过用户的请求，所以每次需要重新响应请求，需要耗费不必要的时间和流量；
  3. **基于请求和响应**：基本的特性，由客户端发起请求，服务端响应；
  4. 简单快速、灵活；
  5. 通信使用明文、请求和响应不会对通信方进行确认，无法保护数据的完整性。
- **针对无状态的一些解决策略**：
  - 场景：逛电商商场用户需要使用的时间比较长，需要对用户一段时间的HTTP通信状态机进行保存，比如执行一次登录操作，在30分钟内所有的请求都不需要再次登录
    1. 通过Cookie/Session技术；
    2. HTTP/1.1 持久连接（HTTP keep-alive）方法，只要任意一端没有明确提出断开连接，则保持TCP连接状态，在请求首部字段中的Connection:keep-alive即为表明使用了持久连接



### 5.3 HTTPS

- **HTTPS 特点**：基于HTTP协议，通过SSL或TLS提供加密处理数据、验证对方身份以及保护数据完整性。
  1. **内容加密**：采用混合加密技术，中间者无法直接查看明文内容
  2. **验证身份**：通过证书认证客户端访问的是自己的服务器
  3. **保护数据完整性**：防止传输的内容被中间人冒充或者篡改

> **混合加密**：结合非对称加密和对称加密技术。客户端使用对称加密生成秘钥对传输数据进行加密，然后使用非对称加密的公钥再对秘钥进行加密，所以网络上传输的数据是被秘钥加密的密文和用公钥加密的秘密秘钥，因此即使被黑客截取，由于没有私钥，无法获取到加密明文的秘钥，便无法获取到明文数据。
>
> **数字摘要**：通过单向hash函数对原文进行哈希，将需加密的明文“摘要”成一串固定长度的密文，不同的明文摘要成的密文其结果总是不相同，同样的明文其摘要必定一致，并且即使知道了摘要也不能反推出明文。
>
> **数字签名技术**：数字签名建立在公钥加密体制基础上，是公钥加密技术的另一类应用。它把公钥加密技术和数字摘要结合起来，形成了实用的数字签名技术。
>
> - 收方能够证实发送方的真实身份；
> - 发送方事后不能否认所发送过的报文；
> - 收方或非法者不能伪造、篡改报文。



### 5.4 HTTP通信传输

![è¿éåå¾çæè¿°](https://img-blog.csdn.net/20180719094739178?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

- 客户端输入URL回车，DNS解析域名得到服务器的IP地址，服务器在80端口监听客户端请求，端口通过TCP/IP协议（可以通过socket实现）建立连接。HTTP属于TCP/IP模型中的应用层，所以通信的过程其实是对应数据的入栈和出栈。

![è¿éåå¾çæè¿°](https://img-blog.csdn.net/20180719094756330?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9taW5nMTAwMDAx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)



### 5.5 HTTPS实现原理

![è¿éåå¾çæè¿°](http://on-img.com/chart_image/5b503d10e4b0edb750e0d4f8.png)

1. client向server发送请求 https://baidu.com，然后连接到server的443端口；

2. 服务端必须要有一套数字证书，可以自己制作，也可以向组织申请。区别在于自己颁发的证书需要客户端验证通过，才可以继续访问，而使用受信任的公司申请的证书则不会弹出提示页面，这套证书其实就是一对公钥和私钥；

3. 传送证书

   这个证书其实就是公钥，只是包含了很多信息，如证书的颁发机构，过期时间、服务端的公钥，第三方证书认证机构（CA）的签名，服务端的域名信息等内容。

4. 客户端解析证书

   这部分工作是由客户端的TLS来完成的，首先会验证公钥是否有效，比如颁发机构，过期时间等等，如果发现异常，则会弹出一个警告框，提示证书存在问题。如果证书没有问题，那么就生成一个随机值（秘钥）。然后用证书对该随机值进行加密。

5. 传送加密信息

   这部分传送的是用证书加密后的秘钥，目的就是让服务端得到这个秘钥，以后客户端和服务端的通信就可以通过这个随机值来进行加密解密了。

6. 服务端加密信息

   服务端用私钥解密秘密秘钥，得到了客户端传过来的私钥，然后把内容通过该值进行对称加密。

7. 传输加密后的信息

   这部分信息是服务端用私钥加密后的信息，可以在客户端被还原

8. 客户端解密信息

   客户端用之前生成的秘钥解密服务端传过来的信息，于是获取了解密后的内容。



# 二、HttpClient使用详解

## 1. HttpClient简介

- HttpClient是Apache Jakarta Common 下的子项目，用来提供高效的、最新的功能丰富的支持HTTP协议的客户端编程工具包，并且支持HTTP协议最新的版本和建议。
- HttpClient 的主要功能：
  - 基于标准的、纯净的Java语言，实现了HTTP1.0和HTTP1.1
  - 以可以扩展的面向对象的结构实现了HTTP全部的方法（GET/POST/PUT/HEAD/DELETE/OPTIONS等）
  - 支持加密的HTTPS协议、
  - 通过HTTP代理方式建立透明的连接
  - 支持代理服务器（Nginx等）
  - 利用CONNECT方法通过HTTP代理建立隧道的HTTPS连接
  - Basic, Digest...等认证方案
  - 插件式的自定义认证方案
  - 可插拔的安全套接字工厂，使得接入第三方解决方案变得容易
  - 连接管理支持多线程的应用。支持设置最大连接数，同时支持设置每个主机的最大连接数，发现关闭过期的连接。
  - 自动化处理Set-Cookie：来自服务器的头，并在适当的时候将它们发送回cookie
  - 可以自定义Cookie策略的插件化机制
  - Request的输出流可以避免流中内容体直接从socket缓冲到服务器
  - Reponse的输入流可以有效的从socket服务器直接读取相应内容
  - 在HTTP1.0和HTTP1.1中使用keep-alive来保持持久连接
  - 可以直接获取服务器发送的响应码和响应头部
  - 具备设置连接超时的能力
  - 支持HTTP/1.1响应缓存
  - 源代码基于Apache License可免费获取
  - 支持自动（跳转）转向
  - ...



## 2.一般使用步骤

- 使用**HttpClient发送请求**、**接收响应**，一般需要以下步骤：

- **HttpGet请求响应的一般步骤**：

  1. 创建HttpClient对象，可以使用 `HttpClients.createDefault()`;

  2. 无参数GET请求：直接使用构造方法 `HttpGet(String url)` 创建 HttpGet 对象

     带参数GET请求：先使用 `URIBuilder(String url)` 创建对象，再调用 `addParameter(String param, String value)`, 或 `setParameter(String param, String value)`来设置请求参数，并调用 `build()` 方法构建一个URI对象。只有构造方法`HttpGet(URI uri)`来创建HttpGet对象；

  3. 创建HttpResponse，调用 `HttpClient` 对象的`execute(HttpUriRequest request)` 发送请求，该方法返回一个`HttpResponse`。调用`HttpResponse`的`getAllHeaders()、getHeaders(String name)`等方法可获取服务器的响应头；调用`HttpResponse`的`getEntity()`方法可获取HttpEntity对象，该对象包装了服务器的响应内容。程序可通过该对象获取服务器的响应内容。通过调用`getStatusLine().getStatusCode()`可以获取响应状态码；

  4. 释放连接。

- **HttpPost请求响应的一般步骤**：

  1. 创建`HttpClient`对象,可以使用`HttpClients.createDefault()`；

  2. **无参数POST请求**：直接使用构造方法`HttpPost(String url)`创建`HttpPost`对象即可；

     **带参数POST请求**：先构建HttpEntity对象并设置请求参数，然后调用setEntity(HttpEntity entity)创建HttpPost对象；

  3. 创建`HttpResponse`，调用`HttpClient`对象的`execute(HttpUriRequest request)`发送请求，该方法返回一个`HttpResponse`。调用`HttpResponse`的`getAllHeaders()、getHeaders(String name)`等方法可获取服务器的响应头；调用`HttpResponse`的`getEntity()`方法可获取HttpEntity对象，该对象包装了服务器的响应内容。程序可通过该对象获取服务器的响应内容。通过调用`getStatusLine().getStatusCode()`可以获取响应状态码；

  4. 释放连接。



## 3. 代码示例

- 构建一个Maven项目，引入以下依赖：

  ```xml
  <dependency>
      <groupId>org.apache.httpcomponents</groupId>
      <artifactId>httpclient</artifactId>
      <version>4.3.5</version>
  </dependency>
  <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-log4j12</artifactId>
      <version>1.7.7</version>
  </dependency>
  <dependency>
      <groupId>org.apache.commons</groupId>
      <artifactId>commons-io</artifactId>
      <version>1.3.2</version>
  </dependency>
  ```

### 3.1 普通无参GET请求

```java
// 普通的无参数get请求：打开一个url,抓取url响应结果
    @Test
    public void doGet() throws Exception{
        // 创建HttpClient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();
        // 创建Get请求
        HttpGet httpGet = new HttpGet("http://www.baidu.com");
        CloseableHttpResponse response = null;
        try{
            // 执行get请求
            response = httpClient.execute(httpGet);
            // 判断返回状态是否为200
            if(response.getStatusLine().getStatusCode()==200){
                // 请求体内容
                String content = EntityUtils.toString(response.getEntity(),"UTF-8");
                // 打出请求体内容
                System.out.println(content);
                // 内容长度
                System.out.println("内容长度："+content.length());
            }
        }finally {
            if(response!=null){
                response.close();
            }
            httpClient.close();
        }
    }
```

### 3.2 执行带参GET请求

```java
// 执行带参数的get请求：模拟使用百度搜索关键字“java”，并获取响应结果
    @Test
    public void doGetParam() throws Exception{
        CloseableHttpClient httpClient = HttpClients.createDefault();
        // 定义请求的参数
        URI uri = new URIBuilder("http://www.baidu.com/s").setParameter("wd","java").build();
        HttpGet httpGet = new HttpGet(uri);
        CloseableHttpResponse response = null;
        try{
            response = httpClient.execute(httpGet);
            if(response.getStatusLine().getStatusCode()==200){
                String content = EntityUtils.toString(response.getEntity(),"UTF-8");
                System.out.println(content);
                System.out.println("内容长度："+content.length());
            }
        }finally {
            if(response!=null){
                response.close();
            }
            httpClient.close();
        }

    }
```

### 3.3 普通无参POST请求

```java
//普通的无参数POST请求：设置header来伪装浏览器请求
    @Test
    public void doPost() throws Exception{
        // 创建HttpClient对象
        CloseableHttpClient httpClient = HttpClients.createDefault();
        // 创建Http Post请求
        HttpPost httpPost = new HttpPost("http://www.baidu.com");
        // 伪装浏览器请求
        //httpPost.setHeader("User-Agent", "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36");
        CloseableHttpResponse response = null;
        try{
            // 执行http post请求
            response = httpClient.execute(httpPost);
            if(response.getStatusLine().getStatusCode()==200){
                String content = EntityUtils.toString(response.getEntity(),"UTF-8");
                System.out.println(content);
                System.out.println("内容长度："+content.length());
            }else{
                System.out.println("请求失败");
            }
        }finally {
            if(response!=null){
                response.close();
            }
            httpClient.close();
        }
    }
```

### 3.4 执行带参POST请求

```java
// 执行带参数的POST请求：模拟开源中国检索java，并伪装浏览器请求
    @Test
    public void doPostParam() throws Exception{
        CloseableHttpClient httpClient = HttpClients.createDefault();
        HttpPost httpPost = new HttpPost("http://www.oschina.net/search");
        // 设置两个post参数，一个是scope,一个是q
        List<NameValuePair> parameters = new ArrayList<NameValuePair>(0);
        parameters.add(new BasicNameValuePair("scope","project"));
        parameters.add(new BasicNameValuePair("q","java"));
        // 构造一个form表单式的实体
        UrlEncodedFormEntity formEntity = new UrlEncodedFormEntity(parameters);
        // 将请求实体设置到HttpPost对象中
        httpPost.setEntity(formEntity);
        // 伪装浏览器
        httpPost.setHeader("User-Agent", "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/56.0.2924.87 Safari/537.36");
        CloseableHttpResponse response = null;
        try{
            response = httpClient.execute(httpPost);
            if(response.getStatusLine().getStatusCode()==200){
                String content = EntityUtils.toString(response.getEntity(),"UTF-8");
                System.out.println(content);
                System.out.println("内容长度："+content.length());
            }
        }finally {
            if(response!=null){
                response.close();
            }
            httpClient.close();
        }
    }
```



