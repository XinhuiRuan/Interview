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

十九. click在ios上有300ms延迟，原因及如何解决？
(1)粗暴型，禁用缩放
  <meta name="viewport" content="width=device-width, user-scalable=no"> 

(2)利用FastClick，其原理是：
  检测到touchend事件后，立刻出发模拟click事件，并且把浏览器300毫秒之后真正出发的事件给阻断掉
  
详细介绍：https://www.cnblogs.com/zhaodahai/p/6831165.html


二十. addEventListener参数
addEventListener(event, function, useCapture)
其中，event指定事件名；function指定要事件触发时执行的函数；useCapture指定事件是否在捕获或冒泡阶段执行。

JavaScript事件监听以及addEventListener参数分析：https://www.cnblogs.com/strivers/p/7489272.html


二十一. iframe通信，同源和不同源两种情况，多少种方法
同源使用localStorage，但是不能跨域；
不同源采用iframe的postMessage实现不同源通信。

使用 iframe + postMessage 实现跨域通信：https://blog.csdn.net/tang_yi_/article/details/79401280
HTML5 postMessage 和 onmessage API 详细应用：https://www.cnblogs.com/sugar-tomato/p/4497108.html


二十二. 介绍知道的http返回的状态码 / HTTP状态码说说你知道的 / 讲讲304
100    Continue    继续。客户端应继续其请求
101    Switching Protocols    切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议

200    OK    请求成功。一般用于GET与POST请求

201    Created    已创建。成功请求并创建了新的资源

202    Accepted    已接受。已经接受请求，但未处理完成

203    Non-Authoritative Information    非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本

204    No Content    无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档

205    Reset Content    重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域

206    Partial Content    部分内容。服务器成功处理了部分GET请求

300    Multiple Choices    多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择

301    Moved Permanently    永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替

302    Found    临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI

303    See Other    查看其它地址。与301类似。使用GET和POST请求查看

304    Not Modified    未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源。
——— 如果客户端发送了一个带条件的GET 请求且该请求已被允许，而文档的内容（自上次访问以来或者根据请求的条件）并没有改变，则服务器应当返回这个304状态码。
HTTP 304状态码的详细讲解：https://blog.csdn.net/qq_39767955/article/details/81092779

305    Use Proxy    使用代理。所请求的资源必须通过代理访问

306    Unused    已经被废弃的HTTP状态码

307    Temporary Redirect    临时重定向。与302类似。使用GET请求重定向

400    Bad Request    客户端请求的语法错误，服务器无法理解

401    Unauthorized    请求要求用户的身份认证

402    Payment Required    保留，将来使用

403    Forbidden    服务器理解请求客户端的请求，但是拒绝执行此请求

404    Not Found    服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面

405    Method Not Allowed    客户端请求中的方法被禁止

406    Not Acceptable    服务器无法根据客户端请求的内容特性完成请求

407    Proxy Authentication Required    请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权

408    Request Time-out    服务器等待客户端发送的请求时间过长，超时

409    Conflict    服务器完成客户端的PUT请求是可能返回此代码，服务器处理请求时发生了冲突

410    Gone    客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置

411    Length Required    服务器无法处理客户端发送的不带Content-Length的请求信息

412    Precondition Failed    客户端请求信息的先决条件错误

413    Request Entity Too Large    由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息

414    Request-URI Too Large    请求的URI过长（URI通常为网址），服务器无法处理

415    Unsupported Media Type    服务器无法处理请求附带的媒体格式

416    Requested range not satisfiable    客户端请求的范围无效

417    Expectation Failed    服务器无法满足Expect的请求头信息

500    Internal Server Error    服务器内部错误，无法完成请求

501    Not Implemented    服务器不支持请求的功能，无法完成请求

502    Bad Gateway    作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应

503    Service Unavailable    由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中

504    Gateway Time-out    充当网关或代理的服务器，未及时从远端服务器获取请求

505    HTTP Version not supported    服务器不支持请求的HTTP协议的版本，无法完成处理

HTTP状态码五种总结大全：https://blog.csdn.net/Sunny_Future/article/details/81359794


二十三. http常用请求头
https://blog.csdn.net/qq_30553235/article/details/79282113


二十四. 强缓存和协商缓存 / 强缓存、协商缓存什么时候用哪个
缓存分为两种：强缓存和协商缓存，根据响应的header内容来决定。

              获取资源形式       状态码         发送请求到服务器

强缓存         从缓存取     200（from cache）   否，直接从缓存取

协商缓存       从缓存取     304（not modified） 是，通过服务器来告知缓存是否可用


强缓存相关字段有expires，cache-control。如果cache-control与expires同时存在的话，cache-control的优先级高于expires。

协商缓存相关字段有Last-Modified/If-Modified-Since，Etag/If-None-Match。

