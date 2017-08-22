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

### JQuery的ajax操作

#### 你用的什么框架?

JQuery

#### 具体操作

