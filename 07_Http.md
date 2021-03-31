## 网络
- http1.1与http2.0的区别
### http幂等性
HTTP方法的幂等性是指一次和多次请求某一个资源应该具有同样的副作用。
### TCP与UDP的区别
- TCP面向连接的，UDP面向报文的
- TCP保证数据正确性，UDP可能丢包（不安全）
- TCP基于流模式，UDP数据报模式
- TCP保证数据顺序，UDP不保证 
#### TCP  
TCP是面向连接的协议，在收发数据前，必须和对方建立可靠的连接。  
1. ACK 是TCP报头的控制位之一，对数据进行确认。确认由目的端发出， 用它来告诉发送端这个序列号之前的数据段都收到了。 比如确认号为X，则表示前X-1个数据段都收到了，只有当ACK=1时,确认号才有效，当ACK=0时，确认号无效，这时会要求重传数据，保证数据的完整性。  
2. SYN 同步序列号，TCP建立连接时将这个位置1。  
3. FIN 发送端完成发送任务位，当TCP完成数据传输需要断开时,，提出断开连接的一方将这位置1。  
#### UDP（User Data Protocol，用户数据报协议）  
UPD是面向报文的。发送方的UDP对应用程序交下来的报文， 在添加首部后就向下交付给IP层。既不拆分，也不合并，而是保留这些报文的边界， 因此，应用程序需要选择合适的报文大小。  
UDP是一个非连接的协议，传输数据之前源端和终端不建立连接， 当它想传送时就简单地去抓取来自应用程序的数据，并尽可能快地把它扔到网络上。 在发送端，UDP传送数据的速度仅仅是受应用程序生成数据的速度、 计算机的能力和传输带宽的限制； 在接收端，UDP把每个消息段放在队列中，应用程序每次从队列中读一个消息段。
#### 应用层：
- 超文本传输协议（HTTP）
- 文件传输（TFTP简单文件传输协议），
- 远程登录（Telnet），提供远程访问其它主机功能, 它允许用户登录internet主机，并在这台主机上执行命令；
- 网络管理（SNMP简单网络管理协议），该协议提供了监控网络设备的方法， 以及配置管理,统计信息收集,性能管理及安全管理等；
- 域名系统（DNS），该系统用于在internet中将域名及其公共广播的网络节点转换成IP地址。
#### 网络层
1. Internet协议（IP）；
2. Internet控制信息协议（ICMP）；
3. 地址解析协议（ARP）；
4. 反向地址解析协议（RARP）

