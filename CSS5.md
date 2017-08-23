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
