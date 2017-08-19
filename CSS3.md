# CSS3(颜色和背景设置)

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
