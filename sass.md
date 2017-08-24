# sass

是一种CSS预处理器，可以在其中使用函数，变量，逻辑判断等，然后翻译成正常的CSS文件，可以使CSS更简洁，适应性强，易于维护和修改

## 安装和使用

1. 如果你使用的是Windows,你可能首先需要安装Ruby
2. gem install sass
3. sass input.scss output.css 编译生成css文件
4. sass --watch input.scss:output.css 监视文件改动并自动编译更新css
5. sass --watch 源文件目录 : 生成文件目录(路径不能为中文)

## 语法

### 文件名后缀

sass有两种后缀名文件：一种后缀名为sass，不使用大括号和分号；另一种就是我们这里使用的scss文件，这种和我们平时写的css文件格式差不多，使用大括号和分号

### 
