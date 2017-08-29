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

1. 把用户数据存放在服务器端

## sessionStorage

##  localStorage
