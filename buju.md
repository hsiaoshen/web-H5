# 布局


## 两栏自适应布局

### 使用伸缩盒子

思路：有一个设置了flex的父盒子，其中2个子盒子，左盒子设置固定宽高，同时设置缩小因子flex-shrink为0，这是因为缩小因子默认为1，会影响到左盒子，右盒子设置扩展因子flex-grow为1

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>两栏布局(左固定，右适应)</title>
  </head>
  <style media="screen">
    #main{
      display: flex;
    }
    .left{
      width: 200px;
      height: 500px;
      background-color: red;
      flex-shrink: 0;
    }
    .right{
      background-color: blue;
      flex-grow: 1;
      overflow: hidden;
    }
  </style>
  <body>
    <div id="main">
      <div class="left">左边</div>
      <div class="right">右边</div>
    </div>
  </body>
</html>
```


### 使用浮动

思路：父盒子设置width：100%和左浮动，左子盒子设置固定宽高并左浮动，右子盒子设置overflow：hidden形成BFC格局

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>两栏布局(左固定，右适应)</title>
  </head>
  <style media="screen">
  #main{
    background-color: green;
    float: left;
    width: 100%;
}
.left{
    background-color: red;
    height: 500px;
    width: 200px;
    float: left;
}
.right{
    background-color: blue;
    overflow: hidden;//形成BFC
}
  </style>
  <body>
    <div id="main">
      <div class="left">左边</div>
      <div class="right">右边</div>
    </div>
  </body>
</html>
```
### 使用定位

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>两栏布局(左固定，右适应)</title>
  </head>
  <style media="screen">
    #main{
      position: relative;
      width: 100%;
      background-color: green;
    }
    .left{
      width: 200px;
      height: 500px;
      position: absolute;
      background-color: red;
    }
    .right{
      background-color: blue;
      margin-left: 200px;
      overflow: hidden;
    }
  </style>
  <body>
    <div id="main">
      <div class="left">左边</div>
      <div class="right">的说说大家发空间是否可使肌肤的空间的关键是来得及电视剧市场价是当初就仨的处境房间爱上打开附件是打开房间打开大幅度</div>
    </div>
  </body>
</html>
```


## 三栏布局（左右固定，中自适应）

### 浮动篇

思路：父盒子设置左浮动和宽为100%，左子盒子设置固定宽高和左浮动，右子盒子设置固定宽高和右浮动，中间的盒子设置超出隐藏，注意的是html中顺序是先左右再中中

```html
#main{
    background-color: green;
    float: left;
    width: 100%;
}
.left{
    background-color: red;
    height: 500px;
    width: 200px;
    float: left;
}
.center{
    background-color: blue;
    overflow: hidden;
}
.right{
    background-color: red;
    height: 500px;
    width: 200px;
    float: right;
}
<div id="main">
    <div class="left">左边</div>
    <div class="right">右边</div>
    <div class="center">中间</div>
</div>
```

### 伸缩篇

```html
    #main{
      display: flex;
    }
    .left,.right{
      width: 200px;
      height: 500px;
      flex-shrink: 0;
    }
    .left{
      background-color: red;
    }
    .center{
      width: 200px;
      flex-grow: 1;
      background-color: green;
      overflow: hidden;
    }
    .right{
      background-color: blue;
    }
    <div id="main">
      <div class="left">左</div>
      <div class="center">中</div>
      <div class="right">右</div>
    </div>
```

### 圣杯布局

  圣杯布局和双飞翼布局基本上是一致的，都是两边固定宽度，中间自适应的三栏布局，其中，中间栏放到文档流前面，保证先行渲染。解决方案大体相同，都是三栏全部float:left浮动，区别在于解决中间栏div的内容不被遮挡上，圣杯布局是中间栏在添加相对定位，并配合left和right属性，效果上表现为三栏是单独分开的（如果可以看到空隙的话），而双飞翼布局是在中间栏的div中嵌套一个div，内容写在嵌套的div里，然后对嵌套的div设置margin-left和margin-right，效果上表现为左右两栏在中间栏的上面，中间栏还是100%宽度，只不过中间栏的内容通过margin的值显示在中间。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>圣杯布局</title>
    <style>
    #hd{
        height:50px;
        background: #666;
        text-align: center;
    }
    #bd{
        /*左右栏通过添加负的margin放到正确的位置了，此段代码是为了摆正中间栏的位置*/
        padding:0 200px 0 180px;
        height:100px;
    }
    #middle{
        float:left;
        width:100%;/*左栏上去到第一行*/
        height:100px;
        background:blue;
    }
    #left{
        float:left;
        width:180px;
        height:100px;
        margin-left:-100%;
        background:#0c9;
        /*中间栏的位置摆正之后，左栏的位置也相应右移，通过相对定位的left恢复到正确位置*/
        position:relative;
        left:-180px;
    }
    #right{
        float:left;
        width:200px;
        height:100px;
        margin-left:-200px;
        background:#0c9;
        /*中间栏的位置摆正之后，右栏的位置也相应左移，通过相对定位的right恢复到正确位置*/
        position:relative;
        right:-200px;
    }
    #footer{
        height:50px;
        background: #666;
        text-align: center;
    }
</style>
  </head>
  <body>
    <div id="hd">header</div>
    <div id="bd">
        <div id="middle">middle</div>
        <div id="left">left</div>
        <div id="right">right</div>
    </div>
    <div id="footer">footer</div>
  </body>
</html>
```
### 双飞翼布局

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>双飞翼三栏布局</title>
    <style>
#hd{
    height:50px;
    background: #666;
    text-align: center;
}
#middle{
    float:left;
    width:100%;/*左栏上去到第一行*/
    height:100px;
    background:blue;
}
#left{
    float:left;
    width:180px;
    height:100px;
    margin-left:-100%;
    background:#0c9;
}
#right{
    float:left;
    width:200px;
    height:100px;
    margin-left:-200px;
    background:#0c9;
}

/*给内部div添加margin，把内容放到中间栏，其实整个背景还是100%*/
#inside{
    margin:0 200px 0 180px;
    height:100px;
}
#footer{
   clear:both; /*记得清楚浮动*/
   height:50px;
   background: #666;
   text-align: center;
}
</style>
  </head>
  <body>
      <div id="hd">header</div>
  <div id="middle">
  <div id="inside">middle</div>
  </div>
  <div id="left">left</div>
  <div id="right">right</div>
  <div id="footer">footer</div>
  </body>
</html>
```
## 实现动态div

2个div，一个高度随着另一个div的高度变化而变化

***
思路:在外套一层div，设置display:table;给里层2个元素设置dispaly:table-cell,并为其中一个设置宽度
***