### http/0.9,http/1.0, http/1.0+, http1.1, http2/.0区别
- http/0.9：只应用于与老客户端的交互，只支持get方法
- http/1.0：添加了版本号、各种http首部、方法、对多媒体对象的处理。
- http/1.0+：持久的keep-alive连接、虚拟主机支持，代理连接支持，但是都是非官方的事实标准。 
- http/1.1：重点关注校正HTTP设计中的结构性缺陷，明确语义，引入重要的性能措施，并删除一些不好的特性。
- http/2.0：重点关注性能的大幅优化，以及更强大的服务逻辑远程执行框架。将协议模块化为三成（报文传输层、远程调用层、web应用层）
### 有没有了解http2.0，websocket, https,说下你的理解以及你所了解的特性
- http协议，说下200和304的理解和区别
- XSS是什么？攻击原理？怎么预防？（1.转义2.DOM解析白名单3.第三方库4.CSP）
### 从url输入到页面展示到底发生了什么
1. 构建请求（请求头（方法、路径、协议版本）、空行、请求体（协议版本、状态、原因））
2. 先检查强缓存，如果命中直接使用，否则进入下一步。
3. 浏览器向DNS（域名系统）查找域名的IP地址（即是DNS解析）     
4. TCP三次握手  
5. 浏览器向web服务器发送一个HTTP请求  
6. 服务器处理请求  
7. 服务器返回一个HTTP响应  
8. 浏览器解析渲染页面  
9. TCP四次挥手  
### 浏览器实现缓存机制：
https://juejin.im/entry/5ad86c16f265da505a77dca4   
强制缓存、协商缓存   
浏览器的缓存机制也就是我们说的HTTP缓存机制，其机制是根据HTTP报文的缓存标识进行的.  
### 缓存
http权威指南第七章（170）  
缓存是请求资源的副本   
缓存的好处：  
缓存在宏观上可以分成两类：私有缓存和共享缓存。共享缓存就是那些能被各级代理缓存的缓存。私有缓存就是用户专享的，各级代理不能缓存的缓存。   
微观上可以分下面三类：浏览器缓存、代理服务器缓存、网关缓存、数据库缓存   
https://juejin.im/post/5a6c87c46fb9a01ca560b4d7  
#### 浏览器缓存
浏览器对于缓存的处理是根据第一次请求资源时返回的响应头来确定的。  
浏览器怎么确定一个资源该不该缓存，如何去缓存呢❓响应头！   
强缓存阶段(本地缓存：Expires,Cache-Control)，服务器响应的header中会用两个字段来表明——Expires和Cache-Control。   
Cache-Control有很多属性，不同的属性代表的意义也不同。  
private：客户端可以缓存  
public：客户端和代理服务器都可以缓存  
max-age=t：缓存内容将在t秒后失效  
no-cache：需要使用协商缓存来验证缓存数据  
no-store：所有内容都不会缓存。  
协商缓存阶段：是强制缓存失效后，浏览器携带缓存标识向服务器发起请求，由服务器根据缓存标识决定是否使用缓存的过程    
两种缓存方案（If-none-match/ETag,If-modified-since/last-modified）  
### http三次握手四次挥手
https://blog.csdn.net/xiaozhuxmen/article/details/51934706  
https://zhuanlan.zhihu.com/p/77334450?utm_source=wechat_session&utm_medium=social&utm_oi=667801099197747200  
https://www.jianshu.com/p/bd31d3b23725
tcp是面向连接的，可靠的，基于流的传输方式。
- 客户端发送一个带 SYN=1，Seq=X 的数据包到服务器端口（第一次握手，由浏览器发起，告诉服务器我要发送请求了）  
- 服务器收到SYN后，必须确认客户的 SYN，返回一个带 SYN=1， ACK=X+1， Seq=Y 的响应包以示传达确认信息（第二次握手，由服务器发起，告诉浏览器我准备接受了，你赶紧发送吧）
- 客户端收到服务器的SYN+ACK包，再回传一个带 ACK=Y+1， Seq=Z 的数据包，代表“握手结束”（第三次握手，由浏览器发送，告诉服务器，我马上就发了，准备接受吧）  
ACK ： TCP协议规定，只有ACK=1时有效，也规定连接建立后所有发送的报文的ACK必须为1
SYN(SYNchronization) ： 在连接建立时用来同步序号。当SYN=1而ACK=0时，表明这是一个连接请求报文。对方若同意建立连接，则应在响应报文中使SYN=1和ACK=1. 因此, SYN置1就表示这是一个连接请求或连接接受报文。
FIN （finis）：完，终结的意思， 用来释放一个连接。当 FIN = 1 时，表明此报文段的发送方的数据已经发送完毕，并要求释放连接。

#### 为啥需要三次握手
为了防止已失效的连接请求报文段突然又传送到了服务端，因而产生错误”。TCP 是可靠的传输，在建立连接时就应该经过两端的确认过程，如上面的流程，
只有在三次握手的情况下，客户端和服务端都经过了一次真正(SYN+ACK)的确认过程。这样的连接便认为是可信的。
#### 四次挥手
1. 客户端发送一个FIN，用来关闭客户端到服务器的数据传送，客户端进入FIN_WAIT_1状态。
2. 服务器收到FIN后，发送一个ACK给客户端，确认序号为收到序号+1（与SYN相同，一个FIN占用一个序号），服务器进入CLOSE_WAIT状态，而客户端进入FIN_WAIT2状态。
3. 服务器发送一个FIN，用来关闭服务器到客户端的数据传送，服务器进入LAST_ACK状态。
4. 客户端收到FIN后，客户端进入TIME_WAIT状态，接着发送一个ACK给服务器，确认序号为收到序号+1，服务器进入CLOSED状态，完成释放。  
#### 为什么是四次挥手
发送FIN的一方就是主动关闭(客户端)，而另一方则为被动关闭(服务器)。
当一方发送了FIN，则表示在这一方不再会有数据的发送。
其中当被动关闭方收到对方的FIN时，此时往往可能还有数据需要发送过去，因此无法立即发送FIN(也就是无法将FIN与ACK合并发送)，
而是在等待自己的数据发送完毕后再单独发送FIN，因此整个过程需要四次交互。

### 浏览器解析渲染页面
https://blog.csdn.net/weixin_41652128/article/details/86525551  
浏览器拿到响应文本HTML后，接下来介绍下浏览器渲染机制：   
浏览器解析渲染页面分为一下五个步骤：  
- 根据 HTML 解析出 DOM 树
- 根据 CSS 解析生成 CSS 规则树
- 结合 DOM 树和 CSS 规则树，生成渲染树
- 根据渲染树计算每一个节点的信息
- 根据计算好的信息绘制页面

