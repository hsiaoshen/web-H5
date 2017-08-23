# ajax的使用

## 什么是ajax?

是一种用于创建快速动态网页的技术,通过和后台进行少量的数据,在不重新加载页面的情况下实现页面更新.

## 为什么要用ajax?(需要和传统的作对比)

传统的js技术:要想和服务器进行数据交互,首先通过form表单,点击submit按钮向指定Url通过get或post方法向服务器请求,然后等待响应,页面加载

ajax:用户不用感觉页面刷新,而且页面数据还更改了


### 优点
1. 提升了用户体验
2. 优化了服务器和客户端数据之间的传输,减少了请求次数
3. ajax引擎在客户端,减少了大用户量下的服务器加载

### 缺点

破坏了浏览器后退按钮的行为

## 核心对象

XMLHttpRequest对象,是一种支持异步请求的技术,通过它可以使用js向服务器发出请求并处理相应,同时不会阻塞用户

## 最大特点

实现动态不刷新(局部刷新),在不重新加载整个页面的基础上数据更新,使得WEB应用更好的回应用户的动作

## 数据形式

XML数据或者字符串或者json,jsonp数据

##  XMLHttpRequest对象在IE和Firefox中创建方式有没有不同？

有，IE中通过new ActiveXObject()得到，Firefox中通过new XMLHttpRequest()得到

## 用到了什么技术?

1. Ajax（Asynchronous JavaScript + XML）的定义
2. 基于web标准（standards-based presentation）XHTML+CSS的表示；
3. 使用 DOM（Document Object Model）进行动态显示及交互；
4. 使用 XML 和 XSLT 进行数据交换及相关操作；
5. 使用 XMLHttpRequest 进行异步数据查询、检索；
6. 使用 JavaScript 将所有的东西绑定在一起。

## ajax的具体使用


### 原生的ajax

第一步:创建XMLHttpRequest对象
```html
function createXHR(){
    if (typeof XMLHttpRequest != "undefined"){
        return new XMLHttpRequest();
    } else if (typeof ActiveXObject != "undefined"){
         if (typeof arguments.callee.activeXString != "string"){
            var versions = [ "MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
            "MSXML2.XMLHttp"], i, len;
            for (i=0,len=versions.length; i < len; i++){
                try {
                    new ActiveXObject(versions[i]);
                    arguments.callee.activeXString = versions[i];
                    break;
                } catch (ex){
                    //跳过
                }
            }
        }
        return new ActiveXObject(arguments.callee.activeXString);
     } else {
            throw new Error("No XHR object available.");
    }
}

var xhr =  createXHR();

```

第二步:open方法(不会发送请求,只是准备一个请求以备发送)

```html
xhr.open('method',url,async?)

参数: 第三个参数是不是异步
```

第三步:send(发送请求,但是分get和post2种情况)

```html
xhr.send(null);  //若get或head方法,设置主体为null
// xhr.send('string');
// xhr.send(new Blob());
// xhr.send(new Int8Array());
// xhr.send({ form: 'data' });
// xhr.send(document);

```
**get:最常用于向服务器查询某些信息**

**辅助编码函数**
```html
function addURLParam(url, name, value){
    url += url.indexOf('?') == -1 ? '?' : '&';
    url += encodeURIComponent(name) + "=" + encodeURIComponent(value);
    return url;
}
```

```html
xhr.send(null);
```

**post:通常用于向服务器发送应该被保存的数据**

默认情况下，服务器对 POST 请求和提交 Web 表单的请求并不会一视同仁。因此，服务器端必须有程序来读取发送过来的原始数据，并从中解析出有用的部分。不过，我们可以使用 XHR 来模仿表单提交：首先将 Content-Type 头部信息设置为 application/x-www-form-urlencoded，也就是表单提交时的内容类型，其次是以适当的格式创建一个字符串。
```html
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");   //和get最重要的区别
xhr.send(序列化的表单数据字符串); //格式"name=value&name=value&name=value"
```

第四步:接受相应

相关属性:
1. responseText：作为响应主体被返回的文本。
2. responseXML：如果响应的内容类型是“text/xml”或“application/xml”，这个属性中将保存包含着响应数据的 XML DOM 文档。
4. status：响应的 HTTP 状态。
5. statusText： HTTP 状态的说明。

**readState属性(表示请求响应过程的当前活动阶段)**:

只要 readyState 属性的值由一个值变成另一个值，都会触发一次 readystatechange 事件。

* 0：未初始化。尚未调用 open()方法。
* 1：启动。已经调用 open()方法，但尚未调用 send()方法。
* 2：发送。已经调用 send()方法，但尚未接收到响应。
* 3：接收。已经接收到部分响应数据。
* 4：完成。已经接收到全部响应数据，而且已经可以在客户端使用了

```html
xhr.onreadystatechange = function(){
    if (xhr.readyState == 4){
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
            alert(xhr.responseText);
        } else {
            alert("Request was unsuccessful: " + xhr.status);
        }
    }
};
```







### JQuery的ajax操作 --> 返回jqXHR对象

#### 你用的什么框架?

JQuery

#### 具体操作

**$.get**
```html
$.get(url,data,function(data){
    alert(data)
});

/*
参数:
1. url: 请求的url
2. data: 向服务器传的数据
3. callback:请求成功执行的回调函数
*/
```
**$.post**
```html
$.post(url,data,function(data){
    alert(data)
});

/*
参数:
1. url: 请求的url
2. data: 向服务器传的数据
3. callback:请求成功执行的回调函数
*/
```

**$.ajax**
```html
$.ajax(
url:请求的url,
type:请求的方式(一般有get,post,put,head),
async:是否异步(True或False),
cache:是否缓存该页面(默认true,若dateType为jsonp或者script,默认为false),
contentType:发送到服务器内容编码类型(默认值: "application/x-www-form-urlencoded"),
context:这个对象用于设置 Ajax 相关回调函数的上下文(就是要操作的元素,此时success回调函数的this指向该元素),
data:data,
dataType:预期服务器返回的数据类型(如果不指定，jQuery 将自动根据 HTTP 包 MIME 信息来智能判断,若jsonp格式,则能解决跨域问题),
timeout:设置请求超时(毫秒),
success:请求成功的回调函数,
error:请求失败的回调函数,
complete:请求完成执行的回调函数(无论成功或失败都执行),global:是否触发全局 AJAX 事件(默认值: true。设置为 false 将不会触发全局 AJAX 事件，如 ajaxStart 或 ajaxStop 可用于控制不同的 Ajax 事件),
).done(funcion(){})
```
