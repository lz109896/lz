#### 1.	一个暗流涌动的世界
```
安全问题导致大量用户信息泄露，及海量的经济损失
黑客、专家短兵相接

复杂、激情的事。。摸透有点难，但还是要有安全意识，要有基本只是
传播的蠕虫

```
#### 2.	web 安全
```
网站漏洞
WEB安全
软件工程师职责

Web 安全包括:sql 注入（已经相当完善了）
         XSS
         CSRF
         DDOS
         HTTP 劫持

```
#### 3.	标志性的微博事件
```
2011年6月28日晚间 XSS 攻击新浪微博事件，对各大微博以及开放平台，有什么可以吸取的教训和启示？
严重影响用户体验，及产品口碑


这次攻击是典型的利用XSS漏洞进行CSRF攻击，没有用到API，与开放平台无关，开放平台本身有很高的安全性(OAuth)。
1. XSS上面有人说，XSS漏洞不是大问题，我不同意。
XSS分两种：一种是「永久」的，常见的情况是输入框中的问题不进行过滤(strip tags)，导致script这种危险标签会被显示出来，
别人访问这个页面，脚本会被执行。这种非常严重，类似于今年人人网受到的XSS攻击，当时人人网整个站内信系统崩溃。

第二种是「反射」的，就像这次新浪微博，原因是某些网页的JS编写不是很规范，导致网址可以嵌入一个脚本执行。一般认为这种危险
系数较低，但是由于社交网络的特性，导致本身不高的危险，通过关系网被放大。总结：XSS，无论大小，都比较严重，
尤其是对于社交网络。

2. CSRF[修正]CSRF攻击如果由XSS提供入口，攻击的复杂性就大大降低，只需要简单的脚本就可以实现。新浪微博是没有严格的防范
CSRF的，严格的防范流程是在用户载入页面的时候，在Form加入一个隐藏的Input，生成一个随机的字串作为value，同时后台记录这个
value。用户提交Form的时候，验证value是否匹配。这样的方法可以更好防范CSRF，但是新浪为什么没有这么做，我觉得一个可能的
原因是承受力。新浪微博由于用户非常多，一个小小的功能增加就会造成很大的负担，所以在考虑防范CSRF的时候，肯定也会考虑和
增加的投入比，是否值得。新浪微博现在的服务器不算是很稳定，增加这个功能，会增加服务器负担，增加服务器的不稳定。

3. 安全测试世界上没有绝对安全，也没有人能够面面俱到。所以类似WooYun这种漏洞提交平台非常重要，各大厂商也都有关注。

4. 对于开发者现在写Web App，现有的Framework已经可以防范不少的安全漏洞，比自己写要安全不少：以前经常可以碰到简单的
SQL Injection，现在基本上都没有了。往上有许多Self check list，开发者可以对照一下，看看自己哪些方面做的不够。

5. 危机处理从危机处理的方式来说，新浪微博这次处理要好过人人网。人人网的漏洞要更严重，甚至导致站内信系统完全被拖垮，
而人人网并没有发布任何公告，也没有其他的措施，任其发展。第二天，把所有的站内信删掉，当作没发生过一样。新浪这次做的比较
好的地方在于，及时的通过「侧边栏」和「微博小秘书」发布了公告，同时，由于新浪的短链接(人人网当时没有短链接)，可以迅速停掉
对于该网址的解析。不过攻击者也不傻，通过附带随即参数(unix时间戳)来防止新浪一下子全部杀死。

6. 从攻击者的角度除了CSRF，攻击者都倾向于采用「暴力」的方法来抓去信息，比如人人网的攻击通过暴力抓去个人信息页面的信息，
而新浪微博通过暴力抓取粉丝名单页面来传播，大概是因为现在浏览器执行 javascript 的速度有质的提升，使得「暴力」成为可能。

P.S. 人人网和新浪的攻击脚本，没有minified，如果 minified 可以省掉不少带宽，同时也让我们无法更好的读到代码。

```

