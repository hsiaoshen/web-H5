# 伸缩盒子(flex) --> 具有浮动的作用,脱离了标准流

## 常用属性

### flex(设置或检索弹性盒模型对象的子元素如何分配空间)

综合写法: flex:flex-grow flex-shrink flex-basis

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
#### flex-shrink,

按照比例缩小空间,默认比例1

计算:每个子盒子的固定长度 -  (每个自盒子的固定长度和 - 伸缩盒子的长度) / flex-shrink的值和 * 每个子盒子flex-shrink的值

#### flex-basis

如果所有子元素的基准值之和大于剩余空间，则会根据每项设置的基准值，按比率伸缩剩余空间

### flex-flow(设置或检索弹性盒模型对象的子元素排列方式)

综合写法--> flex-flow: flex-direction flex-

#### flex-direction(定义弹性盒子元素的排列方向)

1. row：主轴与行内轴方向作为默认的书写模式。即横向从左到右排列（左对齐）。
2. row-reverse：对齐方式与row相反。
3. column：主轴与块轴方向作为默认的书写模式。即纵向从上往下排列（顶对齐）。
4. column-reverse：对齐方式与column相反。

#### flex-wrap(控制flex容器是单行或者多行，同时横轴的方向决定了新行堆叠的方向)

1. nowrap：flex容器为单行。该情况下flex子项可能会溢出容器
2. wrap：flex容器为多行。该情况下flex子项溢出的部分会被放置到新行，子项内部会发生断行
3. wrap-reverse：反转 wrap 排列。





## react

