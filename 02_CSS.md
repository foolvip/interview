
## css
### IE的怪异模型和标准浏览器的盒子模型，通过box-sizing属性控制两种盒模型的转换
参考：https://www.cnblogs.com/chengzp/p/cssbox.html   
https://www.cnblogs.com/anqwjoe/p/10428136.html   
- box-sizing应用场景
- flex布局
- 未知高度元素怎么左右垂直居中
- 水平居中、垂直居中、水平垂直居中（https://juejin.im/post/5aa252ac518825558001d5de） 
- CSS常用布局（定位布局，流布局，浮动布局，flex布局，grid布局，三栏布局中的圣杯和双飞翼 https://juejin.im/post/5aa252ac518825558001d5de ）  
- px|em|rem
- animaition和transition的相关属性，为什么推荐动画用CSS3而不是js（性能），浏览器对CSS3的加速
### 清除浮动的几种方法
- 额外标签法，<div style="clear:both;"></div>（缺点：不过这个办法会增加额外的标签使HTML结构看起来不够简洁。）
- 使用after伪类
#parent:after{
    content:".";
    height:0;
    visibility:hidden;
    display:block;
    clear:both;
    }
- 设置`overflow`为`hidden`或者auto
### 伪类与伪元素
https://segmentfault.com/a/1190000000484493
### BFC
块级格式化上下文，是一个独立的渲染区域，让处于 BFC 内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响。在同一个BFC中的两个毗邻的块级盒在垂直方向（和布局方向有关系）的margin会发生折叠。（W3C CSS 2.1 规范中的一个概念，它决定了元素如何对其内容进行布局，以及与其他元素的关系和相互作用。）  
BFC的布局规则：   
- 属于同一个 BFC 的两个相邻 Box 垂直排列；
- BOX垂直方向的距离由margin决定，属于同一个BFC的两个相邻box的margin会发生重叠；
- 每个元素的margin box的左边，与包含块border box的左边相接触（对于从左往右的格式化，否则相反）。即使存在浮动也是如此；
- BFC的区域不会与float box重叠；
- BFC就是页面上一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之也是如此。
- 计算BFC高度的时候，浮动元素也参与计算
#### 出发条件
- 根元素
- position: absolute/fixed
- float元素
- overflow !== visible
### 层叠上下文
#### 触发条件
- 根层叠上下文(html)
- position
- css3属性：flex、transform、opacity、filter、will-change、-webkit-overflow-scrolling
#### 层叠等级：层叠上下文在Z轴上的排序
- 在同一层叠上下文中，层叠等级才有意义
- z-index的优先级最高
backgound/border -> z-index为负值 -> 块级元素 -> 浮动元素 -> 行内元素 -> z-index: 0/auto -> z-index为正值

### 解释下 CSS sprites，以及你要如何在页面或网站中使用它
CSS Sprites其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的“background-image”，“background- repeat”，“background-position”的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。这样可以减少很多图片请求的开销，因为请求耗时比较长；请求虽然可以并发，但是也有限制，一般浏览器都是6个。对于未来而言，就不需要这样做了，因为有了`http2`。
### CSS 选择符有哪些？哪些属性可以继承？优先级算法如何计算？
1. id选择器（ # myid）
2. 类选择器（.myclassname）
3. 标签选择器（div, h1, p）
4. 相邻选择器（h1 + p）
5. 子选择器（ul > li）
6. 后代选择器（li a）
7. 通配符选择器（ * ）
8. 属性选择器（a[rel = "external"]）
9. 伪类选择器（a: hover, li:nth-child）  
可继承的样式： font-size font-family color, text-indent;  
不可继承的样式：border padding margin width height ; 
优先级就近原则，同权重情况下样式定义最近者为准;   
载入样式以最后载入的定位为准;  
优先级为:   
!important > id > class > tag> * > 继承 > 默认     
important 比 内联优先级高,但内联比 id 要高
### display与visibility区别
1、空间占据 2、回流与渲染 3、诛连性
### css3新特性
#### 选择器
属性选择器、结构性伪类选择器(not、first-child、nth-child、only-child、root、empty)、状态伪类选择器(hover、focus、active、disabled、checked、read-write)、兄弟元素选择器
#### 使用选择器在页面中插入内容
使用选择器插入文字、使用选择器插入图像、使用content属性插入项目编号
#### 文字相关样式
文字添加阴影、文本自动换行-word-break、使用服务端字体-web Font与@font-face属性、使用rem定义字体大小
#### 盒相关样式
盒的类型(inline-block、inline-table、list-item、none、flex)、overflow、阴影(box-shadow)、指定元素宽度和高度计算方式的box-sizing
#### 背景与边框相关的样式
background-clip指定背景显示范围、background-sizng、background-origin绘制起点   
圆角边框的绘制、图像边框(border-image)
#### css3的变形处理
transform 3D变形、对一个元素使用多种变形
#### css3的动画功能
transitions功能、animations功能
#### 布局相关样式
多栏布局、盒布局、弹性布局、calc方法
#### 媒体查询相关样式

