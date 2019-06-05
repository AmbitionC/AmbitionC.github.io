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
<form method="get/post">    //method表示前端和后端之间发数据的方式，get
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

在CSS文件中，用#号加id

```html
#only {
    background-color: red;
}
```

（2）class选择器，通过class选择，在HTML语言中添加class

- class可以做到多对多

在css文件中，用.demo来选择修饰内容

```css
.demo{
    background-color:red;
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

"*"表示无论标签在哪，都会被渲染

（5）通配符选择器：形式及其单一，表示所有的标签都有这个效果，全局范围内的。

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

（8） !important优先级最高，如在属性后面加上!important则权重最高

（9）CSS权重

<center>

|     选择器      | 权重     |
| :-------------: | -------- |
|   !important    | Infinity |
|    行间样式     | 1000     |
|       id        | 100      |
| class/属性/伪类 | 10       |
|   标签/伪元素   | 1        |
|     通配符      | 0        |

</center>

注：1000与100之间是256进制，不是10进制

5. 主流浏览器及独立内核

- 浏览器组成：shell+内核（操作代码识别和运行）
- IE + trident
- Firefox + Gecko
- Google Chrome + Webkit/blink
- Safari + Webkit
- Opera + presto

#### 2.2.3 CSS复杂选择器

1. 父子选择器 / 派生选择器

如果存在父子结构情况下，如果想要通过标签选择器渲染，则可以使用父子选择器，如在HTML中有如下：

```html
<div>
    <span>123</span>
</div>
<span>456</span>
```

如果需要对<div></div>内部的span内容进行修饰，则在css文件中应写成

```html
div span{
    background-color: red;
}
```

注：父子关系不在于非要标签选择器，而是在于父子关系成立即可，id选择器，class 选择器都行。如：

```html
<div class="wrapper">
    <strong class="box">
        <em>234</em> .   //需要渲染的
</div>
<em>123</em>


.wrapper .box em{
    background-color: red;
}
```

父子选择器下面的简介的子孙关系都可以。

2. 直接子元素选择器

**表示直接一级的子元素，那么孙关系的则不可以渲染。**

```html
<div>
    <em>1</em>
    <strong>
        <em>2</em>
    </strong>
</div>


div > em{
    background-color:green;     //只有1被渲染
}
```

3. 浏览器遍历父子选择器顺序为向右向左，这样时间复杂度最低

<center>

![浏览器遍历父子选择器顺序](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/2HTML%26CSS/2-1%E7%9A%84%E5%89%AF%E6%9C%AC.png)

</center>

4. 并列选择器

对共同的特性来限制一个，多个限制条件选择一个

```html
<div>1</div>
<div class="demo">2</div>       //如果要修饰第二行的话，其中又有div 又有class，所以要用到并列选择器
<p class="demo">3<p>


div.demo{
    background-color:red;
}
```

**并列选择器的使用要注意标签在class和id的前面，保证识别。**

5. 权重的使用案例

如下例，显示的颜色为红色， 因为只要选择同一排的选择器，则进行相加。如果相加相等，则后面的代码会覆盖前面的代码

```html
<div class="classDiv" id="idDiv">
    <p class="classP" id="idP">1</p>
</div>
```

```css
#idDiv p{
    background-color:red;           //100 + 1
}

.classDiv .classP{
    background-color: green;        // 10 + 10
}
```

在都有infinity的情况下，哪怕多一个也是多

```html
<div class="classDiv" id="idDiv">
    <p class="classP" id="idP">1</p>
</div>
```

```css
div #idDiv p .classP{
    background-color:red;!important           //1 + 10 + 1 + 100 + infinity
}

