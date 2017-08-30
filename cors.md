# 跨域

[阮一峰跨域](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)

## 为什么要跨域？

这就要提到同源策略了，所谓同源是指协议相同，域名相同，端口相同，同源的之间可以进行通信以及数据传递，数据访问。而非同源的则不行，这是为了保护用户的安全，防止恶意的网站能随意窃取数据或者利用cookie中的用户状态做一些可怕的事，毕竟提交表单是不受同源限制的。但是我们有时候需要少量的数据进行通讯，这就需要我们跨域了，比如你想获取豆瓣上的API资源就会受到阻碍。

## 不同源受到的限制

1. Cookie、LocalStorage 和 IndexDB 无法读取。
2. DOM 无法获得。
3. AJAX 请求不能发送。


## 浏览器和客户端之间的跨域(ajax)

### cors

需要在后端设置http头部Access-Control-Allow-Origin


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
