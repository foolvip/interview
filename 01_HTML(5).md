# 面试题目总结

## html
### 简述一下你对 HTML 语义化的理解 ？
1. html语义化让页面的内容结构化，去掉或者丢失样式的时候能够让页面呈现出清晰的结构
2. 便于浏览器、搜索引擎解析;
3. 有助于爬虫抓取更多的有效信息，搜索引擎的爬虫也依赖于 HTML 标记来确定上下文和各个关键字的权重，利于 SEO;
4. 语义化更具可读性，对于阅读源码的人，便于理解，便于团队开发和维护。
5. 方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；
### Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?
#### Doctype作用：
<!DOCTYPE> 声明位于文档中的最前面，处于 <html> 标签之前。告知浏览器以何种模式来渲染文档。   
#### 区别：  
严格模式的排版和JS运作模式是以该浏览器支持的最高标准运行。  
在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。  

1.在严格模式中 ：width是内容宽度 ，元素真正的宽度 = margin-left + border-left-width + padding-left + width + padding-right + border-right- width +  margin-right;   
在怪癖模式中 ：width则是元素的实际宽度 ，内容宽度 = width - ( padding-left + padding-right + border-left-width + border-right-width)  
2.可以设置行内元素的高宽  
在Standards模式下，给span等行内元素设置wdith和height都不会生效，而在quirks模式下，则会生效。  
3.可设置百分比的高度  
在standards模式下，一个元素的高度是由其包含的内容来决定的，如果父元素没有设置高度，子元素设置一个百分比的高度是无效的。  
4.用margin:0 auto设置水平居中在IE下会失效  
使用margin:0 auto在standards模式下可以使元素水平居中，但在quirks模式下却会失效,quirk模式下的解决办法，用text-align属性:  
body{text-align:center};#content{text-align:left}  
5.quirk模式下设置图片的padding会失效  
6.quirk模式下Table中的字体属性不能继承上层的设置  
7.quirk模式下white-space:pre会失效  
#### 意义
DOCTYPE不存在或格式不正确会导致文档以混杂模式呈现。  
### 你知道多少种Doctype文档类型？
该标签可声明三种 DTD 类型，分别表示严格版本、过渡版本以及基于框架的 HTML 文档。
 HTML 4.01 规定了三种文档类型：Strict、Transitional 以及 Frameset。  
 XHTML1.0规定了三种XML文档类型：Strict、Transitional 以及 Frameset。  
Standards（标准）模式（也就是严格呈现模式）用于呈现遵循最新标准的网页，而 Quirks（包容）模式（也就是松散呈现模式或者兼容模式用于呈现为传统浏览器而设计的网页。  
1过度型Transitional，这种文档对标记语法要求不是很严格。  
2严格型strict,这种文档对标记语法要求严格。  
3框架型frameset当网页设计中有框架元素(如：frameset/frame))，就用这种文档类型.  

