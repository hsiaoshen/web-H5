# HTTP

## 对HTTP的认识


## 可能遇到的问题

### 当在地址栏中输入url接下来发生什么？


### get和post的区别有那些？

1. 向服务器提交数据的方式不同:

get: 把数据附在URL上发送(就是把数据放置在HTTP协议头中)，url和数据之间用‘？’隔开，参数之间用‘&’连接，
如果数据是英文字母/数字，原样发送，如果是空格，转换为+，如果是中文/其他字符，则直接把字符串用BASE64加密

post: 数据放在http包的包体中

2. 安全性问题：

post比get安全性高，毕竟get是明码传输，数据显示在地址栏中，很容易类似账号密码会被窃取

3. 传送的数据长度不同：

get:其实数据长度也没有限制，只是数据是附在URL后面的，浏览器对URL长度的支持度不同

post：数据长度没有限制，受限制也是受服务器处理程序的能力限制

4. 在服务器端获取不同：

get：request.QueryString

post： request.Form

