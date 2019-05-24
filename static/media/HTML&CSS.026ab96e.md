## 2 HTML & CSS

### 2.0 Links

- [Web前端开发视频](https://study.163.com/course/courseMain.htm?courseId=1004165002) ——入门视频

- [网易前端规范](http://nec.netease.com/) ——前端开发规范


- [MDN-学习Web开发](https://developer.mozilla.org/zh-CN/docs/learn#)

- [浏览器的工作原理](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/)

- [GitHub-一大波前端资源](https://github.com/dypsilon/frontend-dev-bookmarks)

- [前端代码规范及最佳实践](http://coderlmn.github.io/code-standards/)

### 2.1 标签
#### 2.1.1 基础标签

1. 编码字符集

- gb2312 国家标准第2312条，只有简体
- gbk 扩展版本，包含繁体字符集，亚裔字符集
- unicode 万国码
- utf-8 unicode transform from 8

2. 文本类型标签

- &lt;strong>&lt;/strong>：使得字体加粗
- &lt;em>&lt;/em>：使字体斜体
- &lt;del>&lt;/del>：使内容有划除形式，中划线
- &lt;address>&lt;/address>：地址标签，独占一行，斜体


```html
<del style="color: #999">$50</del>
```

#### 2.1.2 高级标签

1. html编码

- &nbsp ; 表示空格
- &lt ; less than 小于号
- &gt ; greater than 大于号

2. 单标签<br>

单独出现，自己具有修饰功能，&lt;br>标签属于单标签，内部无修饰，此外如：<br>

- &lt;meta><br>

- &lt;br><br>

- &lt;hr>水平线<br>

3. &lt;img>标签属性：

- style="width:200px"  图片格式大小；

- alt=""  图片占位符，用文字简单叙述，图片加载不出的情况下，展示文字信息；

- title=""  图片提示符，鼠标悬停到图片后显示提示；

4. &lt;a>&lt;/a>

（1）<a></a>标签可放图片、CSS等任意一种可用于跳转的内容，如：

```html
<a href="https://www.baidu.com" style="width:100px; height:100px; background-color:red; display:b"></a>
```

（2）target="_blank"将链接在新的标签页中打开

```html
<a href="https://www.baidu.com" target="_blank"></a>
```

（3）<a></a>表示的意思，anchor：锚，有以下的作用：

- 超链接


- 锚点（记录一个位置，通过锚点回到顶部等功能）


```html
<div id="demo1" style="width:100px; height:100px; background-color:green;">demo1</div>
<br>*100
<div id="demo2" style="width:100px; height:100px; background-color:red;">demo2</div>
<br>*100
```
- 固定位置

```html
<a style="display:block; position:fixed; bottom:100px; right:100px; border:1px solid black; height:50px; width:200px; background-color:#fcc;" href="#demo1">find demo1 </a>
<a style="display:block; position:fixed; bottom:100px; right:100px; border:1px solid black; height:50px; width:200px; background-color:#ffc;" href="#demo2">find demo2 </a>
```
- 打电话，发邮件等


```html
<a href="mailto: 823147833@qq.com">发邮件</a>
```

- 协议限定符


```html
<a href="javascript:"></a>    //协议限定符，点击后可以强制运行
```

5. &lt;form>&lt;/form>表单标签：能将前端数据发送给后端

- 发送数据的方式

```html
<form method="get/post"> .  //method表示前端和后端之间发数据的方式，get
</form>
```

- action=""发送给谁的地址（后端模拟地址）

```html
<form method="get" action="http://www.baidu.com/123.php"><form>
```

### 2.2 CSS

CSS: cascading（层叠的）style sheet

#### 2.2.1 CSS引入方法

1. 引入CSS方法：


- 行间样式（在body中）

```html
<div style=" width:100px; height:100px; background-color: red;">
</div>
```

- 页面级CSS（在head中）

```html
<style type="text/css">      //告诉浏览器内部为css代码
    div{
        width:100px;
        height:100px;
        background-color: green;
    }
</style>
```

- 外部CSS文件


（1）CSS文件内容

```css
div {width:100px;
    height:100px;}
```

（2）html文件内容，在<head></head>中添加如下：

```html
<link rel="stylesheet" type="text/css" href="lesson.css"> 异步加载
```

2. HTML文件如何引入到浏览器页面上


- 网页的包放在服务器上。

- 服务器有地址，便于客户端进行访问。如服务器地址可以为192.168.000.001。注意，www.baidu.com不是地址，是域名，域名通过dns解析为地址。

```
www.baidu.com -- dns -- 192.168.000.001
```

- 客户端从服务器上索取网页这个包，其中包括html、css、js文件，下载并在浏览器上执行。

- 注：浏览器的下载策略是一边下载一遍执行

- 浏览器会开启不同线程，一边下载HTML，一遍下载CSS（异步加载，也就是同时执行）

3. 计算机中的同步与异步与生活中的概念正好相反，异步的asynchronous；同步的synchronous

#### 2.2.2 CSS选择器

1. CSS选择器，CSS如何选择HTML元素

（1）通过id的方式，在HTML中添加id

```html
<div id="only">123</div>      //id和元素之间一一对应，一个元素只有一个id，一个id只对应一个元素
<div id="only1">345</div>
```

在CSS文件中，用#号加id

```html
#only {
    background-color: red;
}
```

（2）class选择器，通过class选择，在HTML语言中添加class

```html
<div class="demo demo1">123</div>      //class可以多对多，此处demo和demo1都同时作用到这个块
<div class="demo">234</div>
```

在css文件中，用.demo来选择修饰内容

```css
.demo{
    background-color:red;
}
.demo1{
    color:#f40;
}
```

（3）id的对应方式是一对一的，class选择器对应关系是多对多，如在HTML文件中，添加class：

```html
<div class="demo demo1">123</div>
```

在css文件中，可以用两个部分来同时修饰：

```css
.demo{
    background-color:red;
}
.demo1{
    color:#f40;
}
```

（4）标签选择器，表示所有的标签都进行装饰。

如在HTML中写：

```html
<div>123</div>
```

在CSS中写：

```css
div {
    background-color: black;
}
```

则HTML文件中所有的<div></div>块效果相同。


*无论标签在哪，都会被渲染


（5）通配符选择器：形式及其单一，表示所有的标签都有这个效果，全局范围内的。

```css
*{
    background-color: green
}
```

（6）选择器优先级：!important > 行间样式 > id > class=属性选择器 > 标签选择器 > 通配符

（7）属性选择器：在HTML文件中如下样例

```html
<div id="only" class="demo">123</div>
<div id="only">456</div>
```

那么在css文件中写

```css
[id="only"] {
    background-color: red;
}
[class]{
    background-color: green;
}
.demo{
    background-color: black;
}
```

属性选择器与class选择器属于并级的

（8） !important优先级最高，如在属性后面加上!important则权重最高，如

```css
div{
    background-color: green!important;
}
```
（9）CSS权重
<center>

| 选择器 | 权重 |
| :----: | :----: |
| !important | Infinity |
| 行间样式 | 1000 |
| id | 100 |
| class/属性/伪类 | 10 |
| 标签/伪元素 | 1 |
| 通配符 | 0 |

</center>

注：1000与100之间是256进制，不是10进制

5. 主流浏览器及独立内核

- 浏览器组成：shell+内核（操作代码识别和运行）
- IE + trident
- Firefox + Gecko
- Google Chrome + Webkit/blink
- Safari + Webkit
- Opera + presto


### 2.3 盒子模型

### 2.4 浮动模型

### 2.5 补充知识点