#### 5.	XSS 简介
```
A - 反射型 XSS。
B - 存储型 XSS。
C - DOM-Based 型 XSS。
```
![](https://raw.githubusercontent.com/lz109896/Web-datum/cd7903962895dc22e75e9345d36628101b07d018/XSS%20%E7%AE%80%E4%BB%8B%20.png)

#### 6.	反射型 XSS
不存储在服务端的 XSS
```
事实上对于反射型 XSS，大家主要理解下面的这四句话就可以了。

1.反射型 XSS，也可称为非持久型 XSS。
2.其攻击方式往往是通过诱导用户去点击一些带有恶意脚本参数的 URL而发起的。
3.事实上由于反射型 XSS 因为 url 特征导致很容易被防御。很多浏览器如 Chrome 都内置了 相应的 XSS 过滤器，来防范用户
点击了反射型 XSS 的恶意链接
4.反射型 XSS 归根到底就是由于不可信的用户输入被服务器在没有安全防范处理，然后就直接使用到响应页面中，然后反射给用户
而导致代码在浏览器执行的一种 XSS 漏洞。
```
![]()

#### 7.	存储型 XSS
恶意代码存储到漏洞服务器中，用户浏览器相关页面发起攻击

```
1.存储型 XSS 并不需要用户点击链接才能触发。

2.无论是反射型 XSS 还是存储型 XSS，其本质都是 XSS 攻击。因此大家需要始终记住 XSS 攻击的本质就是由于
浏览器执行攻击者插入的恶意的脚步数据所致。

3.总结：持久型 XSS 其实就是由于不可信的用户(黑客)输入在没有任何验证的情况下保存在服务端的文件或者数据库中，
并且取出不可信的数据时也没有做相关安全处理就返回响应，导致了存储的恶意脚本数据在浏览器中执行的一种 XSS 漏洞。
```
![](https://raw.githubusercontent.com/lz109896/Web-datum/cd7903962895dc22e75e9345d36628101b07d018/%E5%AD%98%E5%82%A8%E5%9E%8B%20XSS%201.png)
![](https://raw.githubusercontent.com/lz109896/Web-datum/cd7903962895dc22e75e9345d36628101b07d018/%E5%AD%98%E5%82%A8%E5%9E%8B%20XSS%202.png)

#### 8.	DOM Based 型 XSS
```
前两种 XSS 都需要 服务端参与解析，恶意脚本数据
DOM Based 型 XSS 不依赖于服务端参与解析，前端页面进行 DOM 操作时，带有恶意代码片段被 HTML 解析执行，
从而导致 XSS 攻击，比如修改 DOM 时。基于浏览器（客户端） DOM 解析的攻击
```
![](https://raw.githubusercontent.com/lz109896/Web-datum/cd7903962895dc22e75e9345d36628101b07d018/DOM%20Based%20%E5%9E%8B%20XSS%2019.png)
```
前面所说的反射型 XSS（服务端直接使用恶意脚本并返回结果页）和存储型 XSS （服务端存储恶意脚本并返回）都是需要服务端的
直接参与的。然而对于 DOM-Based 型 XSS 来说，其并不依赖服务端，服务端的响应不会涉及到恶意脚本的内容。DOM-Based 型
XSS 是客户端 XSS 的一种形式, 其数据来源在客户端中。

其中DOM-Based 型 XSS 是由于客户端 JavaScript 脚本修改页面 DOM 结构时引起浏览器 DOM 解析所造成的一种漏洞攻击。
因此如果页面 JavaScript 脚本不存在着漏洞的话，则不会发送 DOM-Based 型 XSS 攻击啦。

事实上，从效果来看 DOM-Based 型 XSS 也是需要诱导用户去打开相应恶意链接才能发送的 XSS 攻击。
```
#### 9.	XSS payload 和危害
```
实现 XSS 攻击的恶意脚本就是 XSS payload 

1.窃取用户的 cookie  document.cookie
2.识别用户浏览器     navigator.userAgent
3.伪造请求          get/post
4.XSS 钓鱼          XSS payload +钓鱼网站
```
```
C. XSS 在页面注入钓鱼网站链接
D. 用户浏览钓鱼网站
A. 用户输入账号密码
B. 账号密码发送到服务端
```
#### 10.	XSS 防御 - httpOnly
![](https://raw.githubusercontent.com/lz109896/Web-datum/cd7903962895dc22e75e9345d36628101b07d018/XSS%20%E9%98%B2%E5%BE%A1%20-%20httpOnly%201.png)
```
给 cookie 设置 httpOnly，阻止客户端监本访问 Cookie
```
![](https://raw.githubusercontent.com/lz109896/Web-datum/cd7903962895dc22e75e9345d36628101b07d018/XSS%20%E9%98%B2%E5%BE%A1%20-%20httpOnly%202.png)

#### 11.	 [资料] Web 相关编码

##### Web 相关编码和转义
```
提到 Web 前端安全，第一个想到的就是 XSS。
而提到 XSS，不得不说的就是编码了。事实上，编码涉及的知识十分的复杂，很难短时间梳理清楚和弄明白。
在这里只要求大家对编码有一个概念就好，日后再进行深究。
```
##### 常用编码
本文从 XSS 中常用的编码讲起，分为

* URL 编码
* HTML 编码
* JS 编码

##### URL编码
```
一般来说，URL只能使用英文字母（a-zA-Z）、数字（0-9）、-_.~4个特殊字符以及所有（;,/?:@&=+$#）保留字符。

意味着如果使用了一些其他文字和特殊字符，则需要通过编码的方式来进行表示，如：
```
```javascript
// 使用了汉字
var url1 = 'http://www.帅.com';
```
另外我们知道在 URL 中传参是通过键值对形式进行的，格式上是以？、& 和 = 为特征标识进行解析，
如果在键或者值的内容中包含一些特殊符号，就会造成解析错误，如下所示：
```javascript
// 键为汉字
var url2 = 'http://www.a.com?我=1';
// 值的内容为特殊符号
var url3 = 'http://a.com?key=?&';
```
对于上面的情况如果我们要正常解析，则需要进行编码，需要用不会造成歧义的符号代替有歧义的符号。

我们可以通过使用系统原生实现的 API 来对字符进行 URL 编码如:

* encodeURI()
* encodeURIComponent()
* escape 逐渐废弃可以不理会

##### encodeURI
encodeURI 是用来编码 URI 的，最常见的就是编码一个 URL。encodeURI 会将需要编码的字符转换为 UTF-8 的格式。
对于保留字符（;,/?:@&=+$#），以及非转义字符（字母数字以及 -_.!~*'()）不会进行转义。

例如之前 URL 中包含中文，我们可以使用 encodeURI：
```javascript
encodeURI('http://www.帅.com'); // http://www.%E5%B8%85.com
encodeURI('http://www.a.com?我=1');// "http://www.a.com?%E6%88%91=1"
```
在这里，%E5%B8%85 就是 帅 的 URL 编码，%E6%88%91 即为 我 的 URL 编码。然后由于 encodeURI 不转义&、?和=。
所以对于 URL 参数的值是无法转义的，如下面的例子：
```javascript
// 值的内容为特殊符号
encodeURI('http://a.com?key=?&'); // "http://a.com?key=?&"
```
此时我们就需要使用 encodeURIComponent 来解决。

##### encodeURIComponent
顾名思义，encodeURIComponent 是用来编码 URI 参数的。它会跳过非转义字符（字母数字以及-_.!~*'()）。但会转义 URL的 
保留字符（;,/?:@&=+$#）。通常来说我们会 encodeURI 结合 encodeURIComponent 来使用，如下所示：
```javascript
// "http://a.com?a=%3F%26"
encodeURI('http://a.com') + '?a=' + encodeURIComponent('?&');  
```
其中 %3F 和 %26 分别为 ? 和 & 的 URL 编码。需注意的是由于 encodeURIComponent 会编码所有的 URL 保留字，
所以不适合编码 URL，例如：
```javascript
// "http%3A%2F%2Fa.com%3Fkey%3D%3F%26"
encodeURIComponent('http://a.com?key=?&');
```
上面的 http%3A%2F%2Fa.com%3Fkey%3D%3F%26 在地址栏会被解析为一个普通的字符串而不是 URL。

##### URL 解码
有了 URL 编码，相应的会有解码机制。比如上面对应的 3个 encode 的API对应的解码 API 如下：

* decodeURI()
* decodeURIComponent()
##### HTML 编码
在 HTML 中，某些字符是预留的，比如不能使用小于号（<）和大于号（>），这是因为浏览器会误认为它们是标签。如果希望正确
地显示预留字符，我们必须在 HTML 源代码中使用字符实体（character entities）。当然还另一个重要原因，有些字符在 ASCII 
字符集中没有定义，因此需要使用字符实体来表示，比如中文。

HTML 编码分为：

* HTML 十六进制编码 &#xH;
* HTML 十进制编码 &#D;
* HTML 实体编码 &lt; 等
在 HTML 进制编码中其中的数字则是对应字符的 unicode 字符编码。
比如单引号的 unicode 字符编码是27，则单引号可以被编码为&#x27;

##### HTML 实体编码
通常来说，在业务中我们用到更多的是 HTML 的实体编码。常用的 HTML 实体编码函数如下所示：
```javascript
/**
 * 转义 HTML 特殊字符
 * @param {String} str
 */
function htmlEncode(str) {
  return String(str)
    .replace(/&/g, '&amp;')
    .replace(/"/g, '&quot;')
    .replace(/'/g, '&#39;')
    .replace(/</g, '&lt;')
    .replace(/>/g, '&gt;');
}
```
更完整的转义列表见这里。http://www.w3school.com.cn/html/html_entities.asp

##### Javascript 转义
JavaScript 中有些字符有特殊用途，如果字符串中想使用这些字符原来的含义，需要使用反斜杠对这些特殊符号进行转义。
我们称之为 Javascript编码。一般有以下几类：http://www.w3school.com.cn/js/js_special_characters.asp

* 三个八进制数字，如果不够个数，前面补0，例如 “e” 编码为“\145”
* 两个十六进制数字，如果不够个数，前面补0，例如 “e” 编码为“\x65”
* 四个十六进制数字，如果不够个数，前面补0，例如 “e” 编码为“\u0065”
* 对于一些控制字符，使用特殊的C类型的转义风格（例如\n和\r）

如下面所示，双引号用于标注字符串，然而在字符串中带了双引号，就会发生歧义：
```javascript
var str = "Hello"";
```
于是我们需要对字符串内的双引号进行转义，也就是加上反斜杠，告诉脚本引擎要区分对待：
```javascript
var str = "Hello\"";
```
更多阅读
对 Web 相关编码和转义十分感兴趣的同学可以阅读下面的文章和内容来加深理解。

前端的各种转义:
https://github.com/FrankFang/githublog/blob/master/%E6%8A%80%E6%9C%AF/%E5%89%8D%E7%AB%AF%E7%9A%84%E5%90%84%E7%A7%8D%E8%BD%AC%E4%B9%89.md


从零开始学web安全（3）:
http://imweb.io/topic/57024e4606f2400432c1396d


#### 12.	XSS 防御 - 输入检查
永远不相信用户的输入

![](https://raw.githubusercontent.com/lz109896/Web-datum/cd7903962895dc22e75e9345d36628101b07d018/XSS%20%E9%98%B2%E5%BE%A1%20-%20%E8%BE%93%E5%85%A5%E6%A3%80%E6%9F%A5%201.png)

#### 13.	XSS 防御 - 输出检查
```
最后一道防线，根据不同场景对数据进行处理
```
![](https://raw.githubusercontent.com/lz109896/Web-datum/cd7903962895dc22e75e9345d36628101b07d018/XSS%20%E9%98%B2%E5%BE%A1%20-%20%E8%BE%93%E5%87%BA%E6%A3%80%E6%9F%A5%201.png)
![](https://raw.githubusercontent.com/lz109896/Web-datum/cd7903962895dc22e75e9345d36628101b07d018/XSS%20%E9%98%B2%E5%BE%A1%20-%20%E8%BE%93%E5%87%BA%E6%A3%80%E6%9F%A5%202.png)

之所以会发生 XSS 攻击，就是由于用户的输入被当做代码来执行，导致出现意料之外的运行结果。

* HTML 标签中（用户输入将在 HTML 解析环境进行）
* HTML 非事件属性中（用户输入将在 HTML 解析环境进行）
* script 标签中 （用户输入将在 JavaScript 解析环境进行）
* HTML 事件属性中（用户输入将在 JavaScript 解析环境进行）
* 地址栏中（用户输入将在 URL 解析环境进行）

为了避免我们用户输入被当做代码来执行，因此我们需要对用户输入中存在的特殊字符做一些处理。处理规则很简单，就是：

* HTML 解析环境使用 HtmlEncode
* JavaScript 解析环境使用 JavaScriptEncode
* URL 解析环境使用 URLEncode


