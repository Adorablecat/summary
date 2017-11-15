# summary
##知识点
一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？
分为4个步骤：
（1），当发送一个URL请求时，不管这个URL是Web页面的URL还是Web页面上每个资源的URL，浏览器都会开启一个线程来处理这个请求，同时在远程DNS服务器上启动一个DNS查询。这能使浏览器获得请求对应的IP地址。
（2）， 浏览器与远程`Web`服务器通过`TCP`三次握手协商来建立一个`TCP/IP`连接。该握手包括一个同步报文，一个同步-应答报文和一个应答报文，这三个报文在 浏览器和服务器之间传递。该握手首先由客户端尝试建立起通信，而后服务器应答并接受客户端的请求，最后由客户端发出该请求已经被接受的报文。
（3），一旦`TCP/IP`连接建立，浏览器会通过该连接向远程服务器发送`HTTP`的`GET`请求。远程服务器找到资源并使用HTTP响应返回该资源，值为200的HTTP响应状态表示一个正确的响应。
（4），此时，`Web`服务器提供资源服务，客户端开始下载资源。
请求返回后，便进入了我们关注的前端模块
简单来说，浏览器会解析HTML生成DOM Tree，其次会根据CSS生成CSS Rule Tree，而javascript又可以根据DOM API操作DOM

HTTP状态码
100  Continue  继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
200  OK   正常返回信息
201  Created  请求成功并且服务器创建了新的资源
202  Accepted  服务器已接受请求，但尚未处理
301  Moved Permanently  请求的网页已永久移动到新位置。
302 Found  临时性重定向。
303 See Other  临时性重定向，且总是使用 GET 请求新的 URI。
304  Not Modified  自从上次请求后，请求的网页未修改过。
400 Bad Request  服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求。
401 Unauthorized  请求未授权。
403 Forbidden  禁止访问。
404 Not Found  找不到如何与 URI 相匹配的资源。
500 Internal Server Error  最常见的服务器端错误。
503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）。
JSONP：json+padding（内填充），顾名思义，就是把JSON填充到一个盒子里
优点是兼容性好，简单易用，支持浏览器与服务器双向通信。缺点是只支持GET请求。
原理是：动态插入script标签，通过script标签引入一个js文件，这个js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入。

XML和JSON的区别？
(1).数据体积方面。
JSON相对于XML来讲，数据的体积小，传递的速度更快些。
(2).数据交互方面。
JSON与JavaScript的交互更加方便，更容易解析处理，更好的数据交互。
(3).数据描述方面。
JSON对数据的描述性比XML较差。
(4).传输速度方面。
JSON的速度要远远快于XML。

webpack
模块打包（HTML、Javascript、CSS以及各种静态文件图片、字体等）工具，支持amd，cmd
以commonJS的形式来书写脚本，具有requireJs和browserify的功能
可以将代码切割成不同的chunk，实现按需加载，降低了初始化时间
webpack 使用异步 IO 并具有多级缓存。这使得 webpack 很快且在增量编译上更加快

