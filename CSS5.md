# CSS3的新特性

## 理念

渐进增强(向上兼容):开始就针对低版本浏览器进行构建页面，完成基本的功能，然后再针对高级浏览器进行效果、交互、追加功能达到更好的体验。(应关注于内容本身)

优雅降级(向下兼容):一开始就构建站点的完整功能，然后针对浏览器测试和修复。比如一开始使用 CSS3 的特性构建了一个应用，然后逐步针对各大浏览器进行 
hack 使其可以在低版本浏览器上正常浏览。(针对那些最高级、最完善的浏览器来设计网站)

```html
.transition {   /*渐进增强写法*/
  -webkit-transition: all .5s;
     -moz-transition: all .5s;
       -o-transition: all .5s;
          transition: all .5s;  
} 
.transition {   /*优雅降级写法*/ 
          transition: all .5s;
       -o-transition: all .5s;
     -moz-transition: all .5s;
  -webkit-transition: all .5s;
}
```

## 选择器

关系选择器
1.包含选择符(E F)
2.子选择符(E>F)
3.相邻选择符(E+F)
4.兄弟选择符(E~F)

属性选择器
1.E[att]
2.E[att=“val”]
3.E[att~=“val”]
4.E[att^=“val”]
5.E[att$=“val”]
6.E[att*=“val”]
7.E[att|=“val”]

伪类选择器
常用：
E:link
E:visited
E:hover
E:active
E:focus
E:first-child
E:last-child
E:nth-child

伪元素
1.E:first-letter/E::first-letter
2.E:first-line/E::first-line
3.E:before/E::before
4.E:after/E::after

## 渐变(gradient)

用来代替图片的

相比图片的好处：

1. 加快页面加载时间，减少带宽占用
2. 渐变是由浏览器生成的，缩放效果比图片好，使用更灵活

### 线性渐变(linear-gradient)

```css
 background:linear-gradient(to bottom, red 20%,white 40%,blue);
 //必须要有方向和起始色和终止色
```

### 径向渐变(radial-gradient)

```css
   /* background-image: radial-gradient(100px at center,yellow 50%  , blue, red); */
    background-image: radial-gradient(100px at left top,yellow 50%  , blue, red);
    //要设置圆心和半径
```

## 过渡(transition)

特点：当前元素只要有“属性”发生变化时，可以平滑的进行过渡。

1. transition-property 设置过渡属性
2. transition-duration 设置过渡时间
3. transition-timing-function 设置过渡速度
4. transition-delay 设置过渡延时

***
transition-timeing-function:
* linear：线性过渡。等同于贝塞尔曲线(0.0, 0.0, 1.0, 1.0)
* ease：平滑过渡。等同于贝塞尔曲线(0.25, 0.1, 0.25, 1.0)
* ease-in：由慢到快。等同于贝塞尔曲线(0.42, 0, 1.0, 1.0)
* ease-out：由快到慢。等同于贝塞尔曲线(0, 0, 0.58, 1.0)
* ease-in-out：由慢到快再到慢。等同于贝塞尔曲线(0.42, 0, 0.58, 1.0)
* step-start：等同于 steps(1, start)
* step-end：等同于 steps(1, end)
***

```css
transition-property: border-color, background-color, color;
transition-duration: .5s;
transition-timing-function: ease-in;
transition-delay: .1s;

或者可以进行综合设置：
transition: border-color 0.5s ease-in 0.1s,
            background-color 0.5s ease-in 0.1,
            color 0.5s ease-in 0.1;
```

## 变换 transform(坐标轴方向:X轴朝右,Y轴朝下)

### 2D
1. translate(x,y)  --> 移动位置相当于自身原来的位置,若果设置百分比,那么是相对于自身宽高的百分比移动的
2. scale(x,y) --> 可以对元素进行水平和垂直方向的缩放,是以自身的元素为基准的
3. rotate(deg)  --> 可以对元素进行旋转，正值为顺时针，负值为逆时针
4. skew(deg, deg) --> 可以使元素按一定的角度进行倾斜


### 3D

