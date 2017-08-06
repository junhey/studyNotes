# 前端面试

###  前言

这里会写这篇文档的初衷

###  面试注意点

这里会写面试过程中的注意点


###  前端面试知识点

这里主要写一些面试总结题


> 欢迎star和提交issues

###  更新时间:2016-10-29



- [git命令](https://github.com/junhey/studyNotes/blob/master/Front-end/Markdown.md)

- [Markdown常用](https://github.com/junhey/studyNotes/blob/master/Front-end/Markdown.md)

- [Json知识](https://github.com/junhey/studyNotes/blob/master/Front-end/JSON.md)


- [.htaccess设置](https://github.com/junhey/studyNotes/blob/master/PHP/htaccess.md)

- [php常见问题](https://github.com/junhey/studyNotes/blob/master/PHP/php.md)

- [redis学习](https://github.com/junhey/studyNotes/blob/master/PHP/Redis.md)


- [开发流程](https://github.com/junhey/studyNotes/blob/master/PHP/Development_process.md)

- [CodeIgniter](https://github.com/junhey/studyNotes/blob/master/PHP/CodeIgniter.md)


# Front-end-Developer-Interview

根据github上的面试题整理 ​前端工程师面试问题

前端问答

Q:从浏览器地址输入url到显示页面的步骤（以HTTP为例）

A:
1. 浏览器输入URL
2. 浏览器查看缓存，如果请求资源在缓存中并且最新，跳转到转码步骤，如果请求资源没有缓存，发起新请求，其中检查是否最新是通过两个HTTP头进行控制Expires和Cache-control
3. 浏览器解析URL获取协议，主机端口，path
4. 浏览器组装一个HTTP（GET）请求报文
5. 浏览器获取主机ip地址，其中经的过程：浏览器缓存-本机缓存-hosts文件-路由器缓存-ISP DNS缓存-DNS递归查询(可能负载均衡导致每次ip不一样)
6. 打开一个socket与目标ip地址，端口建立TCP链接，三次握手
7. TCP链接建立后发送HTTP请求
8. 服务器接受请求并解析，将请求转发到服务程序，如虚拟主机使用HTTP Host头部判断请求的服务程序
9. 服务端检查HTTP请求头是否包含缓存验证信息，如果验证缓存信息是最新的，返回304等对应的状态码
10. 处理程序读取完整的请求并准备HTTP响应，可能需要查询数据库等操作
11. 服务器响应报文通过TCP连接发送回浏览器
12. 浏览器接收到HTTP响应，然后根据情况选择关闭TCP连接或者保留重用，关闭TCP连接的四次握手
13. 浏览器检查响应状态码是否为1XX，3XX，4XX，5XX这些情况与2XX处理不同
14. 如果资源可缓存，进行缓存
15. 对响应进行解码（gzip压缩）
16. 根据资源类型决定如果处理
17. 解析HTML文档，构建DOM树，下载资源，构造CSSOM树，执行js脚本
18. 显示页面（HTML解析过程中会逐步显示页面）


Q:前端需要注意的seo

A:
1. 合理的title\description\keywords，搜索对三个的权重逐个减少
2. 语义化的HTML代码，符合W3C规范，语义化的代码可以让搜索引擎容易理解网页
3. 重要的内容HTML代码放前面，搜索引擎抓取HTML顺序是从上往下的，有的搜索引擎对抓取的长度有限制。
4. 重要内容不要用js输出，爬虫不会执行js来获取内容。
5. 少用iframe，搜索引擎不会抓取iframe中的内容
6. 非装饰性的图片必须加alt（img图片内容的等价描述），title（提高附加的advisory information，通常鼠标滑过元素上显示）
7. 提高网站速度，网站速度是搜索引擎排序的一个重要指标

Q:web开发中会话跟踪有哪些方法

A:
1. cookie
2. session
3. URL重写
4. 隐藏input
5. ip地址

- HTML

Q：HTML5新增了哪些内容或API，使用过哪些

A：
页面可见性API--page Visbility
全屏API --full Screen
获取MediaAPI--getUserMedia
电池API --battery
资源预加载API--link Prefetching
页面可见性API--Page Visibility 

使用方法见为[w3c](https://www.w3.org)

Q：input和textarea的区别

A：
<input>是一个单行输入框，有value属性，但是它不能自动换行。
<textarea>是一个多行输入框，，没有value属性，但是它能自动换行。

Q：用一个div模拟textarea的实现

A：
使用contenteditable标签，设置contenteditable=“true"
contenteditable属性兼容所有浏览器（IE6之前的版本是否兼容未测试）

Q：移动设备忽略将页面中的数字识别为电话号码的方法
A：<meta name="format-detection" content="telephone=no">

- CSS

Q：左右布局：左边定宽、右边自适应，不少于3种方法

A：
1、固定宽度区浮动，自适应区不设宽度而设置margin
2、固定宽度区使用绝对定位，自适应区仍然设置margin
3、对自适应宽度区同时使用margin和left



Q：CSS3用过哪些新特性

A：
CSS3 选择器（Selector）
@Font-face 特性、
Word-wrap & Text-overflow 样式
Text-decoration
多列布局（multi-column layout）
边框和颜色，颜色支持透明度（color, border）
渐变效果（Gradient）
阴影（Shadow）和反射（Reflect）效果
盒子模型
Transitions, Transforms 和 Animation

Q：BFC、IFC
A：
BFC(Block formatting context)直译为"块级格式化上下文"。它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

BFC布局规则：
内部的Box会在垂直方向，一个接一个地放置。
Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
BFC的区域不会与float box重叠。
BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
计算BFC的高度时，浮动元素也参与计算

哪些元素会生成BFC?
根元素
float属性不为none
position为absolute或fixed
display为inline-block, table-cell, table-caption, flex, inline-flex
overflow不为visible

Q：对栅格的理解

A：
栅格系统能自动根据当前设备的屏幕分辨率，横向分配出等宽的单元格，可以做到移动自适应。

Q：水平居中，垂直居中的实现方式
A：
1. margin:0 auto
2. 绝对定位，left为50%，定宽，margin-left为负宽度的一半
3. 改变块级元素的display为inline类型，然后设置text-align:center来实现居中效果

Q：1像素边框的问题

A：
1. 最简单的解决办法，就是用图片做边框，只是修改颜色不太方便。
2. transform:scale 使用伪类 :after 或者 :before 创建 1px 的边框，然后通过 media 适配不同的设备像素比，然后调整缩放比例，从而实现一像素边框
3. viewport  网页的内容都渲染在 viewport 上，所以设备像素比的差异，直接影响的也是 viewport 的大小通过 js 获取到设备像素比，然后动态添加 <meta> 标签 

- JavaScript
Q：前端安全问题：CSRF和XSS
A：


Q：项目中使用过哪些优化方法
A：

Q：优化中会提到缓存的问题，问：静态资源或者接口等如何做缓存优化
A：

Q：页面DOM节点太多，会出现什么问题？如何优化？
A：

Q：图片懒加载
A：

Q：实现页面加载进度条
A：

Q：事件委托
A：

Q：实现extend函数
A：

Q：为什么会有跨域问题及其解决方式
A：

Q：jsonp原理、postMessage原理
A：


Q：实现拖拽功能，比如把5个兄弟节点中的最后一个节点拖拽到节点1和节点2之间
A：

Q：动画：setTimeout何时执行，requestAnimationFrame的优点
A：

Q：手写parseInt的实现：要求简单一些，把字符串型的数字转化为真正的数字即可，但不能使用JS原生的字符串转数字的API，比如Number()
A：

Q：编写分页器组件的时候，为了减少服务端查询次数，点击“下一页”怎样能确保还有数据可以加载（请求数据不会为空）？
A：

Q：ES6新增了哪些特性，使用过哪些，也有当场看代码说输出结果的
A：

Q：require.js的实现原理（如果使用过webpack，进一步会问，两者打包的异同及优缺点）
A：


Q：promise的实现原理，进一步会问async、await是否使用过
A：


Q：JS模块化的实践
A：

Q：实现gulp的功能
A：

Q：使用前端框架（angular/vue/react）带来哪些好处，相对于使用jQuery
A：

Q：vue双向数据绑定的实现
A：
VueJS 则使用 ES5 提供的 Object.defineProperty() 方法，监控对数据的操作，从而可以自动触发数据同步。并且，由于是在不同的数据上触发同步，可以精确的将变更发送给绑定的视图，而不是对所有的数据都执行一次检测。
数据与视图的绑定与同步，最终体现在对数据的读写处理过程中，也就是 Object.defineProperty() 定义的数据 set、get 函数中

Object.defineProperty()

语法：
Object.defineProperty(obj, prop, descriptor)

参数说明：
obj：必需。目标对象
prop：必需。需定义或修改的属性的名字
descriptor：必需。目标属性所拥有的特性

返回值：
传入函数的对象。即第一个参数obj

设置的特性总结：
value: 设置属性的值
writable: 值是否可以重写。true | false
enumerable: 目标属性是否可以被枚举。true | false
configurable: 目标属性是否可以被删除或是否可以再次修改特性 true | false

Q：单页应用，如何实现其路由功能
A：




Q：Vue.js与其他框架的区别？

A：
1.与angularjs的区别
相同点：
都支持指令：内置指令和自定义指令。
都支持过滤器：内置过滤器和自定义过滤器。
都支持双向数据绑定。
都不支持低端浏览器。
不同点：
1.AngularJS的学习成本高，比如增加了Dependency Injection特性，而Vue.js本身提供的API都比较简单、直观。
2.在性能上，AngularJS依赖对数据做脏检查，所以Watcher越多越慢。
Vue.js使用基于依赖追踪的观察并且使用异步队列更新。所有的数据都是独立触发的。
对于庞大的应用来说，这个优化差异还是比较明显的。
2.与React的区别
相同点：
react采用特殊的JSX语法，Vue.js在组件开发中也推崇编写.vue特殊文件格式，对文件内容都有一些约定，两者都需要编译后使用。
中心思想相同：一切都是组件，组件实例之间可以嵌套。
都提供合理的钩子函数，可以让开发者定制化地去处理需求。
都不内置列数AJAX，Route等功能到核心包，而是以插件的方式加载。
在组件开发中都支持mixins的特性。
不同点：
React依赖Virtual DOM,而Vue.js使用的是DOM模板。React采用的Virtual DOM会对渲染出来的结果做脏检查。
Vue.js在模板中提供了指令，过滤器等，可以非常方便，快捷地操作DOM。


正在更新中...
欢迎star