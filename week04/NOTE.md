一、浏览器工作原理：
1.用户输入 地址栏会判断输入的关键字是搜索内容还是请求URL，如果是搜索内容使用默认搜索引擎合成带有搜索关键字的URL， 如果是URL，地址栏会根据规则加上协议合成完整的URL

2.URL请求过程 浏览器进程通过进程间的通讯（IPC）把URL请求发送至网络进程，网络进程接收到URL请求后，发起真正的URL请求流程： 2.1. 网络进程查找本地缓存是否缓存了该资源，如果有缓存，直接返回资源给浏览器进程；如果没有，直接进入网络请求流程；请求第一步进行DNS解析，获取IP地址； 2.2. 利用IP地址和服务器建立TCP连接，建立连接后，浏览器构建请求行，请求头等信息； 2.3. 服务器接收到请求信息后，根据请求信息生成相应数据，并发给网络进程，等网络进程接收相应行和相应头，就开始解析相应头的内容； 2.4. 网络进程解析相应头，发现状态码是301或者是302，说明浏览器需要重定向到其他URL，网络进程从相应头的Location字段里面读取重定向的地址，在发起新的HTTP或者HTTPS请求。 如果是状态码是200，标识浏览器可以技术处理该请求； 2.5. 相应数据类型处理；相应头中Content-Type的值告诉浏览器服务器返回的响应体数据的类型； Content-Type = text/html 告诉浏览器，服务返回的是HTML格式 Content-Type = application/octet-stream 表示字节流类型，通常情况下，浏览器会按照下载类型来处理请求

3.准备渲染进程，新打开一个页面创建一个渲染进程，如果从一个页面打开了一个新页面，新页面和当前页面属于同一站点，那么新页面会复用父页面的渲染进程；

4.提交文档，浏览器进程将网络进程中接收到的HTML数据提交给渲染进程; 4.1. 浏览器进程接收到网络进程的响应图数据后，想渲染进程发起‘提交文档’的消息； 4.2. 渲染进程接收到‘提交文档’的消息后，和网络进程建立传输数据的‘管道’； 4.3. 文档数据传输完成，渲染进程返回‘确认提交’的消息给浏览器进程； 4.4. 浏览器进程收到‘确认提交’的消息后，更新界面状态，如：安全状态，地址栏URL、前进后退的历史状态，并更新Web页面；

5.渲染阶段；渲染进程开始页面解析和子资源加载；
二、有限状态机
有限状态机处理字符串；
	每一个状态都是一个机器，所有的机器接受的输入时一致的，状态机的每一个机器本身没有状态，是纯函数没有副作用；

	两种状态：
		* Moore:每个机器都有确定的下一个状态；
		* Mealy:每个机器根据输入决定下一个状态；
Http
    request
        GET / HTTP/1.1  // 第一行被称作 Request Line，它分为三个部分，HTTP Method，也就是请求的“方法”，请求的路径和请求的协议和版本。
        Host: time.geekbang.org // Request Header

        field1=aaa&code=x%3D1 // Body
    response
        HTTP/1.1 301 Moved Permanently // 第一行被称作 Status Line，它也分为三个部分，协议和版本、状态码和状态文本。
        // Response Header
        Date: Fri, 25 Jan 2019 13:28:12 GMT
        Content-Type: text/html
        Content-Length: 182
        Connection: keep-alive
        Location: https://time.geekbang.org/
        Strict-Transport-Security: max-age=15768000

        // Body
        26
        <html>
        <head><title>301 Moved Permanently</title></head>
        <body bgcolor="white">
        <center><h1>301 Moved Permanently</h1></center>
        <hr><center>openresty</center>
        </body>
        </html>
        0