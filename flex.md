# 伸缩盒子(flex) --> 具有浮动的作用,脱离了标准流

## PC端

### 常用属性

#### flex-grow

按照比例分配剩余空间,比例不允许是负值

自己的理解:
1. 如果没设置flex-grow,那么flex-grow:0
2. 
```html
<ul class="flex">
    <li>a</li>
    <li>b</li>
    <li>c</li>
</ul>

.flex{display:flex;width:600px;margin:0;padding:0;list-style:none;}
.flex li:nth-child(1){width:200px;}
.flex li:nth-child(2){flex-grow:1;width:50px;}
.flex li:nth-child(3){flex-grow:3;width:50px;}
```

## react

