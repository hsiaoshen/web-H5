# 2017-8-14

## 相关知识点

1. 页面引用CSS样式 
2. 对浏览器的认识

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

2. 对浏览器的认识?

***
主流浏览器的内核

1. Trident内核：IE,MaxThon,TT,The World,360,搜狗浏览器等
2. Gecko内核:Mozilla
3. Presto内核:Opera7及以上
4. Webkit内核：Safari,Chrome等
***