### 响应式布局和自适应的区别：
http://www.alloyteam.com/2015/04/zi-shi-ying-she-ji-yu-xiang-ying-shi-wang-ye-she-ji-qian-tan/  
响应式网页设计是自适应网页设计的子集。响应式网页设计指的是页面的布局（流动网格、灵活的图像及媒介查询）。总体目标就是去解决设备多样化问题。响应式布局等于流动网格布局，而自适应布局等于使用固定分割点来进行布局。当固定宽度与流动宽度结合起来时，自适应布局就是一种响应式设计，而不仅仅是它的一种替代方法。
#### 响应式布局：
- 允许网页的宽度自动的调整、
- 尽量少使用绝对的宽度，多点百分比、
- 相对大小的字体、
- 流式布局，float等float的好处是，如果宽度太小，放不下两个元素，后面的元素会自动滚动到前面元素的下方，不会在水平方向overflow（溢出），避免了水平滚动条的出现、
- 选择加载css，<link rel="stylesheet" type="text/css" media="screen and (max-device-width: 400px)" href="tinyScreen.css" />，这个意思是如果屏幕宽度小于400像素（max-device-width: 400px），就加载tinyScreen.css文件。  
#### 自适应布局
是为了解决如何才能在不同大小的设备上呈现相同的网页。手机的屏幕比较小，宽度通常在600像素以下，pc的像素一般在1000像素以上，部分配置高的笔记本在2000像素以上的也有，同样的页面要显示在不同的设备上面，还要呈现出满意的效果，不是一件容易的事情。因此就有人想出了一个办法，能不能"一次设计，普遍适用"，让同一张网页自动适应不同大小的屏幕，根据屏幕的宽度，自动调节网页的内容大小，但是无论怎么样子，他们的主体的内容和布局是没有变化的。使用媒体查询方式。
响应式的概念应该覆盖了自适应，而且涵盖的内容更多。
### FFC与BFC的区别
- flexbox不支持::first-line和::first-letter这两种伪元素
- vertical-align对Flexbox中的子元素是没有效果的。
- float和clear属性对flexbox中的元素是没有效果的，也不会使子元素脱离文档流（但是对Flexbox是有效果的）
- 多栏布局在（column-*）flexbox中也是失效的，也就是说我们不能使用多栏布局在flexbox排列其下的子元素。
- flexbox下的子元素不会继承父级容器的宽。

### oocss
主要原则：分离结构和外观，分离容器和内容。

### 讲述你对reflow和repaint的理解。
https://segmentfault.com/a/1190000002629708    
https://juejin.im/post/5c6cb7b4f265da2dae511a3d#heading-6  
repaint 就是重绘，reflow 就是回流。   
严重性： 在性能优先的前提下，性能消耗 reflow 大于 repaint。   
体现：repaint是某个DOM 元素进行重绘；reflow 是整个页面进行重排，也就是页面所有DOM元素渲染。 
如何触发：style变动造成repaint和reflow。     
不涉及任何DOM元素的排版问题的变动为repaint，例如元素的 color/text-align/text-decoration 等等属性的变动。
除上面所提到的DOM元素style的修改基本为reflow。例如元素的任何涉及长、宽、行高、边框、display等style的修改。
#### 常见触发场景
- 触发repaint：  
color的修改，如color=#ddd；  
text-align 的修改，如 text-align=center；  
a:hover 也会造成重绘。  
:hover引起的颜色等不导致页面回流的style变动。     
- 触发 reflow：  
width/height/border/margin/padding 的修改，如 width=778px；
动画，:hover等伪类引起的元素表现改动，display=none 等造成页面回流；  
appendChild等DOM元素操作；  
font类style的修改；   
background 的修改，注意着字面上可能以为是重绘，但是浏览器确实回流了，经过浏览器厂家的优化，部分 background 的修改只触发 repaint，当然 IE 不用考虑；  
scroll 页面，这个不可避免；  
resize 页面，桌面版本的进行浏览器大小的缩放，移动端的话，还没玩过能拖动程序，resize 程序窗口大小的多窗口操作系统。  
读取元素的属性（这个无法理解，但是技术达人是这么说的，那就把它当做定理吧）：读取元素的某些属性（offsetLeft、offsetTop、offsetHeight、offsetWidth、scrollTop/Left/Width/Height、clientTop/Left/Width/Height、getComputedStyle()、currentStyle(in IE))；
#### 如何避免： 
- 尽可能在 DOM 末梢通过改变 class 来修改元素的 style 属性：尽可能的减少受影响的 DOM 元素。
- 避免设置多项内联样式：使用常用的 class 的方式进行设置样式，以避免设置样式时访问 DOM 的低效率。
- 设置动画元素position属性为 fixed 或者 absolute：由于当前元素从 DOM 流中独立出来，因此受影响的只有当前元素，元素 repaint。
- 牺牲平滑度满足性能：动画精度太强，会造成更多次的 repaint/reflow，牺牲精度，能满足性能的损耗，获取性能和平滑度的平衡。
- 避免使用table进行布局：table的每个元素的大小以及内容的改动，都会导致整个table进行重新计算，造成大幅度的repaint或者reflow。改用div则可以进行针对性的repaint和避免不必要的reflow。
- 避免在CSS中使用运算式：学习CSS的时候就知道，这个应该避免，不应该加深到这一层再去了解，因为这个的后果确实非常严重，一旦存在动画性的repaint/reflow，那么每一帧动画都会进行计算，性能消耗不容小觑。

### iphone10的适配
https://www.cnblogs.com/lolDragon/p/7795174.html
#### 适配方案viewprot-fit
auto: 默认   
viewprot-fit:contain; 页面内容显示在safe area内     
cover: viewport-fit:cover,页面内容充满屏幕   
```html
<meta name="viewport" content="width=device-width,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
```
#### css constant()函数
在iOS 11中的WebKit包含了一个新的CSS函数constant()，以及一组四个预定义的常量：safe-area-inset-left, safe-area-inset-right, safe-area-inset-top和 safe-area-inset-bottom。当合并一起使用时，允许样式引用每个方面的安全区域的大小。   