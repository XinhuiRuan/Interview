# Interview
The interview questions of Front-end

一. 说一下 http 和 https

1. http和https的基本概念
http: 超文本传输协议，是互联网上应用最为广泛的一种网络协议，是一个客户端和服务器端请求和应答的标准（TCP），用于从WWW服务器传输超文本到本地浏览器的传输协议，它可以使浏览器更加高效，使网络传输减少。

https: 是以安全为目标的HTTP通道，简单讲是HTTP的安全版，即HTTP下加入SSL层，HTTPS的安全基础是SSL，因此加密的详细内容就需要SSL。https的SSL加密是在传输层实现的。

https协议的主要作用是：建立一个信息安全通道，来确保数组的传输，确保网站的真实性。

2. http和https的区别？
http传输的数据都是未加密的，也就是明文的，网景公司设置了SSL协议来对http协议传输的数据进行加密处理，简单来说https协议是由http和ssl协议构建的可进行加密传输和身份认证的网络协议，比http协议的安全性更高。
主要的区别如下：
  Https协议需要ca证书，费用较高。
  http是超文本传输协议，信息是明文传输，https则是具有安全性的ssl加密传输协议。
  使用不同的链接方式，端口也不同，一般而言，http协议的端口为80，https的端口为443
  http的连接很简单，是无状态的；HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全。

3. https协议的工作原理
客户端在使用HTTPS方式与Web服务器通信时有以下几个步骤：
  客户使用https url访问服务器，则要求web 服务器建立ssl链接。
  web服务器接收到客户端的请求之后，会将网站的证书（证书中包含了公钥），返回或者说传输给客户端。
  客户端和web服务器端开始协商SSL链接的安全等级，也就是加密等级。
  客户端浏览器通过双方协商一致的安全等级，建立会话密钥，然后通过网站的公钥来加密会话密钥，并传送给网站。
  web服务器通过自己的私钥解密出会话密钥。
  web服务器通过会话密钥加密与客户端之间的通信。
  
4. https协议的优点
使用HTTPS协议可认证用户和服务器，确保数据发送到正确的客户机和服务器；
HTTPS协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，要比http协议安全，可防止数据在传输过程中不被窃取、改变，确保数据的完整性。
HTTPS是现行架构下最安全的解决方案，虽然不是绝对安全，但它大幅增加了中间人攻击的成本。
谷歌曾在2014年8月份调整搜索引擎算法，并称“比起同等HTTP网站，采用HTTPS加密的网站在搜索结果中的排名将会更高”。

5. https协议的缺点
https握手阶段比较费时，会使页面加载时间延长50%，增加10%~20%的耗电。
https缓存不如http高效，会增加数据开销。
SSL证书也需要钱，功能越强大的证书费用越高。
SSL证书需要绑定IP，不能再同一个ip上绑定多个域名，ipv4资源支持不了这种消耗。


二. TCP三次握手，一句话概括

三次握手可以简化为：客户端发起请求连接服务端确认，服务端也发起连接客户端确认。
每次握手的作用：
  第一次握手：服务端只可以确认 -> 自己可以接受客户端发送的报文段
  第二次握手：1. 客户端可以确认 -> 服务端收到了自己发送的报文段，2. 客户端并且可以确认 -> 自己可以接受服务端发送的报文段
  第三次握手：服务端可以确认 -> 客户端收到了自己发送的报文段
  
详细资源：https://www.cnblogs.com/Paul-watermelon/p/11141420.html  
关于第三次握手为什么客户端还要发送 Seq = X + 1 的解释：https://zhidao.baidu.com/question/1833591122346527500.html
因为 Seq是数据包本身的序列号；ack是期望对方继续发送的那个数据包的序列号。


三. TCP 和 UDP 的区别

1、连接方面区别
TCP面向连接（如打电话要先拨号建立连接）。
UDP是无连接的，即发送数据之前不需要建立连接。

2、安全方面的区别
TCP提供可靠的服务，通过TCP连接传送的数据，无差错，不丢失，不重复，且按序到达。适合大数据量的交换。
UDP尽最大努力交付，即不保证可靠交付。

3、传输效率的区别
TCP传输效率相对较低。
UDP传输效率高，适用于对高速传输和实时性有较高的通信或广播通信。（对实时的应用比如IP电话和视频会议等）

