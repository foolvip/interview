## js
### 什么是js? js语言的特点
JavaScript是一种基于对象（Object）和事件驱动（Event Driven）并具有相对安全性的客户端脚本语言。同时也是一种广泛用于客户端Web开发的脚本语言，常用来给HTML网页添加动态功能，比如响应用户的各种操作。它最初由网景公司（Netscape）的Brendan Eich设计，是一种动态、弱类型、基于原型的语言，内置支持类。
#### 特点
- 运行在客户端浏览器上
- 基于面向对象
- 不用预编译，直接解析执行代码；
- 是弱类型语言，较为灵活；
- 与操作系统无关，跨平台的语言；
- 脚本语言、解释性语言 
### JS 的优势是什么
- 更少的服务器交互 - 在将页面发送到服务器之前，可以验证用户输入,节省了服务器流量，意味着服务器的负载更少
- 立即反馈 - 用户不需要等待页面重新加载来查看是否忘记输入某些内容。
- 增强交互 - 在界面中，当用户使用鼠标悬停或通过键盘激活它们时会做出响应。
- 丰富的接口 - 可以使用JS包含拖放组件和滑块等项，为网站提供丰富的界面。
### js编译和执行顺序
JS是一段一段执行的（以script标签来分割），执行每一段之前，都有一个“预编译”，预编译干的活是：声明所有var变量（初始为undefined），解析定义式函数语句。
### script标签的async和defer属性
https://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html  
默认情况下，脚本的下载和执行将会按照文档的先后顺序同步进行。当脚本下载和执行的时候，文档解析就会被阻塞，在脚本下载和执行完成后才能继续往下进行解析。
#### 相同点
适用于外部脚本文件、立即下载脚本
#### 不同点
defer：表示脚本可以延迟到文档完全被解析和显示之后再执行。等到文档解析完(DOMContentLoaded事件发生)脚本才开始执行。这个属性的用途是表明脚本在执行时不会影响页面的构造。也就是说，脚本会被延迟到这个页面都解析完毕后再运行。因此，在script元素中设置defer属性。相当于告诉浏览器立即下载，但是延迟执行。   
async: 脚本的加载过程和文档加载也是异步发生的。但脚本下载完成后会停止HTML解析，执行脚本，脚本解析完继续HTML解析。立即下载脚本，但不妨碍页面中的其他操作（目的是是不让页面等待脚本下载和执行，从而异步加载页面其他内容），比如下载其他资源或等待加载其他脚本。告诉浏览器立即下载。标记为async的脚本并不保证按照指定它们的先后顺序执行。脚本的加载过程和文档加载也是异步发生的。
### document.load和jquery的ready的区别
document.onload是在样式结构加载完才执行，window.onload()不仅要样式结构加载完还要执行完所有样式图片资源文件全部加载完后才会触发
document.ready原生中无此方法，jQuery中有$().ready()，ready事件不要求页面全加载完，只需要加载完DOM结构即可触发（相当于DOMContentLoaded）。                
### load、DOMContentLoaded
#### DOMContentLoaded
dom内容加载完毕，实际上是：HTML文档被加载和解析完成（此时会触发DOMContentLoaded事件）  
如果页面中同时存在css和js，并且css后面存在js，则DOMContentLoaded事件会在css加载完后才执行（因为当css后面有js的时候，css会阻塞js运行，而js会阻塞DOM解析，从而导致DOMContentLoaded必须等到css以及css后面的js执行完成后，才会触发）。
其他情况下（只存在css,js在css前面），DOMContentLoaded都不会等待css加载，并且DOMContentLoaded事件也不会等待图片、视频等其他资源加载。
#### load
页面上所有的资源（图片，音频，视频等）被加载以后才会触发load事件，简单来说，页面的load事件会在DOMContentLoaded被触发之后才触发    
### js、css加载会造成阻塞吗
https://juejin.im/post/5b88ddca6fb9a019c7717096  
https://www.ctolib.com/topics-96984.html  
https://www.zybuluo.com/yangfch3/note/671516     
- css加载不会阻塞DOM树的解析（DOM解析和CSS解析是两个并行的进程）   
- css加载会阻塞DOM树的渲染（由于Render Tree是依赖于DOM Tree和CSSOM Tree的，所以他必须等待到CSSOM Tree构建完成（防止回流和重绘），也就是CSS资源加载完成(或者CSS资源加载失败)后，才能开始渲染。因此，CSS加载是会阻塞Dom的渲染的）  
- css加载会阻塞后面js语句的执行.（由于js可能会操作之前的Dom节点和css样式，因此浏览器会维持html中css和js的顺序。因此，样式表会在后面的js执行前先加载执行完毕。所以css会阻塞后面js的执行）
#### 减少白屏时间，我们应该尽可能的提高css加载速度，比如可以使用以下几种方法:
- 使用CDN(因为CDN会根据你的网络状况，替你挑选最近的一个具有缓存内容的节点为你提供资源，因此可以减少加载时间)
- 对css进行压缩(可以用很多打包工具，比如webpack,gulp等，也可以通过开启gzip压缩)
- 合理的使用缓存(设置cache-control,expires,以及E-tag都是不错的，不过要注意一个问题，就是文件更新后，你要避免缓存而带来的影响。其中一个解决方案是在文件名字后面加一个版本号)
- 减少http请求数，将多个css文件合并，或者是干脆直接写成内联样式(内联样式的一个缺点就是不能缓存)

 
### 0.1 + 0.2
https://github.com/mqyqingfeng/Blog/issues/155  
是浮点数精度问题导致      
ECMAScript中的Number类型使用 IEEE754 标准来表示整数和浮点数值。所谓 IEEE754 标准，全称IEEE二进制浮点数算术标准，这个标准定义了表示浮点数的格式等内容。  
在 IEEE754 中，规定了四种表示浮点数值的方式：单精确度（32位）、双精确度（64位）、延伸单精确度、与延伸双精确度。像ECMAScript采用的就是双精确度，也就是说，会用64位字节来储存一个浮点数。  
#### 浮点数转二进制、浮点数的存储
IEEE754标准认为，一个浮点数 (Value) 可以这样表示：Value = sign * exponent * fraction     
二进制科学计数法的表示时：V = (-1)^S * (1 + Fraction) * 2^E   
(-1)^S 表示符号位，当 S = 0，V 为正数；当 S = 1，V 为负数。     
(1 + Fraction)，这是因为所有的浮点数都可以表示为 1.xxxx * 2^xxx 的形式，前面的一定是 1.xxx，那干脆我们就**不存储这个 1**了，直接存后面的 xxxxx 好了，这也就是 Fraction 的部分。   
最后再看 2^E  E 既可能是负数，又可能是正数。真到实际存储的时候，我们并不会直接存储 E，而是会存储 E + bias，当用 8 个字节的时候，这个 bias 就是 127。     
所以，如果要存储一个浮点数，我们存 S 和 Fraction 和 E + bias 这三个值就好了，那具体要分配多少个字节位来存储这些数呢？IEEE754 给出了标准：我们会用 1 位存储 S，0 表示正数，1 表示负数。
用 11 位存储 E + bias，对于 11 位来说，bias 的值是 2^(11-1) - 1，也就是 1023。
用 52 位存储 Fraction。
#### 浮点数的运算
五个步骤完成：对阶、尾数运算、规格化、舍入处理、溢出判断。   
所以两次存储（0.1，0.2）时的精度丢失加上一次运算时的精度丢失，最终导致了 0.1 + 0.2 !== 0.3
#### 判断0.1 + 0.2 === 0.3
```js
let a = 0.1 + 0.2, b = 0.3;
Math.abs(a - b) < Number.EPSILON; // true: === ; false: !==
// Math.pow(2,-52)是Number.EPSILON 的兼容性写法
```

