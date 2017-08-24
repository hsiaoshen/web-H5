# 布局


## 两栏自适应布局

### 使用伸缩盒子



### 使用浮动

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