4、连接对象数量的区别
TCP连接只能是点到点、一对一的。
UDP支持一对一，一对多，多对一和多对多的交互通信。

5、头部开销的区别
TCP的首部较大，至少为20字节。
UDP只有8字节。

详细资源：一文搞懂TCP与UDP的区别 https://www.cnblogs.com/fundebug/p/differences-of-tcp-and-udp.html


四. WebSocket的实现和应用

1. 什么是WebSocket?
WebSocket是HTML5中的协议，支持持久连续，http协议不支持持久性连接。Http1.0和HTTP1.1都不支持持久性的链接，HTTP1.1中的keep-alive，将多个http请求合并为1个。

2. WebSocket是什么样的协议，具体有什么优点？
HTTP的生命周期通过Request来界定，也就是Request一个Response，那么在Http1.0协议中，这次Http请求就结束了。
在Http1.1中进行了改进，是的有一个connection：Keep-alive，也就是说，在一个Http连接中，可以发送多个Request，接收多个Response。但是必须记住，在Http中一个Request只能对应有一个Response，而且这个Response是被动的，不能主动发起。
WebSocket是基于Http协议的，或者说借用了Http协议来完成一部分握手，在握手阶段与Http是相同的。我们来看一个websocket握手协议的实现，基本是2个属性，upgrade，connection。

基本请求如下：
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
Origin: http://example.com

多了下面2个属性：
Upgrade:webSocket
Connection:Upgrade
告诉服务器发送的是Websocket协议，快点帮我找到对应的助理处理，不是那个老土的HTTP

Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
这3个属性的解释详见知乎版

详细资源：WebSocket介绍  https://www.cnblogs.com/qdhxhz/p/8467715.html
                知乎版  https://www.zhihu.com/question/20215561


五. 说一下web Quality（无障碍）

能够被残障人士使用的网站才能称得上一个易用的（易访问的）网站。
残障人士指的是那些带有残疾或者身体不健康的用户。

使用alt属性：
<img src="person.jpg"  alt="this is a person"/>

有时候浏览器会无法显示图像。具体的原因有：
—— 用户关闭了图像显示
—— 浏览器是不支持图形显示的迷你浏览器
—— 浏览器是语音浏览器（供盲人和弱视人群使用）
如果您使用了 alt 属性，那么浏览器至少可以显示或读出有关图像的描述。

六. 几个很实用的BOM属性对象方法

Bom是浏览器对象模型。

1. location对象
与当前窗口中加载的文档有关的信息，还可以将URL解析为独立的片段。。
location.href -- 返回或设置当前文档的URL
location.search -- 返回URL中的查询字符串部分。例如 http://www.dreamdu.com/dreamd.php?id=5&name=dreamdu 返回包括(?)后面的内容
location.hash -- 返回URL#后面的内容，如果没有#，返回空
location.host -- 返回URL中的域名部分，例如www.dreamdu.com
location.hostname -- 返回URL中的主域名部分，例如dreamdu.com
location.pathname -- 返回URL的域名后的部分。例如 http://www.dreamdu.com/xhtml/ 返回/xhtml/
location.port -- 返回URL中的端口部分。例如 http://www.dreamdu.com:8080/xhtml/ 返回8080
location.protocol -- 返回URL中的协议部分。例如 http://www.dreamdu.com:8080/xhtml/ 返回(//)前面的内容 http:
location.assign -- 设置当前文档的URL
location.replace() -- 设置当前文档的URL，并且在history对象的地址列表中移除这个URL，location.replace(url);
location.reload() -- 重载当前页面

2. history对象
保存着用户上网的历史记录。
history.go() -- 前进或后退指定的页面数 history.go(num);
history.back() -- 后退一页
history.forward() -- 前进一页

3. Navigator对象
识别和检测显示网页的浏览器类型
navigator.userAgent -- 返回用户代理头的字符串表示(就是包括浏览器版本信息等的字符串)
navigator.cookieEnabled -- 返回浏览器是否支持(启用)cookie


六. 说一下HTML5 drag api
dragstart：事件主体 -> 被拖放元素，在开始拖放时触发。
darg：事件主体 -> 被拖放元素，在拖放过程中触发。
dragenter：事件主体 -> 拖放过程中经过的元素，在被拖放元素进入本元素的范围内时触发。
dragover：事件主体 -> 拖放过程中经过的元素，在被拖放元素在本元素的范围内移动时触发。
dragleave：事件主体 -> 拖放过程中经过的元素，在被拖放元素离开本元素的范围内时触发。
drop：事件主体 -> 目标元素，有其他元素被拖放到了本元素中时触发。
dragend：事件主体 -> 被拖放元素，在整个拖放操作结束时触发


