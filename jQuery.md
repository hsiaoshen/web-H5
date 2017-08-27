# JQuery

## 如果$与其他库的冲突怎么解决？



有以下几种方法:

前提：首先引用写在其他库的后面,jQuery.noConflict() --> 移交$控制权，使其他可以使用$

1. 直接使用jQuery来代替$使用，就是写起来不方便
2. 传参式:
```scrpipt
jQuery.noConflict();
jQuery(function($){
});
```
3. 定义新的快捷方式

```script
var $j = jQuery.noConflict();
$j(function(){})
```

4. 匿名函数式:好处是能让$让多个库使用(还能避免js库导入顺序不清楚时产生的冲突)

```script
jQuery.noConflict();
(function($){
})(jQuery)；

```
### 实现原理

```script
var
// Map over jQuery in case of overwrite
_jQuery = window.jQuery,

// Map over the $ in case of overwrite
_$ = window.$,

jQuery.extend({
    noConflict: function( deep ) {
            if ( window.$ === jQuery ) {
                window.$ = _$;
            }

            if ( deep && window.jQuery === jQuery ) {
                window.jQuery = _jQuery;
            }

            return jQuery;
        }
});
```

描述:

在jQuery加载的时候，通过事先声明的_jQuery变量获取到当前window.jQuery，通过_$获取到当前window.$。

通过jQuery.extend()把noConflict挂载到jQuery下面。所以我们在调用的时候都是jQuery.noConflict()这样调。

在调用noConflict()时做了2个判断，

第一个if，把$的控制权交出去。

第二个if，在noConflict()传参的时候把，jQuery的控制权交出去。

最后noConflict()返回jQuery对象，用哪个参数接收，哪个参数将拥有jQuery的控制权。


## $的作用

是jQuery的简写，是代码书写简单，优雅。常见作用有:

1. 利用选择器选择DOM元素
2. 是功能函数前缀
3. 解决window.onload函数的冲突
4. 创建DOM元素

## script标签的属性

1. async  表示立即下载该脚本，但不妨碍页面中的其他操作(比如：下载其他资源或等待加载其他脚本)，只对外部文件有效。
2. defer 表示脚本可以延迟到文档完全被解析和显示后再执行。只对外部文件有效。

## $(function(){})和 $(document).ready()的作用？

保证页面结构加载完毕后再执行js代码

## $(document).ready() 和 window.onload()的区别

1. window.onload必须等到页面内包括图片的所有元素加载完毕后才能执行。$(document).ready()是DOM结构绘制完毕后就执行，不必等到加载完毕。 
2. window.onload不能同时编写多个，如果有多个window.onload方法，只会执行一个。$(document).ready()可以同时编写多个，并且都可以得到执行
3. window.onload没有简化写法，$(document).ready(function(){})可以简写成$(function(){})

注意: 如果需要所有资源要加载完毕就要用到$(window).load(function() {}),既能在所有资源加载完毕后再执行js代码，又能编写多个


## jquery的$(document).ready()和onload的加载顺序

IE只有在页面不是嵌入frame中的情况下才和Firefox等一样，先执行$(document).ready()的内容，再执行原来的onload方法。对于嵌入frame中的页面，也只是绑定在load事件上执行，所以自然是在原来的onload绑定的方法执行之后才轮到$(document).ready()的内容



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


### 通过位置选择元素

1. :only-child --> 返回所有没有兄弟节点的元素
2. :even --> 匹配上下文中的偶数元素
3. :odd --> 匹配上下文中的奇数元素
4. :eq(n) --> 从0开始计数，第n个元素
5. :nth-child(n) --> 从1计数，第n个子元素

### 过滤器

1. :animated	选择处于动画状态的元素
2. :button	选择按钮元素(包括input[type=submit], input[type=reset], input[type=button]和button)
3. :checkbox	选择复选框元素(input[type=checkbox])
4. :contains(food)	选择包含文本food的元素
5. :disabled	选择处于禁用状态的元素
6. :enabled	选择处于启用状态的元素
7. :file	选择文件输入元素(input[type=file])
8. :has(selector)	选择至少包含一个匹配指定选择器的元素的元素
9. :header	选择标题元素, 比如<h1> ~ <h6>
10. :hidden	选择隐藏元素
11. :image	选择图片输入元素(input[type=image])
12. :input	选择表单元素(input, select, textarea, button)
13. :not(selector)	选择不匹配指定选择器的元素
14. :parent	选择有子节点(包含文本)的元素, 空元素除外
15. :password	选择口令元素(input[type=password])
16. :radio	选择单选框元素(input[type=radio])
17. :reset	选择重置按钮元素(input[type=reset])或者(button[type=reset])
18. :selected	选择列表中处于选中状态的元素
19. :submit	选择提交按钮 (input[type=submit])或者(button[type=submit])
20. :text	选择文本输入框元素 (input[type=text])
21. :visible	选择可见的元素

### DOM操作

#### 创建元素

1. $('<p>')  --> 创建了一个p元素
2. document.createElement("span") 
3. .clone()  --> 深度复制所有匹配的元素集合，包括所有匹配元素、匹配元素的下级元素、文字节点
  
#### 添加子元素或者后代元素

##### .append(),.prepend(),.appendTo(),.prependTo()

在选中的元素集合的内部的最后添加一个子元素

注意：如果是在该元素的内部最后选中本来存在的元素添加，那么相当于从原来位置移动走了，而不是赋复制

可以使用回调函数动态插入元素

```html
$('div').append(function(index, html){
  return ($('p'));
});

//index: 是元素的索引值.
//html: 是元素的内容.
```
#### 封装

##### .wrap(),.wrapAll(),.wrapInner()

区别：

wrap()是在满足集合的每个元素外面包裹一层HTML结构；wrapAll()是在满足集合的所有元素外面包裹一层HTML结构；wrapInner()是在满足集合的每个元素的内容外部包裹一层HTML结构(最内层只有一个元素)

#### .after('要插入的元素'),.insertAfter('目标元素')

在一个元素后面加一个兄弟元素(多个元素时每个元素后面加一个兄弟元素)

#### .before(),.insertBefore()

在一个元素前面加一个兄弟元素


#### .replaceWith()和.replaceAll()

$(traget).replaceWith(新元素) --> 目标元素用新元素来替代

.replaceAll() --> 新元素替换目标元素
