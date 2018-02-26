# 关于select的使用

使用select实现一些功能

## 2个select对应位置联动

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>select</title>
	<style>
		#domain, #email-suffix {
			width: 100px;
			/*height: 100px;*/
		}
		#email-suffix {
			font-size: 12px;
			padding: 1px 0;
		}
	</style>
</head>
<body>
	<select id="domain" onchange="Ld(this,document.all.emailSuffix)">
		<option value="YMTC">YMTC</option>
		<option value="XMC" >XMC</option>
	</select>

	<select id="emailSuffix" onchange="Ld(this,document.all.domain)">
		<option value="@YMTC.com">@YMTC.com</option>
		<option value="@XMC.com">@XMC.com</option>
	</select>
	<script>
		function Ld (obj, obj2){
			 obj2.options[obj.selectedIndex].selected=true;
		}
	</script>
</body> 
</html>
```
技术要点：
1. document.all的使用--> 获取当前页面的所有元素集合
2. this的使用
3. document.all获取该页面的id或者name元素:document.all.xxx
4. 关于selectedIndex属性:返回的是选中元素的位置序号，若是多选则返回选中的第一个