七. 说一下http2.0
首先补充一下，http和https的区别，相比于http,https是基于ssl加密的http协议。

简要概括：http2.0是基于1999年发布的http1.0之后的首次更新。
1. 提升访问速度（可以对于，请求资源所需时间更少，访问速度更快，相比http1.0）
2. 允许多路复用：多路复用允许同时通过单一的HTTP/2连接发送多重请求-响应信息。改善了：在http1.1中，浏览器客户端在同一时间，针对同一域名下的请求有一定
  数量限制（连接数量），超过限制会被阻塞。
3. 二进制分帧：HTTP2.0会将所有的传输信息分割为更小的信息或者帧，并对他们进行二进制编码。
4. 使用报头压缩，HTTP2.0降低了开销。
5. HTTP2.0让服务器可以将响应主动“推送”到客户端缓存中

详细资源：https://blog.csdn.net/N1314N/article/details/89406875


八. 补充400和401、403状态码
4XX 的响应结果表明客户端是发生错误的原因所在。

(1)400状态码（bad request）：请求无效，表示请求报文中存在语法错误。
产生原因：
  1. 前端提交数据的字段名称和字段类型与后台的实体没有保持一致
  2. 前端提交到后台的数据应该是json字符串类型，但是前端没有将对象JSON.stringify转化成字符串。
解决方法：
  1. 对照字段的名称，保持一致性
  2. 将obj对象通过JSON.stringify实现序列化
  
(2)401状态码（unauthorized）：表示发送的请求需要有通过HTTP认证的认证信息

(3)403状态码（forbidden）：服务器已经得到请求，但是资源的访问被服务器拒绝


九. fetch发送两次请求的原因
fetch发送post请求的时候，总是发送2次，第一次状态码是204（No Content），第二次才成功？

比方说发送post请求“/createSth”，在控制台能看到两个url一致的请求：
  —— 第一个无body、无响应、以OPTIONS方式发送；
  —— 第二个就是正常的有参数body、有response、post方式提交的请求。

原因很简单，因为你用fetch的post请求的时候，导致fetch第一次使用Options请求发起一个预检的跨域请求（preflight request），从而获知服务端是否允许该跨域请求。如果服务器支持，则在第二次中发送真正的请求。

相关资源：
  fetch的post方法发送两次请求的例子和解释：https://segmentfault.com/q/1010000008693779
  JS发送跨域Post请求出现两次请求的解决办法：https://blog.csdn.net/weixin_34314962/article/details/93723222
  如何使用 fetch api：https://www.jianshu.com/p/1b966c113f64?utm_source=oschina-app
  ajax和axios、fetch的区别：https://www.jianshu.com/p/8bc48f8fde75
  

十. Cookie、sessionStorage、localStorage 的区别
共同点：
  都是保存在浏览器端，并且是同源的
  
不同点：
  Cookie：cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递。而sessionStorage和localStorage不会自动把数据发 
          给服务器，仅在本地保存。cookie数据还有路径（path）的概念，可以限制cookie只属于某个路径下，存储的大小很小只有4K左右。 （重点：可以在浏览器
          和服务器端来回传递，存储容量小，只有大约4K左右）
  sessionStorage：仅在当前浏览器窗口关闭前有效，自然也就不可能持久保持，localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据； 
          cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。（重点：本身就是一个回话过程，关闭浏览器后消失，session为一个回话，当页
          面不同即使是同一页面打开两次，也被视为同一次回话）
  localStorage：localStorage 在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的。（重点：同源窗口都会共享，并且不会失效，不管窗口或者
          浏览器关闭与否都会始终生效）
          
