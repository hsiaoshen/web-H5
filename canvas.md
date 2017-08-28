# canvas 画布

## 什么canvas？

是一个新型的双标签，可被用来通过脚本(一般是js)绘制图形，但是本身不具有绘画功能，还可以实现动画效果

## 怎么测试浏览器对canvas的支持不支持？

```html
<canvas>该浏览器不支持</canvas>
```
如果显示出字体来就是不支持

## 特点

1. 默认300px*150px
2. 可以通过style来设置其他属性
3. 重新设置canvas标签的宽高会让画布擦除所有内容
4. 坐标(0,0)为左上角

## 语法

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>画布的基本使用</title>
  </head>
  <body>
    <canvas id="canvas" width="500px" height="300px">该浏览器不支持</canvas>
    <img src="qq.ico" alt="" id="pic">
  </body>
  <script type="text/javascript">
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    var img = document.getElementById('pic');

    //一. 画线操作
    ctx.beginPath()  //设置绘制的开始，每次执行此方法，表示重新绘制路径
    ctx.moveTo(50,50) //设置绘制路径的起点

    ctx.lineTo(100,200) //画直线，从起点到x,y的坐标位置连线

    //样式必须在绘制前，否则采用前面的样式，而后面的绘制才会用到设置好的样式

    ctx.strokeStyle = 'red'; //设置描边的颜色样式

    ctx.lineWidth = 3; //设置线条的宽度

    // 二, 画矩形

    ctx.fillStyle = 'blue';

    ctx.fillRect(150,100,50,50)  //绘制填充矩形

    ctx.strokeRect(250,100,50,50) //绘制描边矩形

    ctx.stroke()    //只有该操作，才会显示出来

    ctx.clearRect(0,0,500,300) //擦除指定矩形大小的所有内容，可以用此方法来刷新画布


    ctx.closePath()

    // 三 绘制圆弧
    ctx.beginPath()

    ctx.arc(100,100,50,90*Math.PI/180, 180*Math.PI/180,false);

    ctx.strokeStyle = 'green';

    ctx.stroke()

    //四 绘制文本，首先是文本内容，然后是文本开始坐标x,y

    ctx.font = '24px';

    ctx.textBaseline="middle"; //设置文本基线

    //alphabetic ： 默认。文本基线是普通的字母基线。
    // top ： 文本基线是 字符的顶端。。
    // hanging ： 文本基线是悬挂基线。
    // middle ： 文本基线是字符的正中。
    // ideographic： 文本基线是字符基线。
    // bottom ： 文本基线是字符的底端。

    ctx.textAlign = 'start'; //文本对齐方式有以下属性:start,end,center,left,right

    ctx.fillText("我喜欢钱", 100,100); //绘制填充文本

    // ctx.strokeText("kkkk", 200,200); //绘制描边文本

    ctx.clearRect(0,0,500,300)

    ctx.beginPath()

    // 五  绘制图片:必须灯图片加载完毕后

    img.onload = function(){
      ctx.drawImage(img,0,0,100,100 * 296 / 331);  // 设置图片的起始位置和宽高，最好和原有图标比例相同

      //裁剪指定区域，并且按照指定尺寸渲染到画布上
      // context.drawImage(img,sx,sy,swidth,sheight,x,y,width,height);
      ctx.drawImage(img,80,200,100,110,0,0,200,220);
    }
    ctx.closePath();
    // 六  阴影
    ctx.beginPath();

    //如果不设置，后面的会继承前面的阴影属性

    ctx.fillStyle = "red";
    ctx.shadowColor = "yellow";     //设置阴影的颜色
    ctx.shadowOffsetX = 20;          //设置水平和垂直的阴影偏移
    ctx.shadowOffsetY = 20;
    ctx.shadowBlur = 2;               //设置模糊度，大于1的正整数，数值越大模糊度越大
    ctx.fillRect(100,100,150,150);

    ctx.clearRect(0,0,500,300)
  </script>
</html>

