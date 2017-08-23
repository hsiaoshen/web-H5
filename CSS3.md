# CSS3(颜色和背景设置)

## 透明度设置

opacity:0~1

注意:设置了透明度后子元素会继承,而rgba不会被继承

### 层叠定律
而对于没有激活 z-index 的普通层来说，如果那个层使用了属性值小于1的 opacity 属性，哪个层就会显示在上面。

解决: position 属性值为 absolute、relative 的层，将会比普通层更高层次。使用了小于1的 opacity 属性的层，也比普通层更高层次并且和指定 position 的层同层，但是不支持 z-index 属性，所以指定 position 的层，可以使用 z-index 属性，来覆盖带有小于1的 opacity 属性的层


## 颜色设置

可以方法有:单词,reg(0,0,0),reg(0,0,0,1),#fff


## 背景设置

### background-image,background-repeat,background-position

```css
background-image: url("image/xxx.jpg")
back-repeat: no-repeat/repeat/repeat-x/repeat-y
background-position:top left/10px 20px
```
### background-attachment

1. fixed:背景图像相对于窗体固定。
2. scroll：背景图像相对于元素固定，也就是说当元素内容滚动时背景图像不会跟着滚动，因为背景图像总是要跟着元素本身。但会随元素的祖先元素或窗体一起滚动。
3. local：背景图像相对于元素内容固定，也就是说当元素随元素滚动时背景图像也会跟着滚动，因为背景图像总是要跟着内容。（CSS3）

### background-origin(Css3)

1. padding-box：从padding区域（含padding）开始显示背景图像。
2. border-box：从border区域（含border）开始显示背景图像。
3. content-box：从content区域开始显示背景图像。

### background-clip(CSS3)

![展示图](http://i4.bvimg.com/607379/fde07f0cf105ad50.png)
1. padding-box：从padding区域（不含padding）开始向外裁剪背景。
2. border-box：从border区域（不含border）开始向外裁剪背景。
3. content-box：从content区域开始向外裁剪背景。
4. text:text：
从前景内容的形状（比如文字）作为裁剪区域向外裁剪，如此即可实现使用背景作为填充色之类的遮罩效果

#### 遮照效果

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>遮照效果</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <!-- <link href="css/style.css" rel="stylesheet"> -->
        <style>
            #demo{
                width: 800px;
                 height: 300px; 
                margin: 50px auto;
                text-align: center;
                font:bolder 200px "黑体";
                -webkit-background-clip:text;
                -webkit-text-fill-color: transparent;    
                background-image: url('http://demo.doyoe.com/css3/background-clip/skin/girl.jpg');
                  /* background-position: center top;   */
                /* text-transform:uppercase; */
                -webkit-animation: move 20s ease infinite; 
            }
            @-webkit-keyframes move{
                0%{background-position:left top;}
	            50%{background-position:right top;}
	            100%{background-position:left top;}
            }
        </style>
    </head>
    <body>
        <p id="demo">遮照效果</p>
    </body>
</html>
```