### js数据类型 
### 数据类型
Undefined、Null、Boolean、String、Number、Symbol、Object
### 基础数据类型：
Undefined、Null、Boolean、String、Number、Symbol
#### null
null值表示一个空对象指针，typeof null 结果是object, undefined值派生子null值的，所以undefined == null
#### Number
- 判断是否是数字类型: isNaN()
- 数值转换：Number()、parseInt()、parseFloat()
- 转字符串：toString()
#### String
- split(separator,howmany)、substr()、substring()
- 值不可变性
#### 字符串、数组通用方法
slice(start, end)、
### 引用数据类型：
Object
#### Object
- constructor: 保存着用于创建当前对象的函数
- hasOwnProperty(proName):
- isPrototypeOf(Object)
- toLocaleString()
- toString()
- valueOf()
#### Array
- 检测数组：Array.isArray()
- 转换方法：toLocaleString()、toString()、valueOf()、join(分隔符)
- 添加、删除元素：push、pop、shift、unshift
- 排序：sort()按升序(先toString()然后比较字符串)、reverse()
- 操作：concat()、slice(start, end)、splice()
- 位置：indexOf()、lasgIndexOf()
- 迭代：every、filter、forEach、map、some
- 归并：reduce、reduceRight()
#### Date
- Date.parse()、Date.UTC()、Date.now()
- getTime()、getFullYear()、getDate()、......
#### Function
- 没有重载
- 函数声明提升
- 四种调用函数的方式
1. 直接调用函数的方式，this指向的全局对象window
2. 函数作为对象的方法调用，this指向当前的对象.（函数属于对象的方法）
3. 通过new调用构造器的方式，this指向当前构造函数的原型
4. 通过apply或call的方式,这两个的第一参数即this，当第一个参数为null，this指向window；当第一个参数为一个对象，this就指向当前这个对象。  
函数存在「定义时上下文」和「运行时上下文」以及「上下文是可以改变的」这样的概念。
#### 函数声明有三种方式：
函数声明，函数表达式（又称函数字面量声明），函数对象的声明（使用率很低: var  方法名 =new Function("形参1","形参2","形参3", "方法体");）
#### 函数声明提升
首先是发生在某个作用域中。  
当浏览器拿到一段JavaScript代码的时候并不会去直接执行它，浏览器引擎会在执行JavaScript代码之前对其进行预编译。总的而言就是下列两个步骤：
- javascript预编译：就是通过语法分析和预解析构造合法的语法分析树，读取变量和函数的声明，并确定其作用域即生效范围。  
- javascript执行：执行具体的代码，JavaScript引擎在执行每个函数实例时，都会创建一个执行环境和活动对象（它们属于宿主对象，与函数实例的生命周期保持一致）
函数声明在JS解析时进行函数提升，因此在同一个作用域内，不管函数声明在哪里定义，该函数都可以进行调用。而函数表达式的值是在JS运行时确定，并且在表达式赋值完成后，该函数才能调用。  
### callee属性
每一个对象都有自己的属性，而arguments有一个callee属性，返回正被执行的Function对象。
```js
function f3() {
    console.log(arguments.callee === f3); // true
}
f3('name', 'age');
```

