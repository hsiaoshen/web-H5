# sass

是一种CSS预处理器，可以在其中使用函数，变量，逻辑判断等，然后翻译成正常的CSS文件，可以使CSS更简洁，适应性强，易于维护和修改

## 安装和使用

1. 如果你使用的是Windows,你可能首先需要安装Ruby
2. gem install sass
3. sass input.scss output.css 编译生成css文件
4. sass --watch input.scss:output.css 监视文件改动并自动编译更新css
5. sass --watch 源文件目录 : 生成文件目录(路径不能为中文)

## 语法

### 文件名后缀

sass有两种后缀名文件：一种后缀名为sass，不使用大括号和分号；另一种就是我们这里使用的scss文件，这种和我们平时写的css文件格式差不多，使用大括号和分号

### 导入

导入scss文件：

1. 如果使用 @import 'xx.scss' --> 会合并成一个css文件
2. 如果使用 @import url('xx.scss') --> 不会合并一个文件

导入css文件： 导入的css文件不会合并到编译后的文件中，而是以@import方式存在。

### 注释

1. 多行(/* */)  --> 在css中不会显示
2. 单行注释(//)  --> 会编译到css文件中


### 变量（定义后可在全局使用）

sass的变量必须是$开头，后面紧跟变量名，而变量值和变量名之间就需要使用冒号(:)分隔开（就像CSS属性设置一样），如果值后面加上!default则表示默认值。

默认值会被同一个变量的其他值覆盖掉，默认变量的价值在进行组件化开发的时候会非常有用。

#### 多变量(list,使用nth($val,$index),index从1开始)

一维数据
```scss
$p: 5px 10px 20px 30px;

.one{
  font-size: nth($p,2);  //10px
}
```

二维数据

```scss
$ptwo:5px 10px,15px 20px;

.two{
  font-size: nth(nth($ptwo,2),1);   //15px
}
```
#### 键值对(map )

```scss
$headings: (h1: 2em, h2: 1.5em, h3: 1.2em);
@each $header, $size in $headings {
  #{$header} {
    font-size: $size;
  }
}
```
### 嵌套

#### 选择器嵌套(& 代表父元素选择器)

```html
//sass style
//-------------------------------
#top_nav{
  line-height: 40px;
  text-transform: capitalize;
  background-color:#333;
  li{
    float:left;
  }
  a{
    display: block;
    padding: 0 10px;
    color: #fff;

    &:hover{
      color:#ddd;
    }
  }
}

//css style
//-------------------------------
#top_nav{
  line-height: 40px;
  text-transform: capitalize;
  background-color:#333;
}  
#top_nav li{
  float:left;
}
#top_nav a{
  display: block;
  padding: 0 10px;
  color: #fff;
}
#top_nav a:hover{
  color:#ddd;
}

```
#### 属性嵌套

```scss
.fakeshadow {
  border: {
    style: solid;
    left: {
      width: 4px;
      color: #888;
    }
    right: {
      width: 2px;
      color: #ccc;
    }
  }
}
```

#### 跳出选择器嵌套(跳出所有上级选择器嵌套) @at-root

1. 单个选择器嵌套跳出

```scss
.parent-2 {
  color:#f00;
  @at-root .child {
    width:200px;
  }
}
```
2. 多个选择器嵌套跳出

```scss
.parent-1 {
  color:#f00;
  @at-root {
  .child1 {
    width:100px;
  }
  .child2{
    height:500px;
  }
}
}
```
#### @at-root 和&的结合使用

```html
.child{
    @at-root .parent &{
        color:#f00;
    }
}

//css style
//-------------------------------
.parent .child {
  color: #f00;
}
```
### 混合 @mixin(使用@include 名字  --> 解析是通过拷贝形式)

sass中使用@mixin声明混合，可以传递参数，参数名以$符号开始，多个参数以逗号分开，也可以给参数设置默认值。声明的@mixin通过@include来调用。建议传参数使用，无参数采用%号继承

#### 无参数

```scss
@mixin center-block {
    margin-left:auto;
    margin-right:auto;
}
.demo{
    @include center-block;
}
```
#### 1个参数

```scss
@mixin opacity($opacity:50) {
  opacity: $opacity / 100;
  filter: alpha(opacity=$opacity);
}
//不输入参数，使用默认值
.demo{
@include opacity;
}
// 传参数
.demo1{
  @include opacity(80);
}
```
#### 多个参数

注意：
1. 若传参数时有的没有传参该值为默认值
2. 若传参个数多于设定参数个数会出错


```scss
@mixin horizontal-line($border:1px dashed #ccc, $padding:10px){
    border-bottom:$border;
    padding-top:$padding;
    padding-bottom:$padding;  
}
.imgtext-h li{
    @include horizontal-line(1px solid #ccc);
}
.imgtext-h--product li{
    @include horizontal-line($padding:15px);
}
```

#### 多组参数

多组参数在参数名后面加3个点


#### @mixin 和@content的结合使用

```scss
@mixin max-screen($res){
  @media only screen and ( max-width: $res )
  {
    @content;
  }
}

@include max-screen(480px) {
  body { color: red }
}
```
@include加载了@media,而且用引入的样式替换了@content

### 继承
sass中，选择器继承可以让选择器继承另一个选择器的所有样式，并联合声明。使用选择器的继承，要使用关键词@extend，后面紧跟需要继承的选择器。


#### @extend

用来继承其他选择器的样式

#### 占位选择器 %

这种选择器的优势在于：如果不调用则不会有任何多余的css文件，避免了以前在一些基础的文件中预定义了很多基础的样式，然后实际应用中不管是否使用了@extend去继承相应的样式，都会解析出来所有的样式。占位选择器以%标识定义，通过@extend调用。

PS:在@media中暂时不能@extend @media外的代码片段

### 函数

```scss
@function 函数名($变量名)
{
}
```
#### 常用颜色函数

以lighten减淡和darken加深为最，其调用方法为lighten($color,$amount)和darken($color,$amount)


### @if和@else

### 三目运算

语法为：if($condition, $if_true, $if_false) 。三个参数分别表示：条件，条件为真的值，条件为假的值。

### for循环

for循环有两种形式，分别为：@for $i from through 和@for $var from to 。$i表示变量，start表示起始值，end表示结束值，这两个的区别是关键字through表示包括end这个数，而to则不包括end这个数。
