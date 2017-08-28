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

### .one 只触发一次的绑定

和.on差不多，就是绑定的事件只会触发一次

### .triggerHandler()和.trigger()

共同点:都能触发自定义事件

区别：
1. 前者触发时不会触发事件的默认行为，比如表单提交，后者会触发
2. .trigger() 会影响所有与 jQuery 对象相匹配的元素，而 .triggerHandler() 仅影响第一个匹配到的元素。
3. 使用 .triggerHandler() 触发的事件，并不会在 DOM 树中向上冒泡。 如果它们不是由目标元素直接触发的，那么它就不会进行任何处理。
4. .triggerHandler() 返回最后一个处理的事件的返回值。如果没有触发任何事件，会返回 undefined。与普通的方法返回 jQuery 对象(这样就能够使用链式用法)相反

#### .trigger()向事件中传数据

1. 向事件中传入任意数据
```
$("p").click( function (event, a, b) {
// when a normal click fires, a and b are undefined
// for a trigger like below a refers to "foo" and b refers to "bar"
 
} ).trigger("click", ["foo", "bar"]);
```
2. 通过event对象传递数据
```
var event = jQuery.Event("logged");
event.user = "foo";
event.pass = "bar";
$("body").trigger(event);
```

3. 键值对传递

```
$("body").trigger({
type:"logged",
user:"foo",
pass:"bar"
 
});
```

## 表单事件

### .blur()

失去焦点后触发，不带参数可以手动触发

### .change()

一个元素的值改变的时候将触发change事件。

适用于:input元素，textarea和select元素。
 
注意：
1. 对于下拉选择框，复选框和单选按钮，当用户用鼠标作出选择，该事件立即触发
2. 对于其他类型的input元素，该事件触发将推迟，直到元素失去焦点才会触发。
3. 使用JavaScript改变输入元素的值，例如.val(),将不会触发该事件

### .focus()

不加参数，直接触发元素上的的focus事件

使用:
1. 模拟百度，当页面加载完毕后输入框获得焦点

```
$(document).ready(function(){
  $("#login").focus();
});
```
2. 阻止输入框输入内容

```
$("input[type=text]").focus(function(){
  $(this).blur();
})
```
### .select()

当用户在一个元素中进行文本选择时，这个元素上的select事件就会被触发。此事件只能用在<input type="text"> 和<textarea>。

## 键盘事件

.keydown(),.keypress(),.keyup()

区别:前面2者当键盘按下去的时候就触发了，后面的当键盘按下去再松开时才会触发

## 鼠标事件

### .contextmenu()

 当在一个元素上点击鼠标的右键时,contextmenu事件被发送到这个元素上,但在显示的上下文菜单(右键菜单)之前。 这时上下文菜单键被按下，该事件在html元素上被触发。 任何HTML元素都可以接受此事件。