### 基本类型和引用类型的区别和相同点
项 | 基本类型 | 引用类型
:-: | :-: | :-: 
值 | 简单的数据段 | 可能由多个值构成的对象
存储 | 值保存在变量中 | 值保存在内存中的对象
可操作 | 可以操作保存在变量中的值 | js不允许直接访问内存中的位置，即是不能直接操作对象的内存空间。实际上是操作对象的引用。  
使用方式 | 直接使用 | 动态的属性：修改其属性和方法。
复制值 | 会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上 | 将存储在变量对象中的值复制一份到新变量分配的空间中。这个值的副本是指针，指向存储在堆中的一个对象。
相同点：定义值的方式是相同的。
### 执行环境和作用域
https://github.com/mqyqingfeng/frontend-interview-question-and-answer/issues/12   
https://tylermcginnis.com/ultimate-guide-to-execution-contexts-hoisting-scopes-and-closures-in-javascript/?spm=ata.13261165.0.0.2d8e16798YR8lw
#### 作用域
词法作用域：函数的作用域是在函数定义的时候就决定了。动态作用域：函数的作用域是在函数调用的时候才决定的。js采用词法作用域。
#### 执行环境
- 执行环境：定义了变量或函数有权访问的其他数据，决定了他们各自的行为(或生命周期)。  
- 全局执行环境、函数执行环境。  
- 全局执行环境只能访问全局环境中定义的变量和函数，不能直接访问局部环境中的任何数据。
- 当代码在一个环境中执行时，会创建变量对象的一个作用域链。作用域链的用途是，保证对执行环境有权访问的所有变量和函数的有序访问。
### 每个执行上下文的三个重要属性
- 变量对象(Variable object，VO)
- 作用域链(Scope chain)
- this

