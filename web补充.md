
类库：zepto.js  jQuery.js iScroll.js

CSS预处理器： sass

数据模拟： mock

前端框架：Bootstrap(搜索部分原理面试题)  Ant-design(阿里基于react组件库)

MVC  html(M)  css(V)  js(C)

MVVM框架：react 系列(redux react-router react-redux)
react.js小书

ES6( 箭头函数，class，模板字符串， import export)

{firstName, lastName, year} ==== >
{firstName:firstName,lastName:lastName,year:year}


xxx.js
var a = 1, b = 2,c = 3;
export {a,b,c};
export default function(){....}

import Fun,{a,b,c} from "xxx.js"



生命周期
state,props 区别
组件的封装(function(){}, class, React.createClass())
smart组件 dumb组件


组件之间的通信（父子组件，兄弟组件之间(evetproxy)，祖先后代(redux)）

状态管理（redux)
redux: createStore  combineReduers

react-redux:是将react连接到redux
Provider, connect(高阶组件)


单页面路由（react-router)
路由实现：hash, history.pushState



后端框架：Express
express:中间件，cookie session , mongodb, redis


自动化工具： gulp webpack


http://blog.parryqiu.com/2017/04/05/webpack2-tech-lesson/?utm_source=tuicool&utm_medium=referral



常见性能优化


移动web开发(问题？如何解决？)
http://www.cnblogs.com/liulinjie/p/5663015.html


1px边框问题
http://www.jianshu.com/p/7e63f5a32636


rem单位（移动端开发）？？


link标签？
dns-prefetch, prefetch 优化手段
设置 标签 icon


fetch ?
whatwg-fetch
isomorphic-fetch 

FormData()表单序列化的构造函数


websocket?(前端websocket)
http://www.ruanyifeng.com/blog/2017/05/websocket.html?utm_source=tuicool&utm_medium=referral



http://www.css88.com/archives/7628   （模块机制）
commonjs： 
node  require module.exports 
特点：同步加载，就近依赖


http://www.jb51.net/article/73626.htm
amd: 
特点：异步加载，全局依赖
Require.js库就是amd的模块机制


umd:通用的模块规范（可以根据应用场景，编写一个通用的模块）

browserify :命令行工具，直接将模块转换为浏览器端可用的
