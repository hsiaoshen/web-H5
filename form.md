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


## 控件
### input控件(单标签)

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
6. placehoder
7. form:可以把一个不在form表单中的input作为form表单的input的提交，值为form表单的id
8. autofocus:设置当前文本域页面加载完了过后自动得到焦点
9. formaction:button属性,会覆盖原来的action向指定的action提交表单

### textarea(文本域)

```html
<textarea cols="列数" rows="行数">
....
</textarea>
```
### 能把div变输入框

```html
<div contenteditable></div>
```

### select控件

```html
<select size="" multiple>          //size:可视的的选项有几个
  <option selceted>选项1</option>   //selected:默认选项
  <option>选项2</option>
  <option>选项3</option>
  ...
</select>
```

### fieldset控件

用于将form中的控件进行分组，filedset没有必须或唯一的属性。legend定义标题

```html
<form action="test.php" method="post">
  <fieldset>
    <legend>Title</legend>
    <input type="radio" id="radio">
  </fieldset>
</form>
```

## jQuery关于表单的操作

1. :button --> 选中为button按钮的所有元素,包括input类型和button类型的按钮,等同于$("button, input[type='button']")
2. :checkbox --> 等同于$('[type=checkbox]'), 选择所有类型为复选框的元素。
3. :checked --> 适用于复选框,单选框和option,所有选中的元素
4. :disabled --> 选中所有被禁用的元素
5. :focus --> 获取焦点的元素
6. :input --> 选择所有 input, textarea, select 和 button 元素.
7. :file
8. :image
9. :password
10. :radio
11. :reset
12. :selected
13. :submit
14. :text
15. val()和val(value) --> 获取表单中的值或者给表单赋值
