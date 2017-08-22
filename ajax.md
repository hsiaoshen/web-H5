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
xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
var form = document.getElementById("user-info");
xhr.send(序列化的表单数据字符串); //格式"name=value&name=value&name=value"
```



### JQuery的ajax操作

#### 你用的什么框架?

JQuery

#### 具体操作

