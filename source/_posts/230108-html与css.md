---
title: 前端基础(1)-html与css
img: 'http://pic.tanzhang.work/blog/gallary/230108.jpg!up.webp'
top: false
cover: 'http://pic.tanzhang.work/blog/gallary/230108.jpg!up.webp'
toc: true
categories: 前端
tags:
  - html
  - css
abbrlink: 7777147d
date: 2022-11-12 17:20:16
coverImg:
---
作为一名后端开发人员，偶尔也会需要一点前端的知识，以备不时之需。笔者原本也有是有一点前端基础的，奈何太久不用全都忘光了，最近突然想写点前端相关的东西，然而拿起电脑发现有点无法下手，陷入茫然。也罢，趁这次机会，正好把以前学的点基础东西整理以下，做成一个小系列，类似笔记的方式，方便今后回顾。

## 1.HTML组成

html 页面由3部分组成

```html
<!DOCTYPE html>   <!--声明:告诉浏览器,这是一个html文件,遵循html5规范,必须写到第一行.-->
<html> <!--根标签,是页面最顶层的标签,这个标签里面要包含两对标签head body.-->
    <head>
        <meta charset="UTF-8">   <!--设置页面编码格式-->
        <title>hello world</title>    <!--设置页面标题-->
    </head>
    <body>  <!--页面的所有内容都要写到body中.-->
    </body>
</html>
```

## 2.重要标签

### 2.1属性

标签的一种特性，例如：

```html
<img src="" />
<!-- src就是标签的属性 -->
```

### 2.2特殊标签

**1.表单 input 标签**

```html
<form action="http://www.baidu.com" method="post">
	<input type="text" name="username" value="a1234">
	<input type="submit" value="登录">
</form>
form表单: 将用户输入的信息提交到后台；
表单域: 使用form标签来确定, action表示提交的地址，method表示发送请求的方式；
input标签: type表示输入框的类型,value表示输入框里面的内容;
type可选项：
	button: 表示的是一个普通按钮
	submit: 将表单的内容提交到action地址
	radio: 单选框
	<input type="radio" name="sex" value="男">男<input type="radio" name="sex" value="女">女
	checkbox: 复选框
	<input type="checkbox" name="hobby" value="游泳">游泳<input type="checkbox" name="hobby" value="洗澡">洗澡
	select/list: 下拉框
	<input type="text" list="list">
	<datalist id="list">
		<option>重庆</option>
		<option>成都</option>
		<option>观音桥space</option>
		<option>红旗河沟</option>
	</datalist>
	email: 邮箱
	number: 只能输入数字
	date: 输入日期
	color: 颜色
	reset: 重置
input 其他属性：
	autofocus：自动获取焦点；
	placeholder：提示信息；
	disabled：禁用
```

**2.表格 table 标签**
表格标签：table、thead、tbody、tfoot 用来表示表格的部位，无太大作用；
table 属性：
cellspacing: 取消单元格与单元格之间的间隙
cellpadding: 设置单元格与文字之间的间距
align="center" 让表格相对于父级元素居中
行：tr
单元格：td、th(里面的内容自动加粗,居中)

## 3.CSS层叠样式

css书写方式有3种，分别如下：

- 行内样式：在元素中使用style属性去写css样式；
- 内联样式：在head中写一对style标签，然后在标签中设置样式；
- 外联样式：将css样式单独写到一个css文件中,在需要使用的地方导入就ok，提高代码可复用性；

### 3.1css选择器

#### 3.1.1普通选择器

使用选择器选择需要添加样式的元素，给他们设置相应的样式

```css
/* id选择器:选择页面上某一个元素, 同名id在页面中只能使用一次 */
#id值{
    css属性:值;
    css属性:值;
}
/* 元素选择器/标签选择器:选择页面上这个名字的所有元素 */
标签名{
    css属性:值;
    css属性:值;
}
/* 类选择器:选择页面某一具有相同样式的元素, class可以多次重复使用 */
.class名{
    css属性:值;
    css属性:值;
}
```

例如：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title>css层叠样式</title>
		<style type="text/css">
			/*id选择器*/
			#p01{
				color:red;
				font-size:30px;
			}
			/*标签选择器*/
			p{
				color:red;
			}
			/*类选择器*/
			.cla{
				color:red;
			}
		</style>
	</head>
	<body>
		<p id="p01">这是p1标签</p>
		<p>这是p2标签</p>
		<h1 class="cla">这是h02标签</h1>
	</body>
