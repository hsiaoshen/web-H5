# 边框 内边距 外边距 盒子(要遵循上右下左的顺序)

## 边框 border

### 综合设置

```css
border: width style color
```
style:(必须有,若没这个其他样式无效,值为none时其他样式无效)

1. hidden：隐藏边框。IE7及以下尚不支持
2. dotted：点状轮廓。IE6下显示为dashed效果
3. dashed：虚线轮廓。
4. solid：实线轮廓
5. double：双线轮廓。两条单线与其间隔的和等于指定的border-width值
6. groove：3D凹槽轮廓。
7. ridge：3D凸槽轮廓。
8. inset：3D凹边轮廓。

```css
border: 0 none;  //设置边框为0的方法。
```

### border-radius  边框圆角化(按照顺时针)

```css
border-radius: 水平半径/垂直半径

<!-- 有2个参数时,中间用'/'分隔 -->
```
有以下几种情况:

1. 1个值:4个角
2. 2个值:上左(下右) 上右(下左)
3. 3个值: 上左  上右(下左) 下右
4. 4个值: 上左  上右  下右 下左


## 外边距 margin

小技巧:盒子水平居中
```css
margin:0 auto 
```
取消浏览器的默认属性
```css
* { margin:0; padding: 0}
```

### 外边距合并和解决

外边距垂直方向会发生合并:取最大值为外边距值

第一个h2的margin-bottom（10px），div的margin-top（20px），第二个h2的margin-top（10px）将被合并，它们之间的margin间隙最后是（20px），即取三者之间最大的那个值
```html
h2{margin:10px 0;}
div{margin:20px 0;}
......
<h2>这是一个标题</h2>
<div>
	<h2>这是又一个标题</h2>
</div>
```

第一个h2的margin-bottom（10px），div的margin-top（20px）将被合并，但第二个h2的margin-top不与它们合并，因为它被border分隔，不与它们相邻。

```html
h2{margin:10px 0;}
div{margin:20px 0;border:1px solid #aaa;}
......
<h2>这是一个标题</h2>
<div>
	<h2>这是又一个标题</h2>
</div>
```

总结:
1. margin折叠只发生在块级元素上；
2. 浮动元素的margin不与任何margin发生折叠；
3. 设置了属性overflow且值不为visible的块级元素，将不与它的子元素发生margin折叠；
4. 绝对定位元素的margin不与任何margin发生折叠；
5. 根元素的margin不与其它任何margin发生折叠；

解决嵌套元素合并方案:给父元素加边框或者内边距

## 盒子

把一个元素变成输入框:

```
<p contenteditable></p>
```

### 浮动

浮动:设定了浮动的元素会脱离标准文档流的控制,出现在父元素指定的位置.

```css
float:right(left,none)
```
规律:

1. 一个浮动的元素具有行内块元素的属性
2. 一个盒子的所有子元素都浮动就会排列在一行,若没设置父元素的高度,那么高度为0
3. 如果一个元素的上一个元素是浮动的,若该元素不浮动就上浮;若上个元素不浮动,就和上个元素的底部相平

#### 清除浮动

方法:
1. 设置高度
2. 在浮动的父盒子中添加空元素,并为空元素添加clear:both属性
3. 给浮动的父盒子添加overflow:hidden(scroll或auto)
4. 使用伪元素
```css
            .clearfix::after, 
            .clearfix::before{
                content: '';    //必须有
                height: 0px;
                line-height: 0px; 
                display: block;
                visibility: hidden;
                clear: both;
                }
	      .clearfix{
		zoom:1 //兼容ie	
		}
```
### 定位 position

1. static:静止的,没有脱离标准流
2. relative:相对定位,没有脱离标准流
3. absolute:绝对定位,脱离标准流(祖先元素无定位,相对于body;祖先元素有定位,相对于最近定位了的元素)
4. fixed:固定,脱离了标准流(一般用于广告)

#### z-index
设置层级,只有在position:relative,absolute,fixed时生效