补充说明一下cookie的作用：
  保存用户登录状态。例如将用户id存储于一个cookie内，这样当用户下次访问该页面时就不需要重新登录了，现在很多论坛和社区都提供这样的功能。cookie还可以设置过期时间，当超过时间期限后，cookie就会自动消失。因此，系统往往可以提示用户保持登录状态的时间：常见选项有一个月、三个 月、一年等。
  跟踪用户行为。例如一个天气预报网站，能够根据用户选择的地区显示当地的天气情况。如果每次都需要选择所在地是烦琐的，当利用了cookie后就会显得很人性化了，系统能够记住上一次访问的地区，当下次再打开该页面时，它就会自动显示上次用户所在地区的天气情况。因为一切都是在后台完成，所以这样的页面就像为某个用户所定制的一样，使用起来非常方便。
  定制页面。如果网站提供了换肤或更换布局的功能，那么可以使用cookie来记录用户的选项，例如：背景色、分辨率等。当用户下次访问时，仍然可以保存上一次访问的界面风格。
  
session,cookie,sessionStorage,localStorage详解： https://www.cnblogs.com/xufeimei/p/10143786.html
  
  
十一. 说一下 Web Worker
在HTML页面中，如果在执行脚本时，页面的状态是不可相应的，直到脚本执行完成后，页面才变成可相应。web worker是运行在后台的js，独立于其他脚本，不会影响页面你的性能。并且通过postMessage将结果回传到主线程。这样在进行复杂操作的时候，就不会阻塞主线程了。

如何创建web worker：
  1. 检测浏览器对于web worker的支持性
  2. 创建web worker文件（js，回传函数等）
  3. 创建web worker对象
  
由于Web Worker创建的线程是受限的子线程，所以会有一些使用限制：
  1. Web Worker无法访问DOM节点；
  2. Web Worker无法访问全局变量或是全局函数；
  3. Web Worker无法调用alert()或者confirm之类的函数；
  4. Web Worker无法访问window、document之类的浏览器全局变量；
不过Web Worker中的Javascript依然可以使用setTimeout(),setInterval()之类的函数，也可以使用XMLHttpRequest对象来做Ajax通信。
目前所有主流浏览器均支持 web worker，除了 Internet Explorer。
  
web worker 详细介绍：https://blog.csdn.net/ithanmang/article/details/82622420


十二. 对HTML语义化标签的理解
HTML5语义化标签是指正确的标签包含了正确的内容，结构良好，便于阅读，比如nav表示导航条，类似的还有article、header、footer等等标签。


十三. iframe是什么？有什么缺点？
定义：iframe元素会创建包含另一个文档的内联框架，说白了就是用来在当前HTML页面中嵌入另一个文档的。
提示：可以将提示文字放在<iframe></iframe>之间，来提示某些不支持iframe的浏览器。

优点：
  1. iframe能够原封不动的把嵌入的网页展现出来。
  2. 如果有多个网页引用iframe，那么你只需要修改iframe的内容，就可以实现调用的每一个页面内容的更改，方便快捷。
  3. 网页如果为了统一风格，头部和版本都是一样的，就可以写成一个页面，用iframe来嵌套，可以增加代码的可重用。
  4. 如果遇到加载缓慢的第三方内容如图标和广告，这些问题可以由iframe来解决。

缺点：
  1. iframe会阻塞主页面的onload事件；
  2. iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载，会产生很多页面，不容易管理。
  3. iframe框架结构有时会让人感到迷惑，如果框架个数多的话，可能会出现上下、左右滚动条，会分散访问者的注意力，用户体验度差。
  4. 代码复杂，无法被一些搜索引擎索引到，这一点很关键，现在的搜索引擎爬虫还不能很好的处理iframe中的内容，所以使用iframe会不利于搜索引擎优化（SEO）。
  5. 很多的移动设备无法完全显示框架，设备兼容性差。
  6. iframe框架页面会增加服务器的http请求，对于大型网站是不可取的。

现在基本上都是用Ajax来代替iframe，所以iframe已经渐渐的退出了前端开发。
如果需要使用iframe，最好是通过javascript动态给iframe添加src属性值，这样可以绕开以上一些问题。

iframe详解： https://www.jianshu.com/p/d67b15802a70


十四. Doctype作用？严格模式与混杂模式如何区分？它们有何意义？
<!DOCTYPE>声明叫做文件类型定义（DTD），声明的作用为了告诉浏览器该文件的类型。让浏览器解析器知道应该用哪个规范来解析文档。<!DOCTYPE>声明必须在 HTML 文档的第一行，这并不是一个 HTML 标签。

严格模式：又称标准模式，是指浏览器按照 W3C 标准解析代码。
混杂模式：又称怪异模式或兼容模式，是指浏览器用自己的方式解析代码。

