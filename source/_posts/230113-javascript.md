---
title: 前端基础(2)-javascript
img: 'http://pic.tanzhang.work/blog/gallary/230113.png!up.webp'
top: false
cover: false
toc: true
categories: 前端
tags:
  - javascript
abbrlink: bf59699a
date: 2022-12-09 23:12:05
coverImg:
---
有了 html 和 css，我们可以编写出漂亮的静态页面，但如果需要给页面让页面产生更丰富的动态效果，则需要使用到 javascript。javascript 也是前端中一门重要的基础语言，其主包含如下3部分：

- ECMAScript：ES 定义了JavaScript一些基础语法和关键字(分支,循环, + - * /......)；
- DOM 模块：Document Object Model 文档对象模型，将Html元素对象封装到一个类；
- BOM 模块：Browser Object Model 浏览器对象模型，将浏览器的一些数据封装到类里面；

**javascript 使用方法**

- 写在head里面的script标签里面；
- 写在body中的script标签里面；
- 写在html标签的事件里面，如 onclick 事件；
- 写在单独的js文件里面，通过script标签引入，该script标签只做引入使用，中间不要再写js代码.

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<!-- <script type="text/javascript"></script> -->
	</head>
	<body>
		<script type="text/javascript">
			// 使用js向页面输出一个内容
			document.write("<a href='http://www.baidu.com'>这是一个标题</a>")
		</script>
	</body>
</html>
```

## 1基础语法

### 1.1接受页面输入的内容（注意：接受的内容为字符串类型）

```javascript
var num=prompt("兄弟,你的密码是多少?");
document.write(num);
```

### 1.2声明变量

1、var 声明全局变量

```javascript
var
// var 变量名=值
// 变量命名: 只能使用a-z  A-Z  0-9  _  $
// 注意: 不能够使用数字开头,不能使用关键字;
// 不建议使用$开头
var str="你好!";
document.write(str);
```

2、let 声明局部变量，声明方法跟 var 类似
3、const 声明常量

### 1.3js中的基础数据类型

```javascript
string：字符串，字符串需要用单引号或者双引号引起来；
var str = "aaa";
number：数值类型，包括数整数、小数；
var num = 100;
boolean：布尔类型，只有两个值 true 正确，false 错误；
var bool = true;
undefined：未定义，一个变量创建出来，但是没有赋值，类型就是 undefined；
var und;
null：空，什么都没有；
var nul = null;
```

4.查看某个变量的数据类型

```javascript
var str=242324;
var typ=typeof(str);
document.write(typ);
```

5.数据类型的强制转换

```javascript
var num1=prompt("请输入第一个数值");
var num2=prompt("请输入第二个数值");
num1=parseInt(num1);
num2=parseInt(num2);
var num4=num2-num1;
document.write(num4);
```

### 1.4运算符和控制结构

js 的运算符和控制结构与 java 的是类似的；
特殊：

```javascript
==、!= 只比较数值是否相等
===、!== 会比较数值和类型
```

隐式类型转换：

- undefined、""、0、null 在 if 语句中作为条件会自动转换为 false；
- 非0、非空串、非null 在 if 语句中作为条件会自动转换为 true；

## 2.特殊数据类型

### 2.1数组

js 中的数组是变长的，可以存储任何数据类型；

```javascript
object：对象；
var obj = {};
// array：数组，可以存多个数据；
var arr = [1,2,3,"zhangsan"];
var arr1 = new array();
var arr2 = new array(1,2,3);
function：函数，实现了某些功能的代码的集合；
```

1.在数组的末尾追加数据

```javascript
var arr = [1,2,3];
arr.push(666,777);
document.write(arr);
```

2.在数组的前面追加数据

```javascript
arr.unshift(0);
document.write(arr);
```

3.在数组中间插入/替换数据

```javascript
// 参数1:在哪个下标位置开始插入/替换数据
// 参数2:要替换数据的个数
// 参数3:要插入的数据
arr.splice(2,1,666,88,99);
document.write(arr);
// arr.splice() 还可用于修改,删除数据
```

4.删除最前面的数据，并且将删除的数据返回

```javascript
var aa=arr.shift();
document.write(arr);
document.write(aa);     
```

5.删除末尾数据，并且返回被删除的数据

```javascript
var aa=arr.pop()
document.write(arr)
document.write(aa)
```

6.使用splice()方法删除任意位置的数据

```javascript
arr.splice(a,b);
// a表示开始删除下标，b表示删除数据个数
```

7.使用length--删除最后的数据

```javascript
arr.length--;
document.write(arr);
```

8.将数值转换为字符串

```javascript
arr.join("-");
// 将数组中的数据拼接，不传参时默认使用逗号拼接
```

9.数组自定义排序

```javascript
var arr=[1,5,2,65,35,57,64];
arr.sort(function(a,b){ //function定义排序规则
    return a-b;
});
```

### 2.2函数

函数是实现了一定功能的代码的集合；

#### 2.2.1函数的声明方式

```javascript
// 方式1：函数声明式: function 函数名(参数列表){ } 
function add(a, b) { }