</html>
```

**3.1.2多类名选择器**
一个class属性里面可以有多个类名，多个类名之间用空格隔开：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title></title>
        <style>
            .f-size{
                font-size: 66px;
            }
            .b-color{
                color: blue;
            }
        </style>
    </head>
    <body>
        <span class="f-size b-color">小葱拌豆腐</span>
    </body>
</html>
```

#### 3.1.3组合选择器

组合选择器包括以下四种：

```css
/* 选择器1,选择器2的所有元素 */
选择器1,选择器2 {
    样式1: 值;
    样式2: 值;
}
/* 选择器1所有的后代选择器2元素 */
选择器1 选择器2 {
    样式1: 值;
    样式2: 值;
}
/* 选择选择器1的亲儿子 */
选择器1>选择器2 {
    样式1: 值;
    样式2: 值;
}
/* 选择器1的下一个符合条件的元素 */
选择器1+选择器2 {
    样式1: 值;
    样式2: 值;
}
```

例如：

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            p,div{
                color: red;
            }
            #t p{
                color: green;
            }
            #s>p{
                color: rgb(14, 8, 7);
            }
        </style>
    </head>
    <body>
        <p>旋涡名人</p>
        <div>佐助</div>
        <p>雏田</p>
        <div id="t">
            <p>小樱</p>  <!-- 儿子辈 -->
            <div>大蛇丸</div>
            <div>
                <p>小蛇丸</p>  <!-- 孙子辈 -->
            </div>
        </div>
        <div id="s">
            <p>小樱</p>  <!-- 儿子辈 -->
            <div>大蛇丸</div>
            <div>
                <p>小蛇丸</p>  <!-- 孙子辈 -->
            </div>
        </div>

    </body>
</html>

```

#### 3.1.4伪类选择器

**只 a 标签可用**
link:设置链接访问前的样式
visited:设置访问过后的链接样式
active:设置按住鼠标左键不放的样式
**所有标签可用**
hover:鼠标移入的样式
如果需要使用多种伪类选择器叠加样式，需要按 link、visited、hover、active 的顺序使用；

```html
<style type="text/css">
	a:link{
	color:red;
	}
	a:visited{
	color:green;
	}
	a:active{
	color:#2596FA;
	}
	font:hover{
		background-color:red;
	}
</style>
```

#### 3.1.5通配符选择器

选择当前页面的所有元素

```css
*{
    color: red;
}
```

#### 3.1.6结构伪类选择器

```css
li:first-child{
    color: red;
}
li:last-child{
    color: blue;
}
li:nth-child(3){
    color: yellow;
}
li:nth-child(2n){
    color: pink;
}
```

### 3.2css的特性

#### 3.2.1继承特性

子元素会继承父元素的一些样式

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style>
			#a{
				color: red;
			}
		</style>
	</head>
	<body>
		<p id="a">
			<span>hello</span>
		</p>
	</body>
</html>
```

#### 3.2.2层叠特性

多个样式作用在同一个元素上，样式会进行层叠

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style>
			div {
				color: red;
			}
			#a {
				height: 100px;
			}
		</style>
	</head>
	<body>
		<div id="a">hello</div>
	</body>