### webSocket如何兼容低浏览器？
Adobe Flash Socket 、 ActiveX HTMLFile (IE) 、 基于 multipart 编码发送 XHR 、 基于长轮询的 XHR。
### WebSocket
https://www.cnblogs.com/nnngu/p/9347635.html  
#### 特点
- 服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话
- 建立在 TCP 协议之上，服务器端的实现比较容易。
- 与 HTTP 协议有着良好的兼容性。默认端口也是80和443，并且握手阶段采用 HTTP 协议，因此握手时不容易屏蔽，能通过各种 HTTP 代理服务器。
- 数据格式比较轻量，性能开销小，通信高效。
- 可以发送文本，也可以发送二进制数据。
- 没有同源限制，客户端可以与任意服务器通信。
- 协议标识符是ws（如果加密，则为wss），服务器网址就是 URL。
### WebSocket 是什么原理？为什么可以实现持久连接？
https://www.cnblogs.com/cangqinglang/p/8331120.html    
WebSocket是HTML5提供的在Web应用程序中客户端与服务器端之间进行的非HTTP的通信机制。使用WebSocket API可以在服务器与客户端之间建立一个非HTTP的双向连接。这个连接是实时的，也是永久的，除非被显示的关闭。   
首先Websocket是基于HTTP协议的，或者说借用了HTTP的协议来完成一部分握手。在握手阶段
```js

// 请求头
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==   // 浏览器随机生成Base64 encode, 验证是不是真的是 WebSocket。
Sec-WebSocket-Protocol: chat, superchat  // 用户定义的字符串，用来区分同 URL 下，不同的服务所需要的协议。
Sec-WebSocket-Version: 13 // 告诉服务器所使用的 WebSocket Draft （协议版本）
Origin: http://example.com
// 响应头
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
Sec-WebSocket-Protocol: chat
```

### post和get的区别
https://www.cnblogs.com/logsharing/p/8448446.html   
GET参数通过URL传递，POST放在Request body中。GET产生的URL地址可以被Bookmark，而POST不可以。GET在浏览器回退时是无害的，而POST会再次提交请求。      
GET产生一个TCP数据包；POST产生两个TCP数据包。对于GET方式的请求，浏览器会把http header和data一并发送出去，服务器响应200（返回数据；
而对于POST，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 ok（返回数据）。     
因为POST需要两步，时间上消耗的要多一点，看起来GET比POST更有效。因此Yahoo团队有推荐用GET替换POST来优化网站性能。但这是一个坑！跳入需谨慎。为什么？
1. GET与POST都有自己的语义，不能随便混用。  
2. 据研究，在网络环境好的情况下，发一次包的时间和发两次包的时间差别基本可以无视。而在网络环境差的情况下，两次包的TCP在验证数据包完整性上，有非常大的优点。  
3. 并不是所有浏览器都会在POST中发送两次包，Firefox就只发送一次。    
HTTP的底层是TCP/IP。所以GET和POST的底层也是TCP/IP，也就是说，GET/POST都是TCP链接。GET和POST能做的事情是一样一样的。你要给GET加上request body，给POST带上url参数，技术上是完全行的通的。    
数据传输长度取决于各个浏览器、服务器。  
业界不成文的规定是，（大多数）浏览器通常都会限制url长度在2K个字节，而（大多数）服务器最多处理64K大小的url。超过的部分，恕不处理。如果你用GET服务，在request body偷偷藏了数据，不同服务器的处理方式也是不同的，有些服务器会帮你卸货，读出数据，有些服务器直接忽略，所以，虽然GET可以带request body，也不能保证一定能被接收到哦。

### options请求
http://www.ruanyifeng.com/blog/2016/04/cors.html  
OPTIONS请求方法的主要用途有两个：
- 1、获取服务器支持的HTTP请求方法；
- 2、用来检查服务器的性能。例如：AJAX进行跨域请求时的预检，需要向另外一个域名的资源发送一个HTTP OPTIONS请求头，用以判断实际发送的请求是否安全（跨域）。
这是浏览器给我们加上的，后端并没有做任何操作。    
对那些可能对服务器数据产生副作用的 HTTP 请求方法（特别是 GET 以外的 HTTP 请求，或者搭配某些 MIME 类型的 POST 请求），浏览器必须首先使用 OPTIONS 方法发起一个预检请求（preflight request），从而获知服务端是否允许该跨域请求。服务器确认允许之后，才发起实际的 HTTP 请求。  
当请求满足下述任一条件时，即应首先发送预检请求（使用OPTIONS）：
- 1、使用了下面任一 HTTP 方法：PUT、DELETE、CONNECT、OPTIONS、TRACE、PATCH
- 2、人为设置了对 CORS 安全的首部字段集合之外的其他首部字段。该集合为： Accept、Accept-Language、Content-Language、Content-Type (but note the additional requirements below)、DPR、Downlink、Save-Data、Viewport-Width、Width
- 3、Content-Type 的值不属于下列之一: application/x-www-form-urlencoded、multipart/form-data、text/plain


