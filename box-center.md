# 盒子的局中问题(子绝父相)

## 只考虑水平居中,,没有相对定位

```css
margin:0 auto;
```

## 平移和position的结合(适合盒子的宽高存在,但是我门不知道;translate的平移是相对于自身宽高的)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>css3让一个盒子居中</title>
    <style type="text/css">
        .parent_box{
            width: 400px;
            height: 200px;
            background: red;
            position: relative;
        }
        .child_box{
            width: 200px;
            height: 100px;
            background: #9ff;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate( -50%,-50%);
        }
    </style>
</head>
<body>
    <div class="parent_box">
        <div class="child_box">

        </div>
    </div>
</body>
</html>
```

## flex布局

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>垂直居中</title>
    <style type="text/css">
        .box{
            width: 400px;
            height: 200px;
            background: #f99;
        }
        .box1{
            width: 200px;
            height: 100px;
            background: green;
        }
        .center{
            display: flex;
            justify-content: center;
            align-items: center;
        }
    </style>
</head>
<body>
    <div class="box center">
        <div class="box1">

        </div>
    </div>
</body>
</html>
```
## 自盒子的宽高未知但有(以下这种情况子元素必须是相对定位)

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>居中</title>
    <style type="text/css">
        #box{
            width: 800px;
            height: 400px;
            position: relative;
            background: red;
        }
        #box1{
            width: 100px;
            height: 50px;
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            margin: auto;
            background: green;
        }
    </style>
</head>
<body>
    <div id="box">
        <div id="box1">

        </div>
    </div>
    <script type="text/javascript">

    </script>
</body>
</html>
```
注意事项:

1. 必须有高度
2. 建议设置overflow:auto来防止内容越界溢出


## 宽高已知

思路:
***
给父元素相对定位 
给子元素绝对定位 
left: 50%;top: 50%; 
margin-left: 负的宽度一半;
margin-top: 负的高度一半；
***

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>居中</title>
    <style type="text/css">
        #box{
            width: 400px;
            height: 200px;
            position: relative;
            background: red;
        }
        #box1{
            width: 200px;
            height: 100px;
            position: absolute;
            top: 50%;
            left: 50%;
            margin-left: -100px;
            margin-top: -50px;
            background: green;
        }
    </style>
</head>
<body>
    <div id="box">
        <div id="box1">

        </div>
    </div>
</body>
</html>
```