### HTML5移动端meta标签
简介: 常用于定义页面的说明，关键字，最后修改日期，和其它的元数据。这些元数据将服务于浏览器（如何布局或重载页 面），搜索引擎和其它网络服务。
#### charset属性
```html
<!-- 定义网页文档的字符集 -->
<meta charset="utf-8" />
```
#### name + content属性
```html
<!-- 网页作者 -->
<meta name="author" content="开源技术团队"/>
<!-- 网页地址 -->
<meta name="website" content="https://sanyuan0704.github.io/frontend_daily_question/"/>
<!-- 网页版权信息 -->
 <meta name="copyright" content="2018-2019 demo.com"/>
<!-- 网页关键字, 用于SEO -->
<meta name="keywords" content="meta,html"/>
<!-- 网页描述 -->
<meta name="description" content="网页描述"/>
<!-- 搜索引擎索引方式，一般为all，不用深究 -->
<meta name="robots" content="all" />
<!-- 移动端常用视口设置 -->
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=1.0, user-scalable=no"/>
<!-- 
  viewport参数详解：
  width：宽度（数值 / device-width）（默认为980 像素）
  height：高度（数值 / device-height）
  initial-scale：初始的缩放比例 （范围从>0 到10）
  minimum-scale：允许用户缩放到的最小比例
  maximum-scale：允许用户缩放到的最大比例
  user-scalable：用户是否可以手动缩 (no,yes)
 -->
```
#### http-equiv + content属性
```html
<!-- expires指定网页的过期时间。一旦网页过期，必须从服务器上下载。 -->
<meta http-equiv="expires" content="Fri, 12 Jan 2020 18:18:18 GMT"/>
<!-- 等待一定的时间刷新或跳转到其他url。下面1表示1秒 -->
<meta http-equiv="refresh" content="1; url=https://www.baidu.com"/>
<!-- 禁止浏览器从本地缓存中读取网页，即浏览器一旦离开网页在无法连接网络的情况下就无法访问到页面。 -->
<meta http-equiv="pragma" content="no-cache"/>
<!-- 也是设置cookie的一种方式，并且可以指定过期时间 -->
<meta http-equiv="set-cookie" content="name=value expires=Fri, 12 Jan 2001 18:18:18 GMT,path=/"/>
<!-- 使用浏览器版本 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<!-- 针对WebApp全屏模式，隐藏状态栏/设置状态栏颜色，content的值为default | black | black-translucent -->
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />


<!-- 例子 -->
作者：叶非叶
链接：https://zhuanlan.zhihu.com/p/80357141
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

<meta charset="utf-8"> <!-- 设置文档字符编码 -->
<meta http-equiv="x-ua-compatible" content="ie=edge"><!-- 告诉IE浏览器，IE8/9及以后的版本都会以最高版本IE来渲染页面。 -->
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"><!-- 指定页面初始缩放比例。-->
 
<!-- 上述3个meta标签须放在head标签最前面;其它head内容放在其后面，如link标签-->
 
<!-- 允许控制加载资源 -->
<meta http-equiv="Content-Security-Policy" content="default-src 'self'">
<!-- 尽可能早的放在文档 -->
<!-- 只适用于下面这个标签的内容 -->
 
<!-- 使用web应用程序的名称(当网站作为一个应用程序的时候)-->
<meta name="application-name" content="Application Name">
 
<!-- 页面的简短描述(限150个字符)-->
<!-- 在某些情况下这个描述作为搜索结果中所示的代码片段的一部分。-->
<meta name="description" content="A description of the page">
 
<!-- 控制搜索引擎爬行和索引的行为 -->
<meta name="robots" content="index,follow,noodp"><!-- 所有搜索引擎 -->
<meta name="googlebot" content="index,follow"><!-- 谷歌 -->
 
<!-- 告诉谷歌搜索框不显示链接 -->
<meta name="google" content="nositelinkssearchbox">
 
<!-- 告诉谷歌不要翻译这个页面 -->
<meta name="google" content="notranslate">
 
<!-- Google网站管理员工具的特定元标记，核实对谷歌搜索控制台所有权 -->
<meta name="google-site-verification" content="verification_token">
 
<!-- 说明用什么软件构建生成的网站，(例如,WordPress,Dreamweaver) -->
<meta name="generator" content="program">
 
<!-- 简短描述你的网站的主题 -->
<meta name="subject" content="your website's subject">
 
<!-- 很短(10个词以内)描述。主要学术论文 -->
<meta name="abstract" content="">
 
<!-- 完整的域名或网址 -->
<meta name="url" content="https://example.com/">
 
<meta name="directory" content="submission">
 
<!-- 对当前页面一个等级衡量，告诉蜘蛛当前页面在整个网站中的权重到底是多少。General是一般页面，Mature是比较成熟的页面，Restricted代表受限制的。 -->
<meta name="rating" content="General">
 
<!-- 隐藏发送请求时请求头表示来源的referrer字段。 -->
<meta name="referrer" content="no-referrer">
 
<!-- 禁用自动检测和格式的电话号码 -->
<meta name="format-detection" content="telephone=no">
 
<!-- 通过设置“off”,完全退出DNS队列 -->
<meta http-equiv="x-dns-prefetch-control" content="off">
 
<!-- 在客户端存储 cookie，web 浏览器的客户端识别-->
<meta http-equiv="set-cookie" content="name=value; expires=date; path=url">
 
<!-- 指定要显示在一个特定框架中的页面 -->
<meta http-equiv="Window-Target" content="_value">
 
<!-- 地理标签 -->
<meta name="ICBM" content="latitude, longitude">
<meta name="geo.position" content="latitude;longitude">
<meta name="geo.region" content="country[-state]"><!-- 国家代码 (ISO 3166-1): 强制性, 州代码 (ISO 3166-2): 可选; 如 content="US" / content="US-NY" -->
<meta name="geo.placename" content="city/town"><!-- 如 content="New York City" -->

```