1. 移动 translate3d(value,value,value) 可以改变元素的位置.
2. 缩放 scale3d(x, y, z), scaleX(x) .
3. 旋转 rotate3d(x,y,z,deg), rotateX(deg) 可以对元素进行旋转.
4. 倾斜 skew(deg, deg),skewX(deg) ,skewY(deg)可以使元素按一定的角度进行倾斜

### transform-origin

设置原点坐标

### transform-style

设置从视觉效果来看是3d还是平面

1. flat：指定子元素位于此元素所在平面内
2. preserve-3d：指定子元素定位在三维空间内

立体的
```html
<style>
body {
    -webkit-perspective: 1000px;
    perspective: 1000px;
}
.cube {
    position: relative;
    font-size: 80px;
    width: 2em;
    margin: 1.5em auto;
    -webkit-transform-style: preserve-3d;
    transform-style: preserve-3d;
    -webkit-transform: rotateX(-30deg) rotateY(30deg);
    transform: rotateX(-30deg) rotateY(30deg);
}
.cube > div {
    position: absolute;
    width: 2em;
    height: 2em;
    background: rgba(0, 0, 0, .1);
    border: 1px solid #999;
    color: white;
    text-align: center;
    line-height: 2em;
}
.front {
    -webkit-transform: translateZ(1em);
    transform: translateZ(1em);
}
.top {
    -webkit-transform: rotateX(90deg) translateZ(1em);
    transform: rotateX(90deg) translateZ(1em);
}
.right {
    -webkit-transform: rotateY(90deg) translateZ(1em);
    transform: rotateY(90deg) translateZ(1em);
}
.left {
    -webkit-transform: rotateY(-90deg) translateZ(1em);
    transform: rotateY(-90deg) translateZ(1em);
}
.bottom {
    -webkit-transform: rotateX(-90deg) translateZ(1em);
    transform: rotateX(-90deg) translateZ(1em);
}
.back {
    -webkit-transform: rotateY(-180deg) translateZ(1em);
    transform: rotateY(-180deg) translateZ(1em);
}
</style>
</head>
<body>
<div class="cube">
    <div class="front">1</div>
    <div class="back">2</div>
    <div class="right">3</div>
    <div class="left">4</div>
    <div class="top">5</div>
    <div class="bottom">6</div>
</div>
</body>
```

### perspective

指定观察者与「z=0」平面的距离，使具有三维位置变换的元素产生透视效果。「z>0」的三维元素比正常大，而「z<0」时则比正常小，大小程度由该属性的值决定。


### backface-visibility

1. visible：指定元素背面可见，允许显示正面的镜像。
2. hidden：指定元素背面不可见


## 动画 animation

创建动画并应用在元素上:

1. 通过@keyframes指定动画序列
2. 通过百分比将动画序列分割成多个节点
3. 在各节点中分别定义各属性
4. 通过animation将动画应用于相应元素

### 常用属性

* animation-name 设置动画序列名称
* animation-duration 动画持续时间
* animation-delay 动画延时时间
* animation-timing-function 动画执行速度，linear、ease,ease-in,ease-in-out等
* animation-play-state 动画播放状态，play、paused,running等
* animation-direction 动画逆播，alternate(先正常再反向),reverse,alternate-reverse
* animation-fill-mode 动画执行完毕后状态，forwards、backwards等
* animation-iteration-count 动画执行次数，inifinate(无限循环)等

## 媒体查询 media

媒体查询可以让我们根据设备显示器的特性（如视口宽度、屏幕比例、设备方向：横向或纵向）为其设定CSS样式，媒体查询由媒体类型和一个或多个检测媒体特性的条件表达式组成。用媒体查询，可以在不改变页面内容的情况下，为特定的一些输出设备定制显示效果。

```html
<head>
<meta name="viewport content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no"/>
  <!-- 
width=device-width:宽度等于当前设备的宽度
initial-scale=1：初始的缩放比例（默认为1）
maximum-scale=1：允许用户缩放到得最大比例（默认为1）
user-scalable=no：用户不能手动缩放
-->    
  <style>
     @media all(screen) with                                                 
 </style>                                                                                               
</head> 
```
