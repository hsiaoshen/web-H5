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