选择合适的缓存策略
  对于大部分的场景都可以使用强缓存配合协商缓存解决，但是在一些特殊的地方可能需要选择特殊的缓存策略：
  —— 对于某些不需要缓存的资源，可以使用 Cache-control: no-store ，表示该资源不需要缓存
  —— 对于频繁变动的资源，可以使用 Cache-Control: no-cache 并配合 ETag 使用，表示该资源已被缓存，但是每次都会发送请求询问资源是否更新。
  —— 对于代码文件来说，通常使用 Cache-Control: max-age=31536000 并配合策略缓存使用，然后对文件进行指纹处理，一旦文件名变动就会立刻下载新的文件。

彻底弄懂强缓存与协商缓存：https://www.jianshu.com/p/9c95db596df5
强缓存和协商缓存区别和过程：https://www.jianshu.com/p/f6525b0f8813
http协商缓存VS强缓存（这篇很详细，解惑版）：https://www.cnblogs.com/wonyun/p/5524617.html


二十五. 前端优化
1. 异步加载
  i. 方式：动态脚本加载、defer、async （js文件一般放在页面底部，若放在head里一般要在script标签上加 async 或者 defer 进行异步加载）
  ii. 区别：defer是在html解析完毕才执行,如果有多个则按加载顺序执行；async是加载完毕后立即执行,如果是多个,执行顺序与加载顺序无关。
    这里defer和async的区别超详细：https://segmentfault.com/q/1010000000640869

2. 浏览器缓存（详细看强缓存和协商缓存部分的题目）
  缓存对于前端性能优化来说是个很重要的点，良好的缓存策略可以降低资源的重复加载提高网页的整体加载速度。
  通常浏览器缓存策略分为两种：强缓存和协商缓存。
  
  i. 强缓存
  是指在时间之内不会询问服务器是否需要缓存。
    1. Expires(过期时间) Expries:Sun Jun 16 2019 23:55:21 GMT(服务器时间)
    2. Cache-Control(相对时间)

  ii.协商缓存
  如果本地有缓存,则需要向服务器询问是否需要使用本地缓存。
    1. Last-Modified / if-Modified-Since
    2. Etag / If-None-Match

3. 预加载
  在开发中，可能会遇到这样的情况：有些资源不需要马上用到，但是希望尽早获取，这时候就可以使用预加载。
  预加载其实是声明式的 fetch ，强制浏览器请求资源，并且不会阻塞 onload 事件，可以使用以下代码开启预加载
  <link rel="preload" href="http://example.com">
  预加载可以一定程度上降低首屏的加载时间，因为可以将一些不影响首屏但重要的文件延后加载，唯一缺点就是兼容性不好。

4. 预渲染
  可以通过预渲染将下载的文件预先在后台渲染，可以使用以下代码开启预渲染
  <link rel="prerender" href="http://example.com"> 
  预渲染虽然可以提高页面的加载速度，但是要确保该页面百分百会被用户在之后打开，否则就白白浪费资源去渲染

5. CDN
  CDN 的原理是尽可能的在各个地方分布机房缓存数据，这样即使我们的根服务器远在国外，在国内的用户也可以通过国内的机房迅速加载资源。
  因此，我们可以将静态资源尽量使用 CDN 加载，由于浏览器对于单个域名有并发请求上限，可以考虑使用多个 CDN 域名。并且对于 CDN 加载静态资源需要注意 CDN 
  域名要与主站不同，否则每次请求都会带上主站的 Cookie，平白消耗流量。
  
6. DNS 预解析
  DNS 解析也是需要时间的，可以通过预解析的方式来预先获得域名所对应的 IP。
  <meta http-equiv='x-dns-prefetch-control' content='on'>
  <link rel="dns-prefetch" href="//yuchengkai.cn">
  在https协议中默认a标签不会开启预解析,因此需要手动设置meta
  
7. 节流
  考虑一个场景，滚动事件中会发起网络请求，但是我们并不希望用户在滚动过程中一直发起请求，而是隔一段时间发起一次，对于这种情况我们就可以使用节流。
理解了节流的用途，我们就来实现下这个函数

// func是用户传入需要防抖的函数
// wait是等待时间
const throttle = (func, wait = 50) => {
  // 上一次执行该函数的时间
  let lastTime = 0
  return function(...args) {
    // 当前时间
    let now = +new Date()
    // 将当前时间和上一次执行函数时间对比
    // 如果差值大于设置的等待时间就执行函数
    if (now - lastTime > wait) {
      lastTime = now
      func.apply(this, args)
    }
  }
}

setInterval(
  throttle(() => {
    console.log(1)
  }, 500),
  1
)

8. 防抖
  考虑一个场景，有一个按钮点击会触发网络请求，但是我们并不希望每次点击都发起网络请求，而是当用户点击按钮一段时间后没有再次点击的情况才去发起网络请求，对于这种情况我们就可以使用防抖。
理解了防抖的用途，我们就来实现下这个函数

