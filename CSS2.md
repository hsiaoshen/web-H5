# 常用CSS

## 字体设置

### font-size(如果有继承那就是计算后的值)
1. rem:以html元素的字体为基准,解决了em和px的问题,只需要给html设置字体大小,对于IE8不兼容问题,可使用px
1. em:相对于父元素的,父元素的字体大小 = 1em
1. px:设置精准但是不灵活
1. 百分比:相对于父元素

注意:以上也是度量单位

### font-family

可以同时指定多个字体，中间以逗号隔开，表示如果浏览器不支持第一个字体，则会尝试下一个，直到找到合适的字体。英文字体名必须位于中文字体名之前.使用unicode对中文字体进行编码

### font-weight
font-weight属性用于定义字体的粗细，其可用属性值：normal、bold、bolder、lighter、100~900（100的整数倍）。

### font-style
font-style属性用于定义字体风格，如设置斜体、倾斜或正常字体.normal(默认值),italic(斜体),oblique(倾斜)

### 综合设置

font: font-style font-weight font-size/line-height font-family

注意: 后面2个必须有,而且写综合设置时会改变行高,所以文本的垂直居中一定要写在字体综合设置之后

### 文本装饰 text-decoration

1. none：没有装饰（正常文本默认值）
1. underline：下划线。
1. overline：上划线。
1. line-through：删除线


## 颜色设置

可以方法有:单词,reg(0,0,0),reg(0,0,0,1),#fff

## 背景设置

### back-image

background-image: url("image/xxx.jpg);


## 其他属性(一个汉字算一个字符)

### letter-spacing

字符与字符间的距离(中英文都有效)

### word-spacing

单词之间的距离

### line-height

行高,又称行间距

line-height = height  --> 文本的垂直居中

### 文本水平居中和垂直居中

#### 水平居中

text-align:center

#### 垂直居中

vertical-align(只适合行内元素)

***
1. baseline： 将支持valign特性的对象的内容与基线对齐
2. sub： 垂直对齐文本的下标
3. super： 垂直对齐文本的上标
4. top： 将支持valign特性的对象的内容与对象顶端对齐
5.text-top： 将支持valign特性的对象的文本与对象顶端对齐
6. middle： 将支持valign特性的对象的内容与对象中部对齐
7. bottom： 将支持valign特性的对象的文本与对象底端对齐
8. text-bottom： 将支持valign特性的对象的文本与对象顶端对齐

***

line-height:height(父元素的高度)

### text-indent

首行缩进,单位一般用em(如果是中文则1个em就是一个汉字长度)

### white-space(空白符处理)

1. normal：常规（默认值），文本中的空格、空行无效，满行（到达区域边界）后自动换行。
2. pre：预格式化，按文档的书写格式保留空格、空行原样显示。
3. nowrap：空格空行无效，强制文本不能换行，除非遇到换行标记。内容超出元素的边界也不换行，若超出浏览器页面则会自动增加滚动条。

###  自动换行 word-break

1. normal 使用浏览器默认的换行规则。
2. break-all 允许在单词内换行。
3. keep-all 只能在半角空格或连字符处换行。

### overflow

属性值:

1. hidden:超出部分隐藏
2. visible:超出部分继续显示在元素外
3. scroll: 超出的内容会出现滚动条
4. auto: 不超出不隐藏,超出会出现滚动条