如何区分：浏览器解析时到底使用严格模式还是混杂模式，与网页中的 DTD 直接相关。
  1、如果文档包含严格的 DOCTYPE ，那么它一般以严格模式呈现。（严格 DTD —— 严格模式） 
  2、包含过渡 DTD 和 URI 的 DOCTYPE ，也以严格模式呈现，但有过渡 DTD 而没有 URI （统一资源标识符，就是声明最后的地址）会导致页面以混杂模式呈现。（有 URI 的过渡 DTD —— 严格模式；没有 URI 的过渡 DTD —— 混杂模式） 
  3、DOCTYPE 不存在或形式不正确会导致文档以混杂模式呈现。（DTD不存在或者格式不正确 —— 混杂模式）
  4、HTML5 没有 DTD ，因此也就没有严格模式与混杂模式的区别，HTML5 有相对宽松的语法，实现时，已经尽可能大的实现了向后兼容。（ HTML5 没有严格和混杂之分）

意义：严格模式与混杂模式存在的意义与其来源密切相关，如果说只存在严格模式，那么许多旧网站必然受到影响，如果只存在混杂模式，那么会回到当时浏览器大战时的混乱，每个浏览器都有自己的解析模式。

详解：https://www.cnblogs.com/wuqiutong/p/5986191.html


十五. Cookie如何防范XSS攻击
Cross-Site Scripting（跨站脚本攻击）简称 XSS，是一种代码注入攻击。攻击者通过在目标网站上注入恶意脚本，使之在用户的浏览器上运行。利用这些恶意脚本，攻击者可获取用户的敏感信息如 Cookie、SessionID 等，进而危害数据安全。

为了和 CSS 区分，这里把攻击的第一个字母改成了 X，于是叫做 XSS。

XSS 的本质是：恶意代码未经过滤，与网站正常的代码混在一起；浏览器无法分辨哪些脚本是可信的，导致恶意脚本被执行。

而由于直接在用户的终端执行，恶意代码能够直接获取用户的信息，或者利用这些信息冒充用户向网站发起攻击者定义的请求。

在部分情况下，由于输入的限制，注入的恶意脚本比较短。但可以通过引入外部的脚本，并由浏览器执行，来完成比较复杂的攻击策略。

Cookie防范XSS攻击，需要在HTTP头部配上，set-cookie：
  1. httponly-。这个属性可以防止XSS,它会禁止javascript脚本来访问cookie。
  2. secure - 这个属性告诉浏览器仅在请求为https的时候发送cookie。
结果应该是这样的：Set-Cookie=<cookie-value>.....
  
前端安全系列（一）：如何防止XSS攻击？：https://segmentfault.com/a/1190000016551188#articleHeader11


十六. Cookie和Session的区别
cookie机制采用的是在客户端保持状态的方案，而session机制采用的是在服务器端保持状态的方案。同时我们也看到，

由于采用服务器端保持状态的方案在客户端也需要保存一个标识，所以session机制可能需要借助于cookie机制来达到保存标识的目的

cookie不是很安全，别人可以分析存放在本地的cookie并进行cookie欺骗，考虑到安全应当使用session

session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用cookie

单个cookie保存的数据不能超过4k,很多浏览器都限制一个站点最多保存20个cookie。

Cookie,Session和Token机制和区别：https://www.jianshu.com/p/013f810cdb75


十七. 一句话概括RESTFUL
URL定位资源，用HTTP动词（GET,POST,DELETE,DETC）描述操作。

常用的资源操作类型，即http请求方式(括号中是对应的SQL命令)
  GET（SELECT）：从服务器取出资源（一项或多项）。
  POST（CREATE）：在服务器新建一个资源。
  PUT（UPDATE）：在服务器更新资源（客户端提供改变后的完整资源）。
  PATCH（UPDATE）：在服务器更新资源（客户端提供改变的属性）。
  DELETE（DELETE）：从服务器删除资源。

REST以及RESTful的理解：https://www.jianshu.com/p/0e0ed296d2a3
前端简单理解RESTful：https://blog.csdn.net/meishuixingdeququ/article/details/77478217

十八. 讲讲viewport和移动端布局
响应式布局的常用解决方案对比(媒体查询、百分比、rem和vw/vh）：https://github.com/forthealllight/blog/issues/13
