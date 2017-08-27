# JQuery

[jQuery中文文档手册](http://www.css88.com/jqapi-1.9/)

## 什么是JQuery？

答： jQuery是一个高效，精简且功能丰富的js库。对js代码进行了封装，提供接口便于使用而且兼容众多浏览器，这让文档操作和ajax以及遍历等更加简单，代码简易优雅

## 为什么要用它？

因为jQuery是一个开源的轻量级框架，兼容性强，功能丰富。它有强大的选择器，出色的DOM操作的封装，有可靠的事件处理机制(jQuery在处理事件绑定的时候相当的可靠)
和简洁完善的ajax(需要考虑复杂浏览器的兼容性和XMLHttpRequest对象的创建和使用的问题)。最重要的是，它的理念是我比较赞同的，写的少做的多。

## 能做什么

1. 取得文档中的元素
2. 修改页面的外观
3. 对页面事件的处理
4. 大量插件在页面中的运用
5. 与Ajax技术的完美结合
6. 为页面添加动态效果：为了实现某种交互式行为,设计者也必须向用户提供视觉上的反馈，如渐进进出等
7. 简化常见的JavaScript任务:对数据结构的操作

## 二种引入jQuery的方式

1. 下载好jQuery文件，使用<script>引入
  
```html
  <script language="javascript" type="text/javascript"
src="js/jquery.js" > </script>
```

2. 使用CDN
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>

## 基本使用

### 选择器

1. .find() --> 查询后代元素
2. .next() --> 同级相邻的下一个元素
3. .prev() --> 同级的上一个元素
4. .prevAll() --> 同级的上面所有元素
5. .siblings() --> 同级的所有兄弟元素

### 正则匹配

1. ^ --> 从开头开始匹配
2. $ --> 从结尾开始匹配



