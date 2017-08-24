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

## 三栏布局（左右固定，中自适应）
