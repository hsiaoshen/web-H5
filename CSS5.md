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

## 渐变

用来代替图片的

相比图片的好处：

1. 加快页面加载时间，减少带宽占用
2. 渐变是由浏览器生成的，缩放效果比图片好，使用更灵活

### 线性渐变

```css
 background:linear-gradient(to bottom, red 20%,white 40%,blue);
 //必须要有方向和起始色和终止色
```

### 径向渐变

```css
   /* background-image: radial-gradient(100px at center,yellow 50%  , blue, red); */
    background-image: radial-gradient(100px at left top,yellow 50%  , blue, red);
    //要设置圆心和半径
```

## 过渡

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