### 浏览器引擎说明
浏览器内核分两个部分：渲染引擎和JS引擎，但由于JS引擎越来越独立，所以现在通常所谓的浏览器内核也就单指浏览器所采用的渲染引擎了      
渲染引擎：负责对网页语法的解释（如标准通用标记语言下的一个应用HTML、JavaScript）并渲染（显示）网页     
常见渲染引擎有Chrome、Safar采用Webkit，Firefox火狐采用Gecko，IE采用Trident。（目前Chrome开始采用Blink，IE采用Edge）   
JS引擎：单线程引擎，负责执行JS代码     
常见JS引擎有Chrome采用V8引擎，Safari采用Nitro，Firefox采用SpiderMonkey，微软采用JScript引擎    
### 了解v8引擎吗，一段js代码如何执行的
在执行一段代码时，JS引擎会首先创建一个执行栈然后JS引擎会创建一个全局执行上下文，并push到执行栈中, 这个过程JS引擎会为这段代码中所有变量分配内存并赋一个初始值（undefined），在创建完成后，JS引擎会进入执行阶段，这个过程JS引擎会逐行的执行代码，即为之前分配好内存的变量逐个赋值(真实值)。   

如果这段代码中存在function的声明和调用，那么JS引擎会创建一个函数执行上下文，并push到执行栈中，其创建和执行过程跟全局执行上下文一样。但有特殊情况，即当函数中存在对其它函数的调用时，JS引擎会在父函数执行的过程中，将子函数的全局执行上下文push到执行栈，这也是为什么子函数能够访问到父函数内所声明的变量。     

还有一种特殊情况是，在子函数执行的过程中，父函数已经return了，这种情况下，JS引擎会将父函数的上下文从执行栈中移除，与此同时，JS引擎会为还在执行的子函数上下文创建一个闭包，这个闭包里保存了父函数内声明的变量及其赋值，子函数仍然能够在其上下文中访问并使用这边变量/常量。当子函数执行完毕，JS引擎才会将子函数的上下文及闭包一并从执行栈中移除。         
最后，JS引擎是单线程的，那么它是如何处理高并发的呢？即当代码中存在异步调用时JS是如何执行的。比如setTimeout或fetch请求都是non-blocking的，当异步调用代码触发时，JS引擎会将需要异步执行的代码移出调用栈，直到等待到返回结果，JS引擎会立即将与之对应的回调函数push进任务队列中等待被调用，当调用(执行)栈中已经没有需要被执行的代码时，JS引擎会立刻将任务队列中的回调函数逐个push进调用栈并执行。这个过程我们也称之为事件循环。
#### 变量对象
变量对象是与执行上下文相关的数据作用域，存储了在上下文中定义的变量和函数声明  
在函数上下文中，我们用活动对象(activation object, AO)来表示变量对象。  
进入执行上下文时，初始化的规则:  
1. 函数的所有形参 (如果是函数上下文)  
- 由名称和对应值组成的一个变量对象的属性被创建
- 没有实参，属性值设为 undefined
2. 函数声明  
- 由名称和对应值（函数对象(function-object)）组成一个变量对象的属性被创建
- 如果变量对象已经存在相同名称的属性，则完全替换这个属性
3. 变量声明  
- 由名称和对应值（undefined）组成一个变量对象的属性被创建；
- 如果变量名称跟已经声明的形式参数或函数相同，则变量声明不会干扰已经存在的这类属性
### 闭包
https://zhuanlan.zhihu.com/p/22486908  
https://www.cnblogs.com/rubylouvre/p/3345294.html   
https://blog.csdn.net/yummy_go/article/details/50663081  
闭包是指有权访问另一个函数作用域中的变量的函数；
```js
function a() {
  let i = 0;
  function b () {
    alert(a + b)
  }
  return b;
}
let c = a();
c();
// 函数a的内部函数b被函数a外的一个变量引用的时候，就创建了一个闭包。
```
#### 使用场景
1. 闭包可以读取函数内部变量   
2. 将函数内部变量的值始终保存在内存中
3. 保护函数内的变量安全：如迭代器、生成器。
4. 在内存中维持变量：如果缓存数据、柯里化。
闭包可以运用于高阶函数或者是函数柯里化等场景。  
#### 弊端P(80、183)
IE7之前的浏览器的垃圾收集器是根据内存分配量运行的，像变量是256个，达到临界值，垃圾收集器就会运行。如果一个脚本中包含很多变量。那么在该脚本生命周期，垃圾收集器就不得不频繁运行。肯能造成内存泄漏。
### 为什么要将JS源文件的全部内容包装在一个函数中
它可以创建一个私有命名空间，从而有助于避免不同JS模块和库之间潜在的名称冲突。
### 原型链，对象，构造函数之间的联系
https://blog.csdn.net/cc18868876837/article/details/81211729
```js
function Test（）{};
const test = new Test();
// console.log(Function.__proto__);
// console.log(Function.prototype);
Function.__proto__ === Function.prototype; // 由console得出值相同，因此为规定

// var obj = {}; 
// var obj = new Object(); Function
Object.__proto__ === Function.prototype;

// test.constructor --指向--> 实例化test对象的构造函数
console.log(test.constructor === Test);

// constructor可以更改
function Test1() {
  this.a = 111;
}
test.constructor = Test1
console.log(Test1)
```
### 创建对象的方式（红P144）
- 工厂模式
- 构造函数
- 原型模式
- 组合使用构造函数模式和原型模式
- 动态原型模式
- 寄生构造函数模式
- 稳妥构造函数模式

