# 跨域

[阮一峰跨域](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)
[掘金](https://juejin.im/entry/590c257761ff4b006238bdc9)

## 为什么要跨域？

这就要提到同源策略了，所谓同源是指协议相同，域名相同，端口相同，同源的之间可以进行通信以及数据传递，数据访问。而非同源的则不行，这是为了保护用户的安全，防止恶意的网站能随意窃取数据或者利用cookie中的用户状态做一些可怕的事，毕竟提交表单是不受同源限制的。但是我们有时候需要少量的数据进行通讯，这就需要我们跨域了，比如你想获取豆瓣上的API资源就会受到阻碍。

## 不同源受到的限制

1. Cookie、LocalStorage 和 IndexDB 无法读取。
2. DOM 无法获得。
3. AJAX 请求不能发送。


## 浏览器和客户端之间的跨域(ajax)

### cors

需要在后端设置http头部Access-Control-Allow-Origin

#### 前端代码

1. 
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>cors</title>
</head>
<body>

<!-- 该代码运行于 127.0.0.1:80 端口 -->
	
	<script type="text/javascript">

        //ie8兼容性代码
		function createCORSRequest(method, url){
			var xhr = new XMLHttpRequest();
			if ("withCredentials" in xhr){
				console.log("XMLHttpRequest...");
				xhr.open(method, url, true);
			} else if (typeof XDomainRequest != "undefined"){
				console.log("XDomainRequest...");
				vxhr = new XDomainRequest();
				xhr.open(method, url);
			} else {
				xhr = null;
			}
			return xhr;
		}

		var request = createCORSRequest("get", "http://127.0.0.1:8000/test");
		if (request){
			request.onload = function(){
				//收到跨域ajax响应之后的数据responseText
				console.log(request.responseText);
			};

			request.onerror = function(){
				console.log("request error .....");
			}
			request.send();
		}

</script>
</body>
</html>
```
2. 
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>cors</title>
</head>
<body>

<!-- 该代码运行于 http://127.0.0.1:80 端口 -->

<script type="text/javascript">

/*
实现ajax跨域：只需要访问的后端允许即可，允许需要后端设置 http头部 Access-Control-Allow-Origin
*/

var request = new XMLHttpRequest();
request.open("get", "http://127.0.0.1:8000/test");

request.onload = function(){
  console.log(request.responseText);
};

request.send();

</script>
</body>
</html>
```
3.jQuery.ajax
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>

    <!--  此处的 "/" 不是你操作系统根目录，是你的服务器的根目录  -->
    <script src="/jquery-3.0.0.js" charset="utf-8"></script>
    <script type="text/javascript">

    $.ajax({
      url: "http://127.0.0.1:8000/test",
      method: "get"
    }).done(function(data){
      console.log(data);
    });

    </script>

  </body>
</html>
```

#### 后端是nodejs编写的

```js
var fs = require("fs");
var http = require("http");
var url = require("url");

var data = "{'name': 'lisi', 'age': 10 }";

http.createServer(function(request, response){
    var path = url.parse(request.url).path;
    if (path == "/test"){

      //设置允许客户端的跨域ajax请求
      response.setHeader("Access-Control-Allow-Origin", "*" );
      response.writeHead(200, {"Content-type": "text/plain"});
      response.end(data);
    }
}).listen(8000);

console.log("监听 127.0.0.1:8000 ....");
```

### JSONP

使用跨域要求必须只能是GET请求

#### 使用script标签带着回调函数

前端
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>


 <script>
  //跨域请求的数据就是 data
 	function handler(data){
 		console.log("handler被调用了", data);
 	}

 </script>

  <!-- 当前的页面运行于 127.0.0.1:80 -->
  <!--
   jsonp只能发送 get 请求
   script的特点时一旦加载成功就会立刻执行
  -->

 <script type="text/javascript" src="http://127.0.0.1:8000?callback=handler"></script>

</body>
</html>
```
后端
```js

var fs = require("fs");
var http = require("http");
var url = require("url");

http.createServer(function(req, res){
	 var queryObj = url.parse(req.url, true).query;
	 /*
	    queryObj = {"callback": "handler"}
	 */

	 console.log(queryObj);

	 fs.readFile("./test.json", function(err, data){
		 //"handler({name:'lisi', age: 10})"
		 res.write(queryObj.callback+ "(" + data  + ")");
		 res.end();
	 });


}).listen(8000);

console.log("监听 127.0.0.1:8000 ...");
```

#### jQuery的ajax跨域

前端
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>

    <script src="/jquery-3.0.0.js" charset="utf-8"></script>
    <script type="text/javascript">

    //jsonp被指定的调用函数
    function handler(data){
      console.log("回调函数handler被调用",data);
    }

    //发送的请求  http://127.0.0.1:8000?callback=handler
    $.ajax({
      url:"http://127.0.0.1:8000/",
      method: "get",
      dataType: "jsonp",
      jsonp: "callback",
      jsonpCallback: "handler"
    }).done(function(data, textStatus, jqXHR){
      //此处的data为 服务端返回的函数调用(handler)的参数部分
      console.log(data);
    });

    </script>

  </body>
</html>
```
后端

```js

var fs = require("fs");
var http = require("http");
var url = require("url");

http.createServer(function(req, res){
	var queryObj = url.parse(req.url, true).query;
	var obj = JSON.stringify({name: 'lisi'});

	res.write(queryObj.callback + "(" + obj + ")");
	res.end();

}).listen(8000);

console.log("监听 127.0.0.1:8000 ...");
```

## 页面之间的跨域

### cookie

比如淘宝和天猫，共用同一个账号和登录状态，但是不是一个域名，如何做到呢？

我猜测是设置了document.domain共享同一个Cookie

#### document.domain的具体操作（只适用于Cookie和iframe）

***
举例来说，A网页是‘http://w1.example.com/a.html’，B网页是‘http://w2.example.com/b.html’，那么只要设置相同的document.domain，两个网页就可以共享Cookie。

```
document.domain = 'example.com';
```

另外，服务器也可以在设置Cookie的时候，指定Cookie的所属域名为一级域名，比如.example.com。
```
Set-Cookie: key=value; domain=.example.com; path=/
```
这样的话，二级域名和三级域名不用做任何设置，都可以读取这个Cookie。
***
### iframe(前提在一个域上，可以把文件放在apache上进行测试)

#### window.name(需要监听)

父页面
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>window.name</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .f {
            width: 1000px;
            height: 300px;
            margin: 100px auto;
            border: 1px solid #a94442;
        }

        #frame {
            width: 100%;
            height: 100%;
        }

        h1 {
            text-align: center;
        }

    </style>
</head>
<body>


  <!--
   前提：使用 iframe时
   window.name可以实现页面通信，但是需要监听window.name的变化
 -->

  <script type="text/javascript">
  var data = {
    name: '外部页面'
  };

  window.name = JSON.stringify(data);
  </script>

  <div class="f">
    <iframe id="frame" src="./test-iframe.html" frameborder="0"></iframe>
  </div>

<script>

    window.onload  = function () {
        var frame = document.querySelector("#frame");

        //frame.contentWindow 是得到嵌套页面的window
        frame.contentWindow.document.querySelector("h1").innerHTML = '我被该成红色';
        frame.contentWindow.document.querySelector("h1").style.color = 'red';

        /*
         通过iframe的window.name属性可以访问iframe窗口传递的数据
         缺点： 需要监听iframe中window.name的值变换
         */
        console.log(JSON.parse(frame.contentWindow.name));

    };
</script>


</body>
</html>
```

iframe窗口页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h1>我是 iframe ...</h1>

<script>
    var data = {
        name: '嵌套页面'
    };

    //window.parent 拿到父页面的window
    console.log(JSON.parse(window.parent.name));

    //window.name传递的是字符串，可以json的方法
    window.name = JSON.stringify(data);

</script>

</body>
</html>
```
#### hash 片段识别符(也需要实时监听)

父页面
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>window.location.hash</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .f {
            width: 1000px;
            height: 300px;
            margin: 100px auto;
            border: 1px solid #a94442;
        }

        #frame {
            width: 100%;
            height: 100%;
        }

        h1 {
            text-align: center;
        }

    </style>
</head>
<body>

<h1 id="h">我是源窗口</h1>

<div class="f">
    <iframe id="frame" src="./test-iframe.html" frameborder="0"></iframe>
</div>

<script>

/*
前提：页面之间是iframe的父子关系
使用hash进行通信，使用hashchange事件即可监听自己hansh的变化
通信方式：需要设置对方的location.href来改变hash(其他href中的数据不能变，只改hash)
数据会附带到地址栏，所有数据量有限
*/
    window.onload  = function () {
        var h = document.querySelector("#h");
        var frame = document.querySelector("#frame");


        //frame.contentWindow是嵌套页面的window
        frame.contentWindow.document.querySelector("h1").style.color = 'red';


        var originUrl = frame.src;//test-iframe.html
        var num = 0;

        setInterval(function () {
            //改变子窗口的hash,通过hash传递数据
            frame.contentWindow.location.href = originUrl + '#' + num++;
        }, 1000);

        //监听自己的hash的变化
        window.onhashchange = function () {
            h.innerHTML = window.location.hash;
        };

    };
</script>


</body>
</html>
```

iframe窗口页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h1 id="h">我是 iframe ...</h1>

<script>
    var h = document.querySelector("#h");

    //window.parent 是打开当前页面的父窗口
    var originUrl = window.parent.location.href;

    var num = 0;

    //监听自己的hash变化
    window.onhashchange = function () {
        h.innerHTML = window.location.hash;
        window.parent.location.href = originUrl + '#' + num++;
    };

</script>

</body>
</html>
```
#### window.postMessage

父页面
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>利用window.postMessage</title>
    <style>

        h1 {
            text-align: center;
        }

    </style>
</head>
<body>

<h1>window.open 打开新页面</h1>
<button id="btn">点击打开</button>

<script>

/*
跨域，跨窗口通信
window.open
xxx.postMessage
xxx.onmessage
*/

    window.name = "father";
    var btn = document.querySelector("#btn");
    var timer = null;

    //监听其他页面发来的数据
    window.onmessage = function (e) {
      console.log(e.data);
    };

    btn.onclick = function (e) {
        clearInterval(timer);

        /*window.open,用于获得一个要打开的页面window
         第二个参数，用于指定新窗口的window.name
          返回值为 新窗口的window
         */
        var newWindow = window.open("./test-iframe.html", "son");
        newWindow.onload = function () {
            //新窗口加载完毕之后，可以直接操作新窗口的元素
            newWindow.document.querySelector("h1").style.color = 'red';
        };


        var num = 0;
        setInterval(function(){
            //利用postMessage给打开的页面发送数据
            //第二个参数是给指定域名的页面发送数据
            newWindow.postMessage(num++, "*");
        },1000);

    };
</script>


</body>
</html>
```

iframe窗口页面
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h1>我是 iframe ...</h1>

<script>
  //  console.log("----", window.name);
  //  console.log("---", window.opener);//输出该页面的打开者

    window.onmessage = function (e) {
        console.log(e.source);// 发送方的window, 源
        console.log(e.origin);// 发送方的http://xxxx.xxx.com:8080
        console.log(e.data);//接收到的数据

        //给发送发发送数据
        e.source.postMessage("I am son", e.origin);
    };
</script>

</body>
</html>
```
