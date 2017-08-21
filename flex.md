# 伸缩盒子(flex) --> 具有浮动的作用,脱离了标准流

## PC端

### 常用属性

#### flex-grow

按照比例分配剩余空间,比例不允许是负值,默认值为0

计算:(伸缩盒子的总长度 - 每个子盒子的固定长度和) / flex-grow的总值 * 每个flex-grow的值   +  每个盒子的固定长度

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
#### flex-shrink

按照比例缩小空间,默认比例1

计算:每个子盒子的固定长度 -  (每个自盒子的固定长度和 - 伸缩盒子的长度) / flex-shrink的值和 * 每个子盒子flex-shrink的值

## react