### 检测对象属性存在于实例中还是原型中
- 实例：obj.hasOwnProperty(name);
- 原型中：!obj.hasOwnProperty(name) && (name in obj);
### DOM级别（红p6）
DOM1级的目标是映射文档结构，有两个模块组成：  
- DOM核心(DOM Core)：规定如何映射基于XML的文档结构，以便简化对文档结构中任意部分的访问和操作。
- DOM HTML：在DOM Core的基础上加以扩展，添加了针对HTML的对象和方法  
DOM2级加入了新的模块：    
DOM视图、DOM事件、DOM样式、DOM遍历和范围。  
DOM3级进一步扩展了DOM，引入了以同于方式加载和保存文档的方法。
### DOM事件的几种绑定方式
1. 在html标签中直接绑定；
2. 在js中获取到相应的dom元素后onXX绑定；
3. 在jsN中使用addEventListener()实现绑定；  
### Dom事件中target和currentTarget的区别
- target：直接的事件源（真正的事件源）是target。   
- currentTarget：经过冒泡或者捕获触发的父级的DOM元素是currentTarget。冒泡到哪个父元素，那么currentTarget就是哪个父元素,在事件处理函数中，this就是currentTarget。  
### querySelectorAll 和 getElementsByTagName区别。
项 | querySelectorAll() | getElementsByTagName()
:-: | :-: | :-:
遍历方式 | 深度优先 | 深度优先
返回值类型 | NodeList集合 | HTMLCollection集合
返回值状态 | 静态 | 动态
#### NodeList和HTMLCollection之间的关系
链接：https://www.zhihu.com/question/31576889/answer/52559370  
历史上的DOM集合接口。主要不同在于HTMLCollection是元素集合而NodeList是节点集合（即可以包含元素，也可以包含文本节点）。所以 node.childNodes 返回 NodeList，而 node.children 和 node.getElementsByXXX 返回 HTMLCollection 。  
**唯一要注意的是** querySelectorAll 返回的虽然是 NodeList ，但是实际上是元素集合，并且是静态的（其他接口返回的HTMLCollection和NodeList都是live的）。
- 事实上，将来浏览器将增加 queryAll 接口取代现在的 querySelectorAll，返回 Elements 是 Array 的子类（因而可以使用Array上的forEach、map等方法）。
历史上dom1、dom2乃至dom3标准都是分core/XML和HTML部分的。getElementsByTagName是在core里的（即XML也有的），所以不可能返回HTMLCollection。但是现在的dom标准已经不分core和html了，反映的是浏览器的实现。而现代浏览器的api的兼容起点是IE6（嗯，就是如此）。所以你可以看IE6是如何的。IE6里dom对象是没有构造器，也得不到原型。不过有个事情可以用来判断，NodeList跟HTMLCollection有个差异是前者没有namedItem()方法后者是有的。所以拿个IE6试验下即知。另外一种方式是看IE8。IE8的DOM有了constructor属性，你直接console.log()打出来看就知道了。  
- HTMLCollection是因为某些历史原因，在新一代DOM出现之前，实现HTMLCollection这个接口的集合只包含HTML元素，所以命名为HTMLCollection。
- DOM节点（node）不光包含HTML元素，还包含text node（字符节点）和comment（注释），既然HTMLCollection只包含HTML元素
#### 为什么 getElementsByTagName 比 querySelectorAll 方法快
使用getElementsByTagName方法我们得到的结果就像是一个对象的索引，而通过querySelectorAll方法我们得到的是一个对象的克隆；所以当这个对象数据量非常大的时候，显然克隆这个对象所需要花费的时间是很长的。
### 事件的三个阶段
事件捕获、目标阶段、事件冒泡
### 平时怎么解决跨域的，以及后续JSONP的原理和实现，以及cors怎么设置（head信息字段）
同源策略是一种约定，由Netscape公司1995年引入浏览器，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，浏览器很容易受到XSS、CSFR等攻击。所谓同源是指"协议+域名+端口"三者相同，即便两个不同的域名指向同一个ip地址，也非同源。 
#### 同源策略限制以下几种行为：
- Cookie、LocalStorage 和 IndexDB 无法读取，只支持同域；
- DOM和JS对象无法获得
- AJAX 请求不能发送
#### 解决方法
- jsonp（ JSON with padding）：只能发送get请求
- cors
- postMessage
- document.domain
- window.name
- location.hash
- http-proxy
- nginx
- websocket



