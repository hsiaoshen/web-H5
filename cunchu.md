# 存储

## cookie 和 session

[详解](http://www.cnblogs.com/yunian/articles/5736066.html)

### cookie

1. 浏览某个网站时，一些数据会保存在浏览器端
2. 安全性:虽然不安全，但是可以加密
3. 可以在浏览器禁止，一般很少这么做
4. 数量有限制，一个站点一般20个，单个保存的数据不能超过4k。
5. cookie分为永久和暂时:
***
永久:需要设置失效时间，这样会保存在硬盘中。下次再访问该网站的时候，浏览器先检查有没有 cookie，如果有的话，就读取该 cookie，然后发送给服务器，直到超过设置的失效时间。 存储在硬盘上的Cookie可以在不同的浏览器进程间共享，比如两个IE窗口。

暂时:不设置过期时间,就是会话cookie,浏览器会话期的cookie，关闭标签页cookie就会消失，一般保存在内存中
***
### session

1. 把用户数据存放在服务器端，用在页面之间进行数据传递
2. 当用户请求一个页面时，系统将自动创建一个Session;退出应用程序或关闭服务器时，该Session撤销
3. 通过唯一的session_id进行识别,一般用于确定用户是否登录
4. 唯一的session_id是保存在浏览器的cookie上的,若是浏览器一旦禁用了cookie,那么session也失效了
5. session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能考虑到减轻服务器性能方面，应当使用COOKIE。
6. session很容易失效,用户体验很差，安全性好
7. 原理:
***
会在客户端请求中查找session_id,若存在，直接拿session_id直接拿来检索使用;若不存在，会为该客户端创建session_id,然后在响应时返回session_Id存在浏览器客户端中
***

#### express中是session使用

安装：

```shell
$ npm i express-session --save
```
在app.js中进行设置：

```js
app.use(session({
  store: session 的存储方式，默认存放在内存中，也可以使用 redis，mongodb 等,
  resave: 即使 session 没有被修改，也保存 session 值，默认为 true,
  saveUninitialized: false,
  secret:通过设置的 secret 字符串，来计算 hash 值并放在 cookie 中，使产生的 signedCookie 防篡改,
  rolling:每个请求都重新设置一个 cookie，默认为 false,
  cookie: {         // 设置存放 session id 的 cookie 的相关选项
      maxAge: 1000 * 60 * 30
  }
}));
```

## sessionStorage

##  localStorage