// 方式2：函数表达式: var 变量名 = function(参数列表){ }
var add2 = function(a,b) { }
调用: var a = add2(5,6);

// 方式3：函数可以作为另一个函数的返回值
var f = function(a,b){
	var c = a+b;
	return function(){
		console.log("返回值函数里面的内容");
	}
}
调用: var f1 = f(1,2);
```

函数是属于js中的一种数据类型 function：

```javascript
var add = function add(a, b) { }
console.log(typeof(add2));
```

## 3.函数和变量的提升

js中变量和函数的提升遵循以下三个原则：

- js在解析的时候会将变量的声明提升到当前作用域的最前面，只提升声明，不提升赋值；
- js在解析的时候会将函数的声明提升到当前作用域的最前面，只提升声明，不提升调用；（这条规律仅针对以函数声明式方式声明的函数，而使用函数表达式声明的函数，提升效果跟变量提升是一样的）
- 先提升变量，后提升函数；

### 3.1变量提升案例

```javascript
console.log(a);
var a = "a";
var foo = () => {
    console.log(a);
    var a = "a1";
}
foo();
//打印结果：
//undefined
//undefined
```

上述代码的实际执行顺序如下：

```javascript
var a;//全局作用域
console.log(a); // undefined
a = "a";
var foo = () => {//函数作用域
    var a; // 全局变量会被局部作用域中的同名变量覆盖
    console.log(a); // undefined
    a = "a1";
}
foo();
```

### 3.2函数提升案例

```javascript
console.log(foo1); // [Function: foo1]
foo1(); // foo1
console.log(foo2); // undefined
foo2(); // TypeError: foo2 is not a function
function foo1 () {
	console.log("foo1");
};
var foo2 = function () {
	console.log("foo2");
};
```

## 4.json对象

### 4.1 创建 json 对象

```javascript
//1.直接声明
var zhangsan = {
    "name":"张三"
};
//2.借助Object对象
var lisi = new Object();
lisi.name = "李四";
//3. 创建对象方式3: 函数工厂模式
function Person(name){
    var person = new Object();
    person.name = name;
    person.eat = function(){
        console.log("开吃");
    }
    return person;
}
var wangwu = Person("王五");
//4. 创建对象方式4: 对象工厂模式
function Student(name){
    this.name = name;
}
var zhaoliu = new Student("赵六");
```

### 4.2 json对象属性和方法的操作

```javascript
// 1.调用对象的属性和方法
zhangsan.name;
zhangsan["name"];
zhangsan.eat();
zhangsan["eat"]();
// 2.增加属性和方法
zhangsan.wife="李四";
zhangsan["wife2"]="老王";
zhangsan.sleep=function(){
    console.log("睡觉的行为");
}
// 3.修改属性和行为
zhangsan.wife = "王五";
// 4.删除属性和行为
delete zhangsan.wife;
// 5.找出所有属性和行为
for(var i in zhangsan){
    console.log(zhangsan[i]);
}
```

### 4.3 时间日期对象

```javascript
//时间日期类
var date = new Date();
//取出里面每一个值: 年-月-日 时:分:秒
var year = date.getFullYear();
var month = date.getMonth()+1;	//格林威治时间 0-11,需要对月份+1
if(month<10){
    month = ""+0+month;
}
//month=month<10?"0"+month:month;
var day = date.getDate();
if(day<10){
    day = ""+0+day;
}
var hour = date.getHours();
if(hour<10){
    hour = ""+0+hour;
}
var minutes = date.getMinutes();
if(minutes<10){
    minutes = ""+0+minutes;
}
var seconds = date.getSeconds();
if(seconds<10){
    seconds = ""+0+seconds;
}
console.log(year+"-"+month+"-"+day+" "+hour+":"+minutes+":"+seconds);
```