### 说下深拷贝的实现原理? JSON.stringify,JOSN.parse这种实现的缺点
- 拷贝后两者之间不再存在共享关系  
- 拷贝之后数据类型不能发生改变，也就是需要判断是数组的时候，需要进行单独递归的遍历  
- 在继承的时候，我们通过原型属性实现原型对象属性的继承，在进行深拷贝的时候，我们首先需要提出原型对象上的属性；通过hasOwnProperty方法来进行筛选
### 尾递归的实现原理
### 什么是函数柯里化？说下JS的api中有哪些应用到了函数柯里化的实现？   
### js中bing函数和reduce方法用到了
### ES6的箭头函数中this问题，以及拓展运算符
### getBoundignClientRect获取的top和offsetTop获取的top区别
### session,cookie, sessionStorage, localstorage区别
### AMD、CMD、Commonjs的区别,以及ES6的模块化与其他几种的区别，以及出现的意义
#### 区别
https://www.zhihu.com/question/20351507/answer/14859415  
AMD 规范在这里：https://github.com/amdjs/amdjs-api/wiki/AMD  
CMD 规范在这里：https://github.com/seajs/seajs/issues/242   
https://github.com/seajs/seajs/issues/277  

1. 对于依赖的模块，AMD 是提前执行，CMD 是延迟执行。不过 RequireJS 从 2.0 开始，也改成可以延迟执行（根据写法不同，处理方式不同）。CMD 推崇 as lazy as possible.  
2. AMD 推崇依赖前置，CMD 推崇依赖就近。  

#### AMD
AMD 主要是为前端 js 的表现指定的一套规范；
AMD 是 Asynchronous Module Definition 的缩写，意思是 异步模块定义；采用的是异步的方式进行模块的加载，在加载模块的时候不影响后边语句的运行；  
AMD 也是采用 require() 语句加载模块的，但是不同于 CommonJS ，它有两个参数；require(['模块的名字']，callBack)；requireJs 遵循的就是 AMD 规范；    
AMD 的实现其实是通过 define 函数定义在闭包中，例如：define(id?: String，dependencies?: String[]，factory: Function | Object)；  
其中，id 是模块的名字，是一个可选的参数；dependencied 指定了所要依赖的模块列表，是一个数组，每个依赖的模块的输出将作为参数一次传入 factory 中；如果没有指定 dependencies 的话，那么默认的就是 ["require"，"exports"，"module"]；factory 包括了模块的具体实现，它是一个函数或者对象；如果是函数，那么它的返回值就是模块的输出接口或者值；
#### CMD
CMD 是 Common Module Definition 的缩写，是 seajs 推荐的一套规范，CMD 也是通过异步的方式进行模块的加载的，CMD 的加载是按照就近规则进行的，AMD 依赖的是前置；CMD 在加载的使用的时候会把模块变为字符串解析一遍才知道依赖了哪个模块；   
#### Commonjs
CommonJS 是主要为了 js 在后端的表现制定的，它不适合前端；
CommonJS 其实也有浏览器端的实现，原理是先将所有模块都定义好并通过 id 索引方便的在浏览器环境中进行解析；
CommonJS 是以在浏览器环境之外构建 javaScript 生态系统为目标而产生的写一套规范，主要是为了解决 javaScript 的作用域问题而定义的模块形式，可以使每个模块它自身的命名空间中执行，该规范的主要内容是，模块必须通过 module.exports 导出对外的变量或者接口，通过 require() 来导入其他模块的输出到当前模块的作用域中；目前在服务器和桌面环境中，node.js 遵循的是 CommonJS 的规范；CommonJS 对模块的加载时同步的；    
#### 意义
js之前没有模块化概念，主要命名冲突、模块依赖问题。  
- js事件执行机制，event loop， microtask, task queue;
- Ajax请求方式（XMLHttpRequest原生写法）
- 面向对象的理解