属性包括：
name="viewport"
content="width=device-width, height=device-height,target-densitydpi=high-dpi,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0 user-scalable=no"
### HTML与XHTML——二者有什么区别
区别：
一个是功能上的差别，另外是书写习惯的差别。  
功能上的差别，主要是XHTML可兼容各大浏览器、手机以及PDA，并且浏览器也能快速正确地编译网页。   
XHTML的语法较为严谨。  
1. 所有标签都必须小写
2. 标签必须成双成对
3. 标签顺序必须正确
4. 所有属性都必须使用双引号
5. 不允许使用target="_blank"

### Web标准
WEB标准不是某一个标准，而是一系列标准的集合，是W3C组织和其它标准化组织制定的一套规范集合。网页主要由三部分组成：结构、表现和行为。对应的标准也分三方面：结构化标准语言主要包括XHTML和XML，表现标准语言主要包括CSS，行为标准主要包括对象模型、ECMAScript等。这些标准大部分由万维网联盟起草和发布，也有一些是其他标准组织制订的标准，比如ECMA的ECMAScript标准。
### 前端页面有哪三层构成，分别是什么？作用是什么？
网页分成三个层次，即：结构层、表示层、行为层。   
网页的结构层（structurallayer）由 HTML 或 XHTML 之类的标记语言负责创建。 标签，也就是那些出现在尖括号里的单词，对网页内容的语义含义做出这些标签不包含任何关于如何显示有关内容的信息。例如，P 标签表达了这样一种语义：“这是一个文本段。”
网页的表示层（presentationlayer）由 CSS 负责创建。CSS 对“如何显示有关内容”的问题做出了回答。
网页的行为层（behaviorlayer）负责回答 “内容应该如何对事件做出反应” 这一问题。 这是 Javascript 语言和 DOM 主宰的领域。

### HTML5 为什么只需要写 < !DOCTYPE HTML> ？
HTML5 不基于 SGML(标准通用标记语言（以下简称“通用标言”)，因此不需要对 DTD 进行引用，但是需要doctype来规范浏览器的行为（让浏览器按照它们应该的方式来运行）；   
而 HTML4.01 基于 SGML，所以需要对 DTD 进行引用，才能告知浏览器文档所使用的文档类型。
### HTML5 有哪些新特性、移除了那些元素 ？如何处理 HTML5 新标签的浏览器兼容问题 ？如何区分 HTML 和 HTML5 ？
#### HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
- 语义化更好的内容标签（主体结构元素：article,section,nav,aside. 非主体结构：header, hgroup, address, main, footer）
- 表单控件，calendar、date、time、email、url、search  
- 音频、视频API(audio,video)
- 画布(Canvas) API
- 拖拽释放(Drag and drop) API 
- 地理(Geolocation) API
- history API
- 文件 API
- 本地存储 localStorage 长期存储数据，浏览器关闭后数据不丢失；sessionStorage 的数据在浏览器关闭后自动删除
- 离线应用程序（本地缓存）
- 新的技术webworker, websocket, Geolocation
#### 移除的元素
1. 纯表现的元素：basefont，big，center，font, s，strike，tt，u；
2. 对可用性产生负面影响的元素：frame，frameset，noframes；
#### 如何处理 HTML5 新标签的浏览器兼容问题 
支持HTML5新标签：IE8/IE7/IE6支持通过document.createElement方法产生的标签，可以利用这一特性让这些浏览器支持HTML5新标签，  
浏览器支持新标签后，还需要添加标签默认的样式：当然最好的方式是直接使用成熟的框架、使用最多的是html5shim框架
```js
<!--[if lt IE 9]> 
  <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script> 
<![endif]--> 
```
#### 如何区分： 
DOCTYPE声明、新增的结构元素、功能元素
### 本地缓存与浏览器网页缓存的区别
- 应用范围：本地缓存为整个web应用程序服务，浏览器网页缓存只服务于单个网页。
- 缓存内容：任何网页都具有网页缓存，本地缓存只缓存那些你指定缓存的网页。
- 安全性：本地缓存可以控制对哪些内容进行缓存，是可靠的。网页缓存是不安全的，不可靠的，我们不知道在网站中到底缓存了哪些网页，以及缓存了网页上的那些资源。
### iframe的优缺点？
```js
1. <iframe>优点：
  解决加载缓慢的第三方内容如图标和广告等的加载问题     
  Security sandbox：隔离上下文    
  并行加载脚本  
2. <iframe>的缺点：
 iframe会阻塞主页面的Onload事件；
 即时内容为空，加载也需要时间;
 没有语意;
 数据通信麻烦；
 跨域问题（若非同源，会受到三种跨域限制：一是ajax请求限制；二是DOM无法获得；三是Cookie、LocalStorage 和 IndexDB 无法读取。）；
弹框样式：position:relation；定位不准
加载但也应用时，切换iframe内嵌应用路由，浏览器回退，地址栏URL无变化
```
### 简述一下 src 与 href 的区别
href 是指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，用于超链接。   
src 是指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；
在请求src资源时会将其指向的资源下载并应用到文档内，例如js脚本，img图片和frame等元素。  
当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将js脚本放在底部而不是头部。