```
### 线性渐变

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>线性渐变</title>
  </head>
  <body>


    <canvas id="canvas" width="600" height="600"></canvas>

    <script type="text/javascript">
    var can = document.querySelector('#canvas');
    can.style.border = "1px solid red";
    var ctx = can.getContext("2d");

    //渐变坐标必须和绘制的图形在同一个区域内，否则就不是渐变了
    // ctx.createLinearGradient(起点横坐标,起纵,结束横,结束纵);
    var grd = ctx.createLinearGradient(0,0,200,0);

    //设置颜色，一下只能设置一种
    grd.addColorStop(0, "red");
    grd.addColorStop(0.3, "green");
    grd.addColorStop(0.5, "pink");
    grd.addColorStop(1, "yellow");

    // 关键点：把渐变设置到填充的样式
    ctx.fillStyle = grd;

    //展现了超出区域就不是渐变了
    ctx.fillRect(0,0,200,200);
    ctx.fillRect(0,240,300,300);
    ctx.fillRect(400,400,50,50);

    </script>
  </body>
</html>

```
### 径向渐变

```html
var circle = ctx.createRadialGradient(300,300,50,300,300,200);
circle.addColorStop(0, 'red');
circle.addColorStop(0.5, 'blue');
circle.addColorStop(1, 'yellow');
ctx.fillStyle = circle ;
ctx.arc(300,300,200, 0, 2 * Math.PI);
ctx.fill();
```
### 背景

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>绘制背景</title>
  </head>
  <body>
    <canvas id="canvas" width="600" height="600"></canvas>
  </body>
  <script type="text/javascript">
  var can = document.querySelector('#canvas');
  can.style.border = "1px solid red";
  var ctx = can.getContext("2d");

  var img = new Image();
  img.src = 'qq.ico';
  img.alt = '图片'

  img.onload = function(){
    var pattern = ctx.createPattern(img,'repeat');    //创建pattern对象
    ctx.fillStyle = pattern;  //设置填充样式为创建好的背景
    ctx.fillRect(0,0,331,292);
  }
  </script>
</html>

```
### 画布的缩放

注意：画布的缩放是建立在当前画布的大小之上的，后续的画布操作会被放大或缩小但是前面已经画好的不会改变

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>画布操作</title>
    <style media="screen">
      * {
        margin: 0;
        padding: 0;
      }
    </style>
  </head>
  <body>
    <canvas id="canvas" width="600" height="601"></canvas>

    <script type="text/javascript">

    var can = document.querySelector('#canvas');
    can.style.border = "1px solid red";
    var ctx = can.getContext("2d");

    ctx.strokeStyle = "red";
    ctx.lineWidth = 4;
    ctx.strokeRect(0,0,100,100);

    /*
    只要对画布进行了缩放，那么后续的绘制都会受到影响
    */
    ctx.scale(2,2);//对画布进行了2倍的放大
    ctx.strokeStyle = "green";
    ctx.strokeRect(0,0,100,100);
    ctx.strokeRect(100,100, 20,20);

    ctx.scale(0.5,0.5);//恢复原本尺寸
    ctx.strokeStyle = "red";
    ctx.strokeRect(100,100, 20,20);

    </script>
  </body>
</html>
```

### 画布的原点移动

语法: ctx.translate(x, y),设置整个画布的远点，会影响后边的绘制。


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>画布操作</title>
    <style media="screen">
      * {
        margin: 0;
        padding: 0;
      }
    </style>
  </head>
  <body>
    <canvas id="canvas" width="600" height="601"></canvas>

    <script type="text/javascript">

    var can = document.querySelector('#canvas');
    can.style.border = "1px solid red";
    var ctx = can.getContext("2d");


    ctx.translate(100,100);
    ctx.strokeStyle = "red";
    ctx.lineWidth = 4;
    ctx.strokeRect(0,0,100,100);

    //恢复原点
    ctx.translate(-100,-100);
    ctx.strokeStyle = "green";
    ctx.strokeRect(0,0,100,100);

    </script>
  </body>
</html>
```