### js事件循环以及异步执行顺序
https://blog.csdn.net/cc18868876837/article/details/97107219   
https://www.bilibili.com/video/av21771455?from=search&seid=1679380112698787971   
### 如何使用 JS 创建、读取cookie
创建：document.cookie = "key1 = value1; key2 = value2; expires = date";  
读取：document.cookie  
### call、apply、bind
https://www.cnblogs.com/moqiutao/p/7371988.html    
call 和 apply 都是为了改变某个函数运行时的上下文（context）而存在的，换句话说，就是为了改变函数体内部 this 的指向。apply、call 二者而言，作用完全一样，只是接受参数的方式不太一样。   
bind()方法会创建一个新函数，称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入bind()方法的第一个参数作为 this，传入 bind() 方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。bind 就是用来绑定上下文的，强制将函数的执行环境绑定到目标作用域中去。与 call 和 apply 其实有点类似，但是不同点在于，它不会立即执行，而是返回一个函数。因此我们要想自己实现一个 bind 函数，就必须要返回一个函数，而且这个函数会接收绑定的参数的上下文。
### typeof操作符返回的数据类型
undefined, boolean, string, number, object, function
### 面向对象编程与面向过程编程的区别
- 面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候一个一个依次调用就可以了。
- 面向对象是把构成问题事务分解成各个对象，建立对象的目的不是为了完成一个步骤，而是为了描叙某个事物在整个解决问题的步骤中的行为。

### 任务队列
https://www.cnblogs.com/jiasm/p/9482443.html    
微任务：
then、process.nextTick 、promises、Object.observe、MutationObserver

### void 0 与 undefined的区别
1.undefined可以被重写    
undefined 在 ES5 中已经是全局对象的一个只读（read-only）属性了，它不能被重写。但是在局部作用域中，还是可以被重写的。
```js
(function() {
  var undefined = 10;
 
  // 10 -- chrome
  alert(undefined);
})();
 
(function() {
  undefined = 10;
 
  // undefined -- chrome
  alert(undefined);
})();
```
2.为什么选择void 0 作为undefined的替代  
void 运算符能对给定的任何表达式进行求值，然后返回 undefined。如 void (2), void (‘hello’)。并且void是不能被重写的。但为什么是void 0 呢，**void 0 是表达式中最短**的。用 void 0 代替 undefined 能节省字节。不少 JavaScript 压缩工具在压缩过程中，正是将 undefined 用 void 0 代替掉了。

### for、for in 、for of
- for：数组边界(长度)问题，遍历数组
- for in：对象（原型属性也会被遍历）、数组、字符串（不能遍历32位编码字符，只能遍历16位字符）
- for of：只能用于遍历JavaScript的内置对象，不能遍历自定义对象，数组、对象

### 严格模式
use strict 是一种 ECMAscript5 添加的（严格）运行模式，这种模式使得 Javascript 在更严格的条件下运行。

### new 操作符
在js中,new()常被用来创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例
1. 创建一个简单JavaScript空对象（即{}）；
2. 链接该对象到另一个对象 （即设置该对象的_proto_为构造函数的prototype）；
3. 执行构造函数,将构造函数内的this作用域指向1步骤中新创建的空对象{}；
4. 如果构造函数有返回值，则return 返回值,否则return 空对象obj。
### this理解
https://github.com/AwesomeDevin/blog/issues/10   
你不知道js上卷