## 浏览器、性能
### 浏览器内核
### 如何实现浏览器内多个标签页之间的通信?
- 调用localstorge、cookies等本地存储方式
- localstorge 在另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件，我们通过监听事件，控制它的值来进行页面信息通信； 注意 quirks：Safari 在无痕模式下设置 localstorge 值时会抛出 QuotaExceededError 的异常；
- WebSocket、SharedWorker；


### 线程与进程的区别
一个程序至少有一个进程,一个进程至少有一个线程. 
线程的划分尺度小于进程，使得多线程程序的并发性高。 
另外，进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率。 
线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口。但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制。 
从逻辑角度来看，多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。但操作系统并没有将多个线程看做多个独立的应用，来实现进程的调度和管理以及资源分配。这就是进程和线程的重要区别。
### 你如何对网站的文件和资源进行优化？
- 文件合并
- 文件最小化/文件压缩
- 使用 CDN 托管
- 缓存的使用（多个域名来提供缓存）
- 其他
### 请说出三种减少页面加载时间的方法。
1. 优化图片 
2. 图像格式的选择（GIF：提供的颜色较少，可用在一些对颜色要求不高的地方） 
3. 优化CSS（压缩合并css，如margin-top,margin-left...) 
4. 网址后加斜杠（如www.campr.com/目录，会判断这个“目录是什么文件类型，或者是目录。） 
5. 标明高度和宽度（如果浏览器没有找到这两个参数，它需要一边下载图片一边计算大小，如果图片很多，浏览器需要不断地调整页面。这不但影响速度，也影响浏览体验。 
当浏览器知道了高度和宽度参数后，即使图片暂时无法显示，页面上也会腾出图片的空位，然后继续加载后面的内容。从而加载时间快了，浏览体验也更好了。） 
6. 减少http请求（合并文件，合并图片）。
### 你都使用哪些工具来测试代码的性能？
Profiler, JSPerf（http://jsperf.com/nexttick-vs-setzerotimeout-vs-settimeout）, Dromaeo
#### 什么是 FOUC（无样式内容闪烁）？你如何来避免 FOUC？
FOUC - Flash Of Unstyled Content 文档样式闪烁  
#### 形成原因：
- 通过 @import 引入 css 样式
<style>
    @import "../fouc.css";
</style> 
- 样式表放在页面底部
- 有多个样式表，放在 html 不同位置
 <style type="text/css" media="all">@import "../fouc.css";</style>  

#### 原理：
IE会先加载整个HTML文档的DOM，然后再去导入外部的CSS文件，因此，在页面DOM加载完成到CSS导入完成中间会有一段时间页面上的内容是没有样式的，这段时间的长短跟网速，电脑速度都有关系。  
#### 解决方法：
只要在<head>之间加入<link>或<script>标签。