div.classP #idP {
    background-color: green;!important        //1 + 100 + 10 + infinity
}
```

6. 分组选择器

分开的组可以共用一个代码块
如在HTML文件中有如下代码：

```html
<em>1</em>
<strong>2</strong>
<span>3</span>
```

如果需要共用一个css代码块修饰，则可以用分组选择器，通常以数列的形式写出

```css
em,
strong,
span {
    background-color: red;
}
```

#### 2.2.4 CSS实践

1. font-size：内部字体的大小（设置字体的高），默认值16px
2. font-weight：字体加粗（lighter，normal，bold，bolder），取决于字体内部有没有，默认值为bolder
3. font-style：italic 字体斜体 = &lt;em>&lt;/em>
4. font-family：字体的字体，默认为arial
5. color：字体的颜色

- 标准式：纯英文单词 red；green；blue
- 颜色代码（每两位代表一个颜色，表示一个颜色的饱和度） #ff4400如果每两位相同则可以缩写
- 透明色：transparent
- 颜色函数  rgb(0~255, 0~255, 0~255)

6. border：加一个外边框（给容器），复合属性

```css
border: 1px solid black；      //粗细，实体，颜色
```

- border-width: 1px
- border-style: solid（实线）、dotted（点状虚线）、dashed（条状虚线）
- border-color
- border-left/right-color
- border-top/bottom-color

border可以用于画三角形，如

```css
border: 100px solid black;
border-left-color:black;
border-top-color:transparent;
border-right-color:transparent;
border-bottom-color:transparent;
```

7. text-align表示对其方式，默认值为左对齐
   - text-align: left; center; right     // 水平垂直
8. line-height：单行文本高度，文本的所占高度。
   比如文本的字体默认为16px，如果line-height设置为16px，则行间距为0，如果line-height设置为20px，且font-size仍然为16px的话，则就有行间距了。
9. 垂直方向居中，使文本高度=容器高度（line-height = height）
10. CSS只有块注释，如/*  */
11. **文字在容器中水平垂直都居中问题（单行文本水平垂直居中）**
    - 水平居中：text-align
    - 垂直居中，想要垂直居中，则让单行文本的高度line-height=容器高度height
    - 垂直居中或者可以加padding，但是该方法不常用
12. 首行缩进
    - 首行缩进不可以用&nbsp;的方式，空格在不同语言的输入法中，全角半角展示的形式都不一样。
    - text-indent首行缩进

```css
text-indent: 2em;       //缩进两个单位，为相对的单位
```

- m cm mm nm um都是绝对的单位
- px像素是相对的单位，像素是一英寸中有多少个点
- 1em = 1 font-size; = 16px（根据font-size来）

```css
line-height: 1.2em;        //表示16*1.2px
```

13. text-decoration文本装饰
    - <del></del>即表示文本上添加横线，如:

```html
<del>原价50元</del>;
<span>现价100元</span>
```

- 该标签一般不用，因为HTML文件都是负责结构，样式应该由CSS来实现。
- 要做到同样的效果，则可以用text-decoration: line-through;

```css
span{
    text-decoration: line-through;
}
del{
    text-decoration: none;     //告诉浏览器这一块没有线，则可以把线去掉
}
```

- 对于网页链接也可以通过CSS实现相同的效果，如：

```html
<a href="www.baidu.com">www.baidu.com</a>
<span>www.baidu.com</span>
```

通过text-decoration: underline;

```css
span{
    color:rgb(0, 0, 238);
    text-decoration: underline;     //overline上划线
    cursor:pointer;     //光标定位值，如果设置为pointer，则鼠标移动到位置时，变成小手。其他可以设置的值有：help(问号)，e-resize(向右)，copy(复制)，move(移动)。。。。等
}
```

14. hover伪类选择器
15. 表示鼠标移动至指定字符后，会触发的事件

```html
<a href="www.baidu.com">www.baidu.com</a>
```

```css
a:hover{
    background-color:orange;     //鼠标移动上去后背景颜色变成橘红色
}
```

样例：

```html
<a href="www.baidu.com">www.baidu.com</a>
<a href="www.taobao.com">www.taobao.com</a>
<a href="www.jd.com">www.jd.com</a>
```

```css
a{
    text-decoration: none;
}
a:hover{
    text-decoration: underline;
    background-color: #f40;
    color: #fff;
    font-size: 16px;
    font-weight: bold;
    font-family: arial;
    border-radius: 10px;
}
```

- 伪类的权重为10，如果放在行间样式的话（1000），则就不会引起改变。]

```html
<a style="text-decoration: none;" href="www.baidu.com">www.baidu.com</a>
```

#### 2.2.5 CSS引申

1. 标签的归类

- **行级元素/inline/内联元素      span, strong, em, a, del**

feature：内容决定元素所占位置，不会独占一行。不可以通过CSS改变宽高

```html
<span>123</span>         //符合行级元素特点 
<div>123</div>123        // 复合块级元素特点 
```

```css
span {
	width: 100px;
  height: 100px;
  background-color: red;
}
div {
  width: 100px;
  height: 100px;
  background-color: red;
} 
```

- **块级元素/block      div, p, ul, li, ol, form, address**

feature：独占一行，可以通过CSS改变宽高

- **行级块元素/inline-block   <img>标签**

feature：不独占一行，可以通过CSS改变宽高

```html
<img src="fy.jpg">123
```

```css
img {     
  width: 200px;
} 
```

在CSS中，有默认属性，display，但是可以更改

```css
span {     
  display: inline;//可以更改成block，拥有块级元素的属性
} 
div{     
  display: block;
} 
img{     
  display: inline-block;
} 
```

更改属性，可以让div拥有行级属性的特点

```css
div{     
  display: inline;     
  width: 100px;     
  height: 100px;     
  background-color: red; 
} 
```

**凡是带有inline的元素，都有文字特性，所以会被分割。比如常见的一个bug：将几张图并排的放在网页上，但是展示出来会有缝隙**

```html
<img src="xx.jpg">
<img src="xx.jpg">
<img src="xx.jpg">
<img src="xx.jpg">
```

解决方式：将代码改为

```html
<img src="xx.jpg"><img src="xx.jpg"><img src="xx.jpg"><img src="xx.jpg">
```

常规CSS库的一般设置：

```css
html, body, form, ul, h1, h2, h3, h4, p{
    padding:0; margin:0; border:0;
}
body{
    position: relative;
    color: #424242;
    background-color: transparent;
}
ul{
    list-style: none;
}
a{
    text-decoration: none;
    color: #002be5;
}
a img{
    border: 0;     //如果a标签下有img时，使其border为0
}
i{
    font-style: normal;
}
em{
    color: #e50000;
    font-style: normal;
}
select {
    -webkit-apperance: none;
    border: 0;
    padding: 0;
    margin: 0;
}
input {
    -webkit-apperance: none;
}
```



### 2.3 盒子模型

- 盒子模型原则：可以先写CSS 文件，反向编程的手段。**先定义功能，再选择样式**。
- 实现方式：可以先写一个功能，便于后面的引用（CSS工具库），便于后面的开发，复合模块化开发的过程。

盒子模型：针对于HTML每一个元素，壁、内边距、内容

盒子的三大部分：盒子壁，内边距，盒子内容

- 外边距 margin
- 盒子壁 border
- 内边距 padding（文字与盒子之间的距离）
- 盒子内容 width + height

<center>

![盒子模型](https://ambitionc-blog.oss-cn-hongkong.aliyuncs.com/Blog_Notes/2HTML%26CSS/2-2.png)

</center>

盒子模型：margin + border + padding + content（widht + height）

2. 盒子模型的嵌套问题

3. margin/border-with/padding为一个复合值

如果只有三个的时候，只代表上，左右，下。因为左右等距的情况更多

只有两个的时候，代表上下，左右。

```css
padding: 100px 150px 200px 250px;   //顺时针，上右下左 
```

4. 例如有以下的divCSS文件

```css
div{     
  width: 100px;     
  height: 100px;     
  background-color: red;     
  border: 10px solid black;     
  padding: 10px 20px 30px     
  margin: 10px 20px; 
} 
```

则这个盒子的

- 实际宽度realWidth：160px
- 实际高度realHeight：160px

**其中需要注意的是不包含margin，盒模型不考虑margin**

5. 盒模型的应用：远视图

```html
<div class="wrapper">
    <div class="box">
        <div class="content">
            <div class="content1"></div>
        </div>
    </div>
