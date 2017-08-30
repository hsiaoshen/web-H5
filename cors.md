# 跨域

[阮一峰跨域](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)

## 为什么要跨域？

这就要提到同源策略了，所谓同源是指协议相同，域名相同，端口相同，同源的之间可以进行通信以及数据传递，数据访问。而非同源的则不行，这是为了保护用户的安全，防止恶意的网站能随意窃取数据或者利用cookie中的用户状态做一些可怕的事，毕竟提交表单是不受同源限制的。但是我们有时候需要少量的数据进行通讯，这就需要我们跨域了，比如你想获取豆瓣上的API资源就会受到阻碍。

## 不同源受到的限制

1. Cookie、LocalStorage 和 IndexDB 无法读取。
2. DOM 无法获得。
3. AJAX 请求不能发送。


## 浏览器和客户端之间的跨域




## 页面之间的跨域

### 关于cookie的资源共享

比如淘宝和天猫，共用同一个账号和登录状态，但是不是一个域名，如何做到呢？

我猜测是设置了document.domain共享同一个Cookie

#### document.domain的具体操作（只适用于Cookie和iframe）

***
举例来说，A网页是http://w1.example.com/a.html，B网页是http://w2.example.com/b.html，那么只要设置相同的document.domain，两个网页就可以共享Cookie。

```
document.domain = 'example.com';
```
***