// func是用户传入需要防抖的函数
// wait是等待时间
const debounce = (func, wait = 50) => {
  // 缓存一个定时器id
  let timer = 0
  // 这里返回的函数是每次用户实际调用的防抖函数
  // 如果已经设定过定时器了就清空上一次的定时器
  // 开始一个新的定时器，延迟执行用户传入的方法
  return function(...args) {
    if (timer) clearTimeout(timer)
    timer = setTimeout(() => {
      func.apply(this, args)
    }, wait)
  }
}

9. 懒执行
懒执行就是将某些逻辑延迟到使用时再计算。该技术可以用于首屏优化，对于某些耗时逻辑并不需要在首屏就使用的，就可以使用懒执行。懒执行需要唤醒，一般可以通过定时器或者事件的调用来唤醒。

10. 懒加载
懒加载就是将不关键的资源延后加载。
懒加载的原理就是只加载自定义区域（通常是可视区域，但也可以是即将进入可视区域）内需要加载的东西。对于图片来说，先设置图片标签的 src 属性为一张占位图，将真实的图片资源放入一个自定义属性中，当进入自定义区域时，就将自定义属性替换为 src 属性，这样图片就会去下载资源，实现了图片懒加载。
懒加载不仅可以用于图片，也可以使用在别的资源上。比如进入可视区域才开始播放视频等等。

11. 图片优化
i. 计算图片大小
对于一张 100 * 100 像素的图片来说，图像上有 10000 个像素点，如果每个像素的值是 RGBA 存储的话，那么也就是说每个像素有 4 个通道，每个通道 1 个字节（8 位 = 1个字节），所以该图片大小大概为 39KB（10000 * 1 * 4 / 1024）。
（为什么每个像素是RGBA存储为4个字节？一个像素占多大内存多少字节
  1TB=1024GB 1GB=1024MB 1MB=1024KB 1KB=1024B 1B=8b
  一个像素占多大内存多少字节 取决于需要存储一个像素的多少信息，以及是否采用了压缩技术。
  如果是非黑即白的二值图像，不压缩的情况下一个像素只需要1个bit。
  如果是256种状态的灰度图像，不压缩的情况下一个像素需要8bit（1字节，256种状态）。
  如果用256种状态标识屏幕上某种颜色的灰度，而屏幕采用三基色红绿蓝（RGB），不压缩的情况下一个像素需要占用24bit（3字节），这个就是常说的24位真彩色。
  -> 如果用256种状态标识屏幕上某种颜色的灰度，而屏幕采用三基色RGBA，不压缩的情况下一个像素需要占用32bit（4字节）
）
但是在实际项目中，一张图片可能并不需要使用那么多颜色去显示，我们可以通过减少每个像素的调色板来相应缩小图片的大小。
了解了如何计算图片大小的知识，那么对于如何优化图片，想必大家已经有 2 个思路了：
  减少像素点
  减少每个像素点能够显示的颜色

ii. 图片加载优化
  1. 不用图片。很多时候会使用到很多修饰类图片，其实这类修饰图片完全可以用 CSS 去代替。
  2. 对于移动端来说，屏幕宽度就那么点，完全没有必要去加载原图浪费带宽。一般图片都用 CDN 加载，可以计算出适配屏幕的宽度，然后去请求相应裁剪好的图片。
  3. 小图使用 base64 格式
  4. 将多个图标文件整合到一张图片中（雪碧图）
  5. 选择正确的图片格式：
    5.1 对于能够显示 WebP 格式的浏览器尽量使用 WebP 格式。因为 WebP 格式具有更好的图像数据压缩算法，能带来更小的图片体积，而且拥有肉眼识别无差异的
        图像质量，缺点就是兼容性并不好
    5.2 小图使用 PNG，其实对于大部分图标这类图片，完全可以使用 SVG 代替
    5.3 照片使用 JPEG
    
12. 其他文件优化
  i. CSS 文件放在 head 中
  ii. 服务端开启文件压缩功能
  iii. 将 script 标签放在 body 底部，因为 JS 文件执行会阻塞渲染。当然也可以把 script 标签放在任意位置然后加上 defer ，表示该文件会并行下载，但是会 放到 HTML 解析完成后顺序执行。对于没有任何依赖的 JS 文件可以加上 async ，表示加载和渲染后续文档元素的过程将和 JS 文件的加载与执行并行无序进行。
  iv. 执行 JS 代码过长会卡住渲染，对于需要很多时间计算的代码可以考虑使用 Webworker。Webworker 可以让我们另开一个线程执行脚本而不影响渲染。

面试--关于前端性能优化篇：https://blog.csdn.net/qq_37674616/article/details/86490686
前端面试题（六）前端性能优化篇：https://www.jianshu.com/p/3db597e3928e

二十六. GET和POST的区别


二十七. 301和302的区别


二十八.  HTTP支持的方法
