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