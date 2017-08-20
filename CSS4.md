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