创建ajax过程
(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象.
(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息.
(3)设置响应HTTP请求状态变化的函数.
(4)发送HTTP请求.
(5)获取异步调用返回的数据.
(6)使用JavaScript和DOM实现局部刷新.

http https
默认HTTP的端口号为80，HTTPS的端口号为443。
因为网络请求需要中间有很多的服务器路由器的转发。中间的节点都可能篡改信息，而如果使用HTTPS，密钥在你和终点站才有。https之所以比http安全，是因为他利用ssl/tls协议传输。它包含证书，卸载，流量转发，负载均衡，页面适配，浏览器适配，refer传递等。保障了传输过程的安全性

对前端模块化的认识
AMD 是 RequireJS 在推广过程中对模块定义的规范化产出。
CMD 是 SeaJS 在推广过程中对模块定义的规范化产出。
AMD 是提前执行，CMD 是延迟执行。
AMD推荐的风格通过返回一个对象做为模块对象，CommonJS的风格通过对module.exports或exports的属性赋值来达到暴露模块对象的目的。

你觉得前端工程的价值体现在哪
为简化用户使用提供技术支持（交互部分）
为多个浏览器兼容性提供支持
为提高用户浏览速度（浏览器性能）提供支持
为跨平台或者其他基于webkit或其他渲染引擎的应用提供支持
为展示数据提供支持（数据接口）

谈谈性能优化问题
代码层面：避免使用css表达式，避免使用高级选择器，通配选择器。
缓存利用：缓存Ajax，使用CDN，使用外部js和css文件以便缓存，添加Expires头，服务端配置Etag，减少DNS查找等
请求数量：合并样式和脚本，使用css图片精灵，初始首屏之外的图片资源按需加载，静态资源延迟加载。
请求带宽：压缩文件，开启GZIP，

代码层面的优化
用hash-table来优化查找
少用全局变量
用innerHTML代替DOM操作，减少DOM操作次数，优化javascript性能
用setTimeout来避免页面失去响应
缓存DOM节点查找的结果
避免使用CSS Expression
避免全局查询
避免使用with(with会创建自己的作用域，会增加作用域链长度)
多个变量声明合并
避免图片和iFrame等的空Src。空Src会重新加载当前页面，影响速度和效率
尽量避免写在HTML标签中写Style属性
移动端性能优化
尽量使用css3动画，开启硬件加速。
适当使用touch事件代替click事件。
避免使用css3渐变阴影效果。
可以用transform: translateZ(0)来开启硬件加速。
不滥用Float。Float在渲染时计算量比较大，尽量减少使用
不滥用Web字体。Web字体需要下载，解析，重绘当前页面，尽量减少使用。
合理使用requestAnimationFrame动画代替setTimeout
CSS中的属性（CSS3 transitions、CSS3 3D transforms、Opacity、Canvas、WebGL、Video） - 会触发GPU渲染，请合理使用。过渡使用会引发手机过耗电增加
PC端的在移动端同样适用
数据结构
栈和队列的区别?
栈的插入和删除操作都是在一端进行的，而队列的操作却是在两端进行的。
队列先进先出，栈先进后出。
栈只允许在表尾一端进行插入和删除，而队列只允许在表尾一端进行插入，在表头一端进行删除
栈和堆的区别？
栈区（stack）— 由编译器自动分配释放 ，存放函数的参数值，局部变量的值等。
堆区（heap） — 一般由程序员分配释放， 若程序员不释放，程序结束时可能由OS回收。
堆（数据结构）：堆可以被看成是一棵树，如：堆排序；
栈（数据结构）：一种先进后出的数据结构。
ES6的了解
新增模板字符串（为JavaScript提供了简单的字符串插值功能）、箭头函数（操作符左边为输入的参数，而右边则是进行的操作以及返回的值Inputs=>outputs。）、for-of（用来遍历数据—例如数组中的值。）arguments对象可被不定参数和默认参数完美代替。ES6将promise对象纳入规范，提供了原生的Promise对象。增加了let和const命令，用来声明变量。增加了块级作用域。let命令实际上就增加了块级作用域。ES6规定，var命令和function命令声明的全局变量，属于全局对象的属性；let命令、const命令、class命令声明的全局变量，不属于全局对象的属性。。还有就是引入module模块的概念

js继承
还是看书吧

用过哪些设计模式？
还是看书吧

工厂模式：
主要好处就是可以消除对象间的耦合，通过使用工程方法而不是new关键字。将所有实例化的代码集中在一个位置防止代码重复。
工厂模式解决了重复实例化的问题 ，但还有一个问题,那就是识别问题，因为根本无法 搞清楚他们到底是哪个对象的实例。

构造函数模式
使用构造函数的方法 ，即解决了重复实例化的问题 ，又解决了对象识别的问题，该模式与工厂模式的不同之处在于：
1.构造函数方法没有显示的创建对象 (new Object());
2.直接将属性和方法赋值给 this 对象;
3.没有 renturn 语句。

说说你对闭包的理解
使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染，缺点是闭包会常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。在js中，函数即闭包，只有函数才会产生作用域的概念
闭包有三个特性：
1.函数嵌套函数
2.函数内部可以引用外部的参数和变量
3.参数和变量不会被垃圾回收机制回收

请你谈谈Cookie的弊端
Cookie数量和长度的限制
安全性问题
有些状态不可能保存在客户端

浏览器本地存储
在较高版本的浏览器中，js提供了sessionStorage和globalStorage。在HTML5中提供了localStorage来取代globalStorage。
html5中的Web Storage包括了两种存储方式：sessionStorage和localStorage。
sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储。
而localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。

Web Storage拥有setItem,getItem,removeItem,clear等方法，不像cookie需要前端开发者自己封装setCookie，getCookie。

cookie 和session 的区别：
1、cookie数据存放在客户的浏览器上，session数据放在服务器上。
2、cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗

考虑到安全应当使用session。
3、session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能

考虑到减轻服务器性能方面，应当使用COOKIE。
4、单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。
5、所以个人建议：

将登陆信息等重要信息存放为SESSION
其他信息如果需要保留，可以放在COOKIE中

优先级为:
!important > id > class > tag
important 比 内联优先级高,但内联比 id 要高

说说你对语义化的理解？
1，去掉或者丢失样式的时候能够让页面呈现出清晰的结构

2，有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；

3，方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；

4，便于团队开发和维护，语义化更具可读性，是下一步吧网页的重要动向，遵循W3C标准的团队都遵循这个标准，可以减少差异化。

常见兼容性问题？
png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.也可以引用一段脚本处理.

浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。

IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。

浮动ie产生的双倍距离（IE6双边距问题：在IE6下，如果对元素设置了浮动，同时又设置了margin-left或margin-right，margin值会加倍。）

box{ float:left; width:10px; margin:0 0 0 100px;}
这种情况之下IE会产生20px的距离，解决方案是在float的标签样式控制中加入
_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)

渐进识别的方式，从总体中逐渐排除局部。

首先，巧妙的使用“9”这一标记，将IE游览器从所有情况中分离出来。

接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。

css

  .bb{

   background-color:#f1ee18;/*所有识别*/

  .background-color:#00deff\9; /*IE6、7、8识别*/

  +background-color:#a200ff;/*IE6、7识别*/

  _background-color:#1e0bd1;/*IE6识别*/

  }
怪异模式问题：漏写DTD声明，Firefox仍然会按照标准模式来解析网页，但在IE中会触发
怪异模式。为避免怪异模式给我们带来不必要的麻烦，最好养成书写DTD声明的好习惯。现在
可以使用html5推荐的写法：<doctype html>
上下margin重合问题
ie和ff都存在，相邻的两个div的margin-left和margin-right不会重合，但是margin-top和margin-bottom却会发生重合。

解决方法，养成良好的代码编写习惯，同时采用margin-top或者同时采用margin-bottom。

DOM操作——怎样添加、移除、移动、复制、创建和查找节点。
1）创建新节点

  createDocumentFragment()    //创建一个DOM片段

  createElement()   //创建一个具体的元素

  createTextNode()   //创建一个文本节点
2）添加、移除、替换、插入

  appendChild()

  removeChild()

  replaceChild()

  insertBefore() //并没有insertAfter()
3）查找

  getElementsByTagName()    //通过标签名称

  getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，
  会得到一个数组，其中包括id等于name值的)

  getElementById()    //通过元素Id，唯一性
如何实现浏览器内多个标签页之间的通信?
调用localstorge、cookies等本地存储方式
null和undefined的区别？
null是一个表示"无"的对象，转为数值时为0；undefined是一个表示"无"的原始值，转为数值时为NaN。
当声明的变量还未被初始化时，变量的默认值为undefined。
null用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。
undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法是：
（1）变量被声明了，但没有赋值时，就等于undefined。
（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。
（3）对象没有赋值的属性，该属性的值为undefined。
（4）函数没有返回值时，默认返回undefined。
null表示"没有对象"，即该处不应该有值。典型用法是：
（1） 作为函数的参数，表示该函数的参数不是对象。
（2） 作为对象原型链的终点。

new操作符具体干了什么呢?
1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
2、属性和方法被加入到 this 引用的对象中。
3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。

var obj  = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
js延迟加载的方式有哪些？
defer和async、动态创建DOM方式（创建script，插入到DOM中，加载完毕后callBack）、按需异步载入js
