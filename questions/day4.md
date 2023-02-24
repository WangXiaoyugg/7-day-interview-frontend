# 速记第四天
1. 浏览器是如何渲染 UI 的？
   - 浏览器获取HTML文件，然后对文件进行解析，形成DOM Tree
   - 与此同时，进行CSS解析，生成Style Rules
   - 接着将DOM Tree与Style Rules合成为 Render Tree
   - 接着进入布局（Layout）阶段，也就是为每个节点分配一个应出现在屏幕上的确切坐标
   - 随后调用GPU进行绘制（Paint），遍历Render Tree的节点，并将元素呈现出来
   
   DOM tree是如何构建的？
     - 转码: 浏览器将接收到的二进制数据按照指定编码格式转化为HTML字符串
     - 生成Tokens: 之后开始parser，浏览器会将HTML字符串解析成Tokens
     - 构建Nodes: 对Node添加特定的属性，通过指针确定 Node 的父、子、兄弟关系和所属 treeScope
     - 生成DOM Tree: 通过node包含的指针确定的关系构建出DOM

2. 谈一下百分比布局？
   ​通过百分比单位 " % " 来实现响应式的效果。通过百分比单位可以使得浏览器中的组件的宽和高随着浏览器的变化而变化，从而实现响应式的效果。 直观的理解，我们可能会认为子元素的百分比完全相对于直接父元素，height 百分比相 对于 height，width 百分比相对于 width。 padding、border、margin 等等不论是垂直方向还是水平方向，都相对于直接父元素的 width。 除了 border-radius 外，还有比如 translate、background-size 等都是相对于自身的。
    
   **缺点**
   （1）计算困难 
   （2）各个属性中如果使用百分比，相对父元素的属性并不是唯一的。造成我们使用百分比单位容易使布局问题变得复杂。

3. 获取表单元素的方式有哪些？
   
   - 根据id获取， document.getElementById("id属性的值")
   - 根据标签名获取，document.getElementsByTagName("标签的名字");
   - 根据name获取， document.getElementsByName("name属性的值");
   - 根据类样式的名字获取，document.getElementsByClassName("类样式的名字");
   - 根据选择器获取，document.querySelector("选择器");document.querySelectorAll("选择器");

4. 谈一下浮动布局？
   
   **定义**
   浮动布局:当元素浮动以后可以向左或向右移动，直到它的外边缘碰到包含它的框或者另外一个浮动元素的边框为止。元素浮动以后会脱离正常的文档流，所以文档的普通流中的框就变的好像浮动元素不存在一样。

   **优点**
   这样做的优点就是在图文混排的时候可以很好的使文字环绕在图片周围。另外当元素浮动了起来之后，它有着块级元素的一些性质例如可以设置宽高等，但它与inline-block还是有一些区别的，第一个就是关于横向排序的时候，float可以设置方向而inline-block方向是固定的；还有一个就是inline-block在使用时有时会有空白间隙的问题


   **缺点**
   最明显的缺点就是浮动元素一旦脱离了文档流，就无法撑起父元素，会造成父级元素高度塌陷。


5. Cookie、sessionStorage、localStorage 的区别？
   **相同点**
   都存储在客户端
   都只能存储字符串类型数据

   **不同点**
   cookie数据大小不能超过4k；sessionStorage和localStorage的存储比cookie大得多，可以达到5M+
   cookie设置的过期时间之前一直有效；localStorage永久存储，浏览器关闭后数据不丢失除非主动删除数据；sessionStorage数据在当前浏览器窗口关闭后自动删除
   cookie的数据会自动的传递到服务器；sessionStorage和localStorage数据保存在本地

   **常用操作**
   sessionStorage/localStorage 只能存储字符串的数据，对于JS中常用的数组或对象却不能直接存储，通过JSON.stringify()将json数据类型转化成字符串，再存储到storage，获取数据时使用JSON.parse()将读取的字符串转换成对象即可

   **sessionStorage特点**
   新打开的标签页会复制父级的 sessionStorage，类似于深拷贝，之后 sessionStorage 的变更不会同步
   相同 url 的多个 tab 页，sessionStorage 并不会同步，也就是说它们不属于同一个 session

   **应用场景**
   标记用户与跟踪用户行为的情况，推荐使用cookie
   适合长期保存在本地的数据（令牌token），推荐使用localStorage
   敏感账号一次性登录，推荐使用sessionStorage
   存储大量数据的情况、在线文档（富文本编辑器）保存编辑历史的情况，推荐使用indexedDB（用于在客户端存储大量的结构化数据, 也支持文件/二进制大型对象blobs）


6. 行内元素、块级元素、空元素？

   | CSS                | 标签                                           | 设置宽高 | 独占一行 |
   | :----------------- | :--------------------------------------------- | :------- | :------- |
   | block块级          | h1-h6, p, table, div, ol,ul, li, form等        | 可以     | 会       |
   | inline行内         | span, a, img, input, textarea, select等        | 不可以   | 不会     |
   | inline-block行内块 | img, input,textarea, select, button,canvas,svg | 可以     | 不会     |

   空元素： br, hr, img, input, link, meta

