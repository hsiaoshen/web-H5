# jQuery的事件处理

## 浏览器事件

### .scroll()

使用场合:当用户在元素内执行了滚动操作，就会在这个元素上触发scroll事件。它适用于window对象，但也可以是可滚动frames与CSS overflow属性设置为scroll的元素（或auto时，元素的显示高度小于其内容高度）。

1. 绑定:$('div').scroll(function(){})
2. 触发:$('div').scroll()   --> 触发的是已经绑定了scroll事件的元素


## 文档加载

### holdready 暂缓或回复ready的执行

jQuery.holdReady( hold )   --> hold是布尔类型

注意:为了延迟 ready 事件，首先要调用 $.holdReady(true)。当 ready 事件准备执行时，再调用 $.holdReady(false)。要求是每设置一次true就要调用false才会ready的执行

### ready


## 事件的绑定和移除

### .on()  绑定

```
.on( events [, selector ] [, data ], handler(eventObject) )

```
参数:

1. events:一个或多个空格分隔的事件类型和可选的命名空间，或仅仅是命名空间,比如click
2. selector:一个选择器字符串，用于过滤出被选中的元素中能触发事件的后代元素（this就是指向该后代元素）。如果选择器是 null 或者忽略了该选择器，那么被选中的元素总是能触发事件。
3. data:交给处理函数的参数
4. handle(eventobject) --> 若是为了阻止浏览器的默认行为，直接写false

### .off()  移除

1. .off() --> 移除选定元素的所有事件
2. .off( events [, selector ] [, handler ] ) --》 移除了handler的绑定事件
3. $("body").off("click", "p", foo);   --> 移除绑定事件的指定处理函数foo
4. $("p").off( "click", "**" )    -->   移除绑定事件的所有处理函数

### .on 只触发一次的绑定

和.on差不多，就是绑定的事件只会触发一次
