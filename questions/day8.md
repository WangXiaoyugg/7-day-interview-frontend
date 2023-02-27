# 速记第8天 - react

1. 你的项目为什么选择AntDesign UI库？
     
    **特性**
    提炼自企业级中后台产品的交互语言和视觉风格
    设计价值观：确定性、意义感、生长性和自然

    开箱即用的高质量 React 组件

    使用 TypeScript 开发，提供完整的类型定义文件
    可以享受组件属性输入建议, 定义检查的功能

    全链路开发和设计工具体系

    数十个国际化语言支持:提供 React 组件 ConfigProvider 用于全局配置国际化文案

    深入每个细节的主题定制能力

    **兼容性**
    现代浏览器和 IE8 以上
    支持服务器渲染
    支持 Electron
    可选 Ant Design Mobile 支持移动端
    支持 Preact / React / React Native
   
    **社区支持**
    Ant Desgin of Angular / Ant Design of Vue
    完整文档 / 大厂背书 / 众多用户，容易找到解决方案

2. AntDesign 如何实现虚拟列表？
     - 通过 react-window 虚拟滚动方案引入 VariableSizeGrid
     - 构建 renderVirtualList 函数组件，接收 `rawData, { scrollbarSize, ref, onScroll } `作为参数
         - rawData 表格原始数据源，用于计算总高度、行数和显示数据
         - scrollbarSize 当竖直滚动条显示时，设置内容区域的宽度减去滚动条宽度
         - ref 用于外部直接访问和操作 VariableSizeGrid，处理水平垂直滚动和数据重置
         - onScroll 当表格水平垂直滚动时，同步虚拟列表水平垂直滚动
     - 引入 AntDesign 的 Table 组件，设置 components 属性为 {{ body: renderVirtualList }}

3. AntDesign 如何实现固定表头时，列头和内容对不齐怎么办？
     - 为 Table 设置 scroll={{ y: 任意数值 }} 开启固定表头
     - AntDesign 使用两个的 div 分别嵌套 table 实现固定表头效果 
       - 每个 table 的 table-layout 布局算法为 fixed，即列宽度由表格宽度和列宽度设定
       - 需要手动指定每一列的宽度，以确保上下两个 table 的每一列宽度同步
       - 如果内容可能出现超长连续字段（长数字和长单词），在 columns 属性新增
           - textWrap: 'word-break'
           - ellipsis: true