7. em/px/rem/vh/vw 区别?
   
   - px，表示像素，所谓像素就是呈现在我们显示器上的一个个小点，每个像素点都是大小等同的
   - em是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相对于浏览器的默认字体尺寸（1em = 16px）em 的值并不是固定的，em 会继承父级元素的字体大小
   - rem，相对单位，相对的只是HTML根元素font-size的值
   - vw ，就是根据窗口的宽度，分成100等份，100vw就表示满宽，50vw就表示一半宽。（vw 始终是针对窗口的宽），同理，vh则为窗口的高度

8. vw, vh 与 百分比（%）的区别？
   - % 是基于【父元素】的宽度/高度的百分比，vw，vh是根据视窗的宽度/高度的百分比
   - 视口单位优势在于【vh】能够直接获取高度，而用 % 在没有设置 body 高度情况下，是无法正确获得可视区域的高度。
  

9. 谈一下常见的Web攻击有哪些？

   **XSS**
   XSS(跨站脚本攻击)是一种代码注入攻击。攻击者在目标网站上注入恶意代码，当用户登陆网站时就会执行这些恶意代码，这些脚本可以读取 cookie，session tokens，或者其它敏感的网站信息
   
   XSS的避免方式有
     - url参数使用encodeURIComponent方法转义
     - 尽量不是有InnerHtml插入HTML内容
     - 使用特殊符号、标签转义符。

   **CSRF**
   CSRF（跨站请求伪造：攻击者诱导用户进入第三方网站，在第三方网站中，向被攻击网站发送跨站请求。利用用户在被攻击网站已经获取的注册凭证，绕过后台的用户验证，达到冒充用户对被攻击的网站执行某项操作的目的。

   CSRF避免方式有：
      - 添加验证码
      - 使用token
        - 服务端给用户生成一个token，加密后传递给用户
        - 用户在提交请求时，需要携带这个token
        - 服务端验证token是否正确

    **SQL注入攻击**
    Sql 注入攻击，是通过将恶意的 Sql查询或添加语句插入到应用的输入参数中，再在后台 Sql服务器上解析执行进行的攻击
    Sql 注入攻击的避免方式， 对应输入的参数进行转义和编码

    **DDOS攻击**
    DDoS又叫分布式拒绝服务，其原理就是利用大量的请求造成资源过载，导致服务不可用。

    避免方式有：
       - 限制单IP请求频率。
      - 防火墙等防护设置禁止ICMP包等
      - 检查特权端口的开放

10. 谈一下对重绘和回流？
      
    **重排/回流**
    当DOM的变化影响了元素的几何信息，浏览器需要重新计算元素的几何属性，将其安放在界面中的正确位置，这个过程叫做重排。表现为重新生成布局，重新排列元素。
    布局引擎会根据各种样式计算每个盒子在页面上的大小与位置
    改变元素的位置和尺寸大小都会引发回流
    常见触发回流的属性有： 
        - width | height | margin | padding | display | border | position | overflow ;
        - clientWidth | clientHeight | clientTop | clientLeft | offsetWidth | offsetHeight | offsetTop | offsetLeft | scrollWidth | scrollHeight | scrollIntoView | scrollTo | getComputedStyle | getBoundingClientRect | scrollIntoViewIfNeeded

    **重绘**
    一个元素的外观发生改变，但没有改变布局,重新把元素外观绘制出来的过程，叫做重绘。表现为某些元素的外观被改变。
    当计算好盒模型的位置、大小及其他属性后，浏览器根据每个盒子特性进行绘制。
    常见触发重绘的属性有：color | border-(style or radius) | visibility | background | text-decoration | outline | box-shadow

    **常见触发重排和重绘的方法**
    添加、删除、更新DOM节点
    通过display: none隐藏一个DOM节点-触发重排和重绘
    通过visibility: hidden隐藏一个DOM节点-只触发重绘
    移动或者给页面中的DOM节点添加动画
    添加一个样式表，调整样式属性
    用户行为，例如调整窗口大小，改变字号，或者滚动。

    **常见避免重排/重绘的方法**
    集中改变样式，不要一条一条地修改 DOM 的样式。
    不要把 DOM 结点的属性值放在循环里当成循环里的变量。
    尽量只修改position：absolute或fixed元素，对其他元素影响不大
    使用使用 CSS 的 will-change 属性， 提升为合成层
      - 合成层的位图，会交由 GPU 合成，比 CPU 处理要快
      - 当需要 repaint 时，只需要 repaint 本身，不会影响到其他的层
      - 对于 transform 和 opacity 效果，不会触发 layout 和 paint


    **二者联系**
    『回流』必定会发生『重绘』，『重绘』不一定会引发『回流』。

     