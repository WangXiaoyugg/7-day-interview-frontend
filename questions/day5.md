# 速记第五天
1. 如何使用 rem 或 viewport 进行移动端适配？
   
   **rem适配原理**
   改变了根元素的font-size在不同设备上占据的css像素的个数
   rem适配的优缺点
   优点：没有破坏理想视口
   缺点：px值转换rem太过于复杂(下面我们使用less来解决这个问题)

   **viewport适配的原理**
   viewport适配方案中，每一个元素在不同设备上占据的css像素的个数是一样的。但是css像素和物理像素的比例是不一样的，等比的
   viewport适配的优缺点
   在我们设计图上所量取的大小即为我们可以设置的像素大小，即所量即所设
   缺点破坏理想视口


2. 元素水平垂直居中？
   **给定宽高**
   absolute + 负margin
   absolute + margin auto
   absolute + calc

   **不确定宽高**
   absolute + transform
   line-height
   table/css-table
   flex
   grid
   
   **兼容性方案**
   PC端有兼容性要求，宽高固定，推荐absolute + 负margin
   PC端有兼容要求，宽高不固定，推荐css-table
   PC端无兼容性要求，推荐flex
   移动端推荐使用flex


3. call, apply, bind 三者的区别？
   **相同点**
   都是改变this指向的；
   第一个参数都是this要指向的对象；
   都可以利用后续参数传参

   **不同点**
   call和bind的参数是依次传参，一一对应的， 但apply只有两个参数，第二个参数为数组；
   call和apply都是对函数进行直接调用，而bind方法返回的仍是一个函数；

4. 前端性能优化？
    - 减少http请求数
      - 合并图片。当图片较多时，可以合并为一张大图，从而减少http请求数。
      - 合并压缩css样式表和js脚本
      - 充分利用缓存
    - 图片优化
      - 尽可能的使用PNG格式的图片，它相对来说体积较小
      - 图片的延迟加载，也叫做懒加载
    - 使用cdn
    - 开启gzip
    - 构建优化 (tree-shaking, Scope hoisting, Code-splitting)

5. CSS 预处理器 Sass、Less、Stylus 的区别?
   **什么是CSS预处理器?**
   CSS预处理器是一种语言用来为CSS增加一些变成的特性，无需考虑浏览器兼容问题，例如你可以在CSS中使用变量，简单的程序逻辑、函数等在编程语言中的一些基本技巧，可以让CSS更加简洁，适应性更强，代码更直观等诸多好处

   **基本语法区别**
   Sass是以.sass为扩展名，Less是以.less为扩展名，Stylus是以.styl为扩展名
   Sass 变量必须是以$开头的，然后变量和值之间使用冒号（：）隔开，和css属性是一样的。 Less 变量是以@开头的，其余sass都是一样的。 Stylus 对变量是没有任何设定的，可以是以$开头或者任意字符，而且变量之间可以冒号，空格隔开，但是在stylus中不能用@开头

6. 谈一下JS中的this?
      - 普通函数调用：通过函数名()直接调用：this指向全局对象window（注意let定义的变量不是window属性，只有window.xxx定义的才是。即let a =’aaa’; this.a是undefined）

      - 构造函数调用：函数作为构造函数，用new关键字调用时：this指向新new出的对象

      - 对象函数调用：通过对象.函数名()调用的：this指向这个对象

      - 箭头函数调用：箭头函数里面没有 this ，所以永远是上层作用域this（上下文）

      - apply和call调用：函数体内 this 的指向的是 call/apply 方法第一个参数，若为空默认是指向全局对象window。

      - 函数作为数组的一个元素，通过数组下标调用的：this指向这个数组

      - 函数作为window内置函数的回调函数调用：this指向window（如setInterval setTimeout 等）

7. AJAX 原理？
   异步的JavaScript 和XML，可以在不重新加载整个网页的情况下，与服务器交换数据，并且更新部分网页
   通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用JavaScript来操作DOM而更新页面

   **流程**
   创建 Ajax的核心对象 XMLHttpRequest对象
   通过 XMLHttpRequest 对象的 open() 方法与服务端建立连接
   构建请求所需的数据内容，并通过XMLHttpRequest 对象的 send() 方法发送给服务器端
   通过 XMLHttpRequest 对象提供的 onreadystatechange 事件监听服务器端你的通信状态
   接受并处理服务端向客户端响应的数据结果
   将处理结果更新到 HTML页面中

8. 清除浮动的几个方式？
   - 给父元素末尾添加一个空元素，并设置成清除浮动，即：`<div style="clear:both;"></div>`
      - 优点：通俗易懂，易于掌握
      - 缺点：添加了无意义标签，不易于后期维护，违背了结构和表现分离的标准

   - 给父元素添加 overflow：auto;

   - 让父元素也浮动

      - 缺点：影响整体页面布局，若父元素也有父元素呢？总不能一直浮动到body吧？

   - 使用after伪元素,给父元素添加一个类，来添加一个看不见的块元素，以实现清除浮动。

   - 最优解
     - 首先我们说一个CSS的概念——BFC块级格式上下文，简单来说就是只要样式或方法触发了BFC就可以防止高度塌陷.

9. html dom 的 event 事件?
   - onblur：失去焦点
   - onfocus:元素获得焦点。
   - onload：一张页面或一幅图像完成加载
   - 鼠标事件
     - onmousedown 鼠标按钮被按下。
     - onmouseup 鼠标按键被松开。
     - onmousemove 鼠标被移动。
     - onmouseover 鼠标移到某元素之上。
     - onmouseout 鼠标从某元素移开。
     - onclick: 点击事件
   - 键盘事件：
     - onkeydown 某个键盘按键被按下。
     - onkeyup 某个键盘按键被松开。
     - onkeypress 某个键盘按键被按下并松开。
   - 选择和改变
     - onchange 域的内容被改变。
     - onselect 文本被选中。
   - 表单事件：
     - onsubmit 确认按钮被点击。
     - onreset 重置按钮被点击。

10. 输入 URL 回车后发生了什么?
   检查缓存、先解析URL、然后DNS域名解析、再发起HTTP请求建立TCP连接、服务端响应返回页面资源进行渲染、然后断开TCP连接”

   **详细过程**
   - （找）DNS解析 -> 寻找哪台机器上有你需要资源 根据网址找IP
   - TCP连接 -> 客户端和服务器，TCP作为其传输层协议
   - 发送HTTP请求 -> HTTP报文是包裹在TCP报文中发送的 请求行，请求报头，请求正文
   - 服务器处理请求并返回HTTP报文 -> 状态码,响应报头和响应报文。
   - 浏览器解析渲染页面 -> 浏览器在收到HTML,CSS,JS文件后依次渲染
   - 连接结束 -> 断开TCP连接 四次挥手