</div>
```

```css
.content1{
  height: 10px;
  widht: 10px;
  background-color: #fff;
}  
.content{     
  height: 10px;     
  width: 10px;     
  padding: 10px;     
  background-color: #0f0;
}  
.box{     
  height: 30px;     
  width: 30px;    
  padding: 10px;     
  background-color: #fff; 
}  
.wrapper{     
  height: 50px;     
  width: 50px;     
  padding: 10px;     
  background-color: #0f0;
} 
```

6. 盒模型的margin可以用于行内的元素的距离
7. **body有一个天生的margin为8像素**
8. 定位

- 定位：让特定的元素在特定的地方出现

- position可以设置的值为：

  （1）absolute，为绝对的位置，通常需要和left、top、bottom、right配合使用，left与right通常不一起使用

  left为左边线距离左边多少距离，right为右边线距离右边多少距离，top、bottom亦然

```css
{
  position: absolute; 
	left: 20px; 
  top: 300px;
} 
```

- **脱离原来位置进行定位（层模型）：当一个元素采用absolute绝对定位时，它就脱离了原来的层进入上一个层中。如**

```html
<div class="demo"></div>
<div class="box"></div>
```

```css
.demo{     
  position: absolute;     
  width: 100px;     
  height: 100px;     
  background-color: red;     
  opacity: 0.5 
} 
.box{     
  width:150px;     
  height: 150px;     
  background-color: green; 
} 
```

- **相对于最近的有定位的父级进行定位，如果没有，那么相对于文档进行定位。如**

（2）relative，为相对定位的元素

- **保留原来位置进行定位**

```html
<div class="demo"></div>
<div class="box"></div>
```

```css
.demo{
    position: relative;
    width: 100px;
    height: 100px;
    background-color: red;
    opacity: 0.5
}
.box{
    width:150px;
    height: 150px;
    background-color: green;
}
```

- **相对于自己原来的位置进行定位**

```html
<div class="wrapper">
    <div class="content">
        <div class="box"></div>
    </div>
</div>
```

```css
.wrapper{
    margin-left: 100px;
    width: 200px;
    height: 200px;
    background-color: orange;
}

.content{
    margin-left: 100px;
    width: 100px;
    height: 100px;
    background-color: black;
}

.box{
    position: relative;
    right: 50px;
    width: 50px;
    height: 50px;
    background-color: yellow;
}
```

**【工程经验】用relative作为参照物，absolute进行定位**

- **relative为保留原来位置进行定位，absolute为脱离原来位置定位**

（3）fixed：固定定位，常用于广告定位

```html
<div>apple</div>
<br>*100
```

```css
*{
    margin: 0;
    padding: 0;
}

div{
    position: fixed;
    width: 100px;
    height: 100px;
    top: 50%;
    background-color: red;
}
```

如果需要居中的话（相对于文档居中）

```css
div{
    position: fixed;
    left: 50%;
    top: 50%;
    width: 100px;
    height: 100px;
    background-color: red;
    margin-left: -50px;    //之前为左边的顶点为居中，如果想要实现整体的居中，则需要左上偏移
    margin-top: -50px;
}
```

### 2.4 浮动模型

### 2.5 补充知识点