</html>
```

#### 3.2.3权重

css样式有权重区分，权重大小如下所示：

```
继承过来的样式     标签选择器     类选择器/伪类选择器     id选择器     行内样式
权重:	0      <    1(员工)    <   1(部门主管)      <     1(经理)  <   1(总经理)
```

css权重遵循如下原则：

1. 继承过来的样式权限为0；
2. !important 标记的权重无限大；
3. 同级别的来,权重谁大谁说了算；
4. 不同级别的来,谁的级别大,谁说了算；
5. 权重完全相同,遵循就近原则；

## 4.盒模型

典型的有 span 标签和 div 标签

- span 标签只能装字体，不换行；
- div 可以装任何东西，独占一行；

盒模型：页面的所有元素都可以看做一个盒子；
盒子包含：内边距padding、外边距margin（默认为0）、线宽border、内容区；
盒子大小：（内边距 + 外边距 + 线宽）* 2 + 内容区；
内外边距属性值有如下设置方式

```css
/* 上下左右都相等 */
margin: 参数;
/* 参数1:上下边距, 参数2:左右边距 */
margin: 参数1 参数2;
/* 参数1:上边距, 参数2:左右边距, 参数3:下边距 */
margin: 参数1 参数2 参数3;
/* 上、右、下、左边距 */
margin: 参数1 参数2 参数3 参数4;
/* 参数1:上下边距, auto:相对于父级元素居中 */
margin: 参数1 auto;
```

如下css设置会将 border 和 padding 数值包含在 width 和 height 之内，这样的好处就是修改 border 和 padding 数值时盒子的大小不变，内容大小会自动适应，此时盒子大小计算方式变化为：
外边距*2 + 盒子宽度（内容区 + 内边距*2）

```css
box-sizing:border-box;
```

## 5.html分类

html 标签主要分为以下三类：

- block：块级元素，可以设置宽高，并且会默认独占一行的元素，下一个元素会自动换行；

> div、p、h1~h6、table、br、hr、ol/ul（li）、select（option）、fieldset（legend）

- inline：行内元素，不可以设置宽高，不会默认占一整行；

> font、img、a、span、input、b、small、i、del、u、strong、button、audio、video

- inline-block：行内块元素，可以设置宽高，但是不会占用一整行；

行内元素和块级元素可以相互转换，通过如下属性配置：

```css
/* 将元素转换成块级元素 */
display: block;
/* 将元素转换为行内元素 */
display: inline;
/* 将元素转换为行内块元素 */
display: inline-block;
```

### 5.1边界塌陷

边界塌陷分为两种情况，父子边界塌陷和兄弟边界塌陷；
边界塌陷产生的条件：边界塌陷只会在**垂直方向**上发生，且发生塌陷的元素是**块级元素**；

##### 兄弟边界塌陷

对于兄弟元素产生边界塌陷，塌陷后垂直间距等于二者中 margin 的较大值；
解决办法可以直接将目标的间距直接累加然后添加到一个元素上面；

##### 父子边界塌陷

父子元素产生边界塌陷，父元素会随子元素一起向下或向上移动；
解决办法可以为父元素添加 border 或者 padding，或者为父元素 overflow: hidden 样式；

### 5.2浮动与定位

#### 5.2.1div浮动

可以通过 css 设置div浮动效果，使div 脱离标准文档流；

```css
float: left/right;
```

#### 5.2.2定位

元素定位的模式为：定位模式 + 边偏移；
**定位模式**分为4种：

1. static（静态）：默认模式；
2. fixed（固定位置）：相对于浏览器(body)进行定位；
3. relative（相对定位）：相对于div原来的位置进行定位，保持对原有的位置的占有；
   z-index: 3; 设置元素重叠时的重叠关系，默认为1，数值越大层叠到越上层；
4. absolute（绝对定位）：相对于其父级第一个拥有定位的元素进行定位,如果其父级元素都没有定位,则相对于body进行定位。

**边偏移**
top、left、right、bottom，只需要给2个偏移量，一个水平偏移量，一个垂直偏移量

```html
<style type="text/css">
	#div02 {
		border: 3px solid red;
		height: 50px;
		width: 50px;
		position: absolute;
		top: 100px;
		left: 100px;
	}
</style>
```

**定位的常用方法**：父级元素使用相对定位，子元素使用绝对定位（子绝父相）；

### 5.3元素的显示和隐藏

元素的隐藏分为两种模式

```css
/* 隐藏后不再占有位置 */
display: none;
/* 隐藏后依然占有位置 */
visibility: hidden;
```

### 5.4 before-after伪元素

通过 before 或者 after 可以为标签添加一些内容以外的元素

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style>
			li::after {
				content:">";
			}
		</style>
	</head>
	<body>
		<ul>
			<li>这是第一个1</li>
			<li>这是第一个2</li>
		</ul>
	</body>
</html>
```

## 6.css常用样式

```css
color、font-size、font-weight
border、width、height、background-image、background-size
text-align、padding、margin、line-height

font-family: 宋体;
border-spacing: 0;
border-radius: 25px; 设置倒角
cursor: pointer; 鼠标变小手
float: left; 浮动,脱离标准文档流
overflow: hidden; 
box-sizing: boder-box; 
vertical-align: middle; 
background: rgba(255,250,232,0.5); 最后一位表示不透明度, 范围0~1, 0表示透明
```
