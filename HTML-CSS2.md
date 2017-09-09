# 2017-8-14

## 相关知识点

1. 页面引用CSS样式 
2. 对浏览器的认识
3. 关于表格的跨行跨列

## 具体详解

1.页面引用CSS

页面引用CSS包括行内添加定义style属性值,页面头部内嵌调用和外面链接调用.

外部引用包括:link引用和@import,但是有一定的区别
***
1. 写法上:

link:

```html
<link rel="stylesheet" rev="stylesheet" href="CSS文件" type="text/css" media="all" />
```
@import:

```html
<style type="text/css" media="screen">   
@import url("CSS文件");   
</style>
```

2. link可以引用除CSS以外的其他资源,而@import只能加载CSS
3. link在加载页面的同时加载CSS,而@import在页面加载完后再加载CSS
4. link是XHTML标签，无兼容问题；@import是在CSS2.1提出的，低版本的浏览器不支持
5. link支持使用Javascript控制DOM去改变样式；而@import不支持。
***

link标签的作用:(1)加载css(2)优化:rel='dns-prefetch(dns预解析),prefetch(资源预加载)‘(3)加载logo



2. 对浏览器的认识?

分为shell + 内核。Shell是指浏览器的外壳：例如菜单，工具栏 等。主要是提供给用户界面操作，参数设置等等。它是调用内核来实现各种功能的。内核才是浏览器的核心。内核是基于标记语言显示内容的程序或模块。

浏览器内核包括:渲染引擎(layout engineer或Rendering Engine)和JS引擎.

渲染引擎负责取得网页的内容(HTML、XML、图像等等)、整理讯息(例如加入CSS等)，以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。 所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。

JS引擎(v8)：解析和执行javascript来实现网页的动态效果。 最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。
***
主流浏览器的内核

1. Trident内核：IE,MaxThon,TT,The World,360,搜狗浏览器等
2. Gecko内核:Mozilla
3. Presto内核:Opera7及以上
4. Webkit内核：Safari,Chrome等.WebKit的优势在于高效稳定，兼容性好，且源码结构清晰，易于维护。
***

3.表格跨行跨列:colspan和rowspan
