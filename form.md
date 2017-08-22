# 表单

包括表单控件,表单域和提示信息

## 表单域

```html
<form action="xxx/xxx.cgi" method="get" name="form1">
  <input type="text" name="name" value=""/>
  ...
</form>
```
1. action: 用于指定接收并处理表单数据的服务器程序的url地址
2. method: 用于设置表单数据的提交方式,get/post
3. name: 用于定义指定表单的名称,以便区分同一个页面的多个表单

## input控件(单标签)

```html

<input type="input类型" .../>
```
1. type:
***
text,password,radio,checkbox,button,submit,reset,hidden

file - 选择文件(multiple--多选,accept='image/gif'-- 设置选择文件限制)

image - 图形提交的按钮

email - 限定输入内容为邮箱地址，表单提交时会校验格式

url - 限定输入内容为URL，表单提交时会校验格式

number - 限定输入内容为数字，表单提交时会校验格式

range - 数值范围选择器

Date Pickers - 日期时间选择器-------样式不能修改，移动端用的比较多，因为移动端显示的是系统的时间或日期选择器

1.date - 选取日、月、年

2.month - 选取月、年

3.week - 选取周和年

4.time - 选取时间（小时和分钟）

5.datetime - 选取时间、日、月、年，浏览器兼容性不好，效果等同于datetime-local

6.datetime-local - 选取本地时间、日、月、年

search - 搜索域，语义化，表示定义搜索框

***

2. checked: 默认选择那个
3. disabled: 控件禁止
4. readonly:只读
5. maxlength:可输入的最大值

## textarea(文本域)

```html
<textarea cols="列数" rows="行数">
....
</textarea>
```
## 能把div变输入框

```html
<div contenteditable></div>
```

## select控件

```html
<select size="" multiple>          //size:可视的的选项有几个
  <option selceted>选项1</option>   //selected:默认选项
  <option>选项2</option>
  <option>选项3</option>
  ...
</select>
```
