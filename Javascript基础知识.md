
[1. Javascript简介](#1)

[2. 严格模式(use strict)](#2)

[3. Javascript引用](#3)

[4. 变量](#4)
- [4.1 局部作用域](#4.1)
- [4.2 常量](#4.2)
- [4.3 变量提升](#4.3)
- [4.4 命名规则](#4.4)

[5. 数据类型](#5)
- [5.1 检测类型](#5.1)
- [5.2 Javascript中的数据值](#5.2)
- [5.3 复制变量值](#5.3)
- [5.4 传递参数](#5.4)
- [5.5 数据自动转换的机制](#5.5)

[6. 字符串](#6)

[7. 数组](#7)

[8. 流程控制语句](#8)
- [8.1 JS条件语句](#8.1)
- [8.2 JS循环语句](#8.2)


<h1 id="1">Javascript</h1>

javascript是一种专为与网页交互儿设计的脚本语言。由三部分组成：
- ECMAScript  (ECMA-262定义)  提供核心语言功能
- 文档对象模型（DOM）提供访问和操作网页内容的方法和接口
- 浏览器对象模型（BOM）提供与浏览器交互的方法和接口

JavaScript是一种可以与HTML标记语言混合使用的脚本语言，其编写的程序可以直接在浏览器中解释执行

javascript是一种解释型语言(预编译、执行)

Javascript的国际标准是ECMAScript.
- 语法、类型、语句、关键字、保留字、操作符、对象

<h1 id="2">严格模式(use strict)</h1>

`"use strict";`的目的是指定代码在严格条件下执行。

为什么使用严格模式:

消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;  
- 消除代码运行的一些不安全之处，保证代码运行的安全；
- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript做好铺垫。

"严格模式"体现了Javascript更合理、更安全、更严谨的发展方向，包括IE 10在内的主流浏览器，都已经支持它，许多大项目已经开始全面拥抱它。

另一方面，同样的代码，在"严格模式"中，可能会有不一样的运行结果；一些在"正常模式"下可以运行的语句，在"严格模式"下将不能运行。掌握这些内容，有助于更细致深入地理解Javascript，让你变成一个更好的程序员。

**"use strict" 指令只允许出现在脚本或函数的开头**

<h1 id="3">javascript引用</h1>

```javascript
<!-- 外部引入文件 src属性 -->
<!-- 解析顺序 从上到下 边解析边执行 -->
<!-- 延迟执行：defer 可以延迟执行代码（当页面都加载完毕以后window.onload）  -->

<script type=text/javascript charset=utf-8 defer="defer" src='../commons/001.js'></script>
// ..访问上级文件夹
<script type=text/javascript charset=utf-8 >
	alert('我是内部代码!!!!');
</script>
```

<h1 id="4">变量</h1>

<h3 id="4.1">局部作用域</h3>

由于JavaScript的变量作用域实际上是函数内部，我们在for循环等语句块中是无法定义具有局部作用域的变量的：
```JavaScript
function foo() {
    for (var i=0; i<100; i++) {
        //
    }
    i += 100; // 仍然可以引用变量i
}
```

为了解决块级作用域，ES6引入了新的关键字let，用let替代var可以申明一个块级作用域的变量：
```javascript
function foo() {
    var sum = 0;
    for (let i=0; i<100; i++) {
        sum += i;
    }
    // SyntaxError:
    i += 1;
}
```

<h3 id="4.2">常量</h3>

由于var和let申明的是变量，如果要申明一个常量，在ES6之前是不行的，我们通常用全部大写的变量来表示“这是一个常量，不要修改它的值”：`var PI = 3.14;`

ES6标准引入了新的关键字`const`来定义常量，const与let都具有块级作用域：  
`const PI = 3.14;`

<h3 id="4.3">变量提升</h3>

函数声明和变量声明总是会被解释器悄悄地被"提升"到方法体的最顶部.

`var a;`  
`function(){}`

为了避免一些问题，通常我们在每个作用域开始前声明这些变量，这也是正常的 JavaScript 解析步骤，易于我们理解

`JavaScript 严格模式(strict mode)不允许使用未声明的变量。`


<h3 id="4.4">命名规则</h3>

- js, url参数： 驼峰
- css: 中划线（兼容也最好）
- 文件： 下划线

<h1 id="5">数据类型</h1>

ECMAScript中,数据类型也分为基本类型和引用类型两大类.

### 基本数据类型：Number、Boolean、String、Undefined、Null

- Number：整数和小数(最高精度17位小数)、NaN、Infinity,-Infinity    
  + 除10进制外，还可通过8进制和16进制的字面值来表示，如  	 070 表示56、0xA表示10.
  + 小数为浮点类型，if(a+b == 0.3) //不要做这样的测试，因为	 浮点数值最高精度是17位，而是0.300000000000000004.
- Undefined：表示变量声明但未赋值.
- Null:表示一个空的对象引用(也就是赋值为null)

### 引用类型：Object类型 (比如对象、数组、RegExp、Date...)

<h3 id="5.1">检测类型</h3>

- `Typeof` 操作符: 可以使用 typeof 操作符来查看 JavaScript 变量的数据类型。

![](https://raw.githubusercontent.com/zheng782912/Javascript-study-notes/master/images/basics/clipboard.png)

- `instanceof` 检测**引用类型**的值：`result = variable instanceof constructor`
    - 根据规定，所有引用类型的值都是 Object 的实例。因此，在检测一个引用类型值和 Object 构造函数时，instanceof 操作符始终会返回 true。当然，如果使用 instanceof 操作符检测基本类型的值，则该操作符始终会返回 false，因为基本类型不是对象。

<h3 id="5.2">Javascript中的数据值有两大类：基本类型的数据值和引用类型的数据值。</h3>

- 基本类型是按照值访问的，因为可以操作保存在变量中的实际值
    - 不能给基本类型的值添加属性
- 引用类型则是按引用去访问的
    - 可以为其添加属性和方法，也可以改变和删除其属性和方法

<h3 id="5.3">复制变量值</h3>

除了保存的方式不同之外，在从一个变量向另一个变量复制基本类型值和引用类型值时，也存在不同

- **复制基本类型值**: 
    - 会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上

```JavaScript
var num1 =5;
var num2 = num1;
//num2中的5与num1中的5是完全独立的,该值只是num1中5的一个副本.
```

- **复制引用类型值**: 
    - 同样也会将存储在变量对象中的值复制一份放到为新变量分配的空间中
    - 不同的是，这个值的副本实际上是一个指针，而这个指针指向存储在堆中的一个对象。复制操作结束后，两个变量实际上将引用同一个对象
    - 因此，改变其中一个变量，就会影响另一个变量.

```JavaScript
var obj1 = new Object();    //obj1 保存了一个对象的新实例
var obj2 = obj1;    //这个值被复制到了obj2中
obj1.name = "Nicholas";
console.log(obj2.name); //"Nicholas"
//obj1 和 obj2 都指向同一个对象
```
![](https://raw.githubusercontent.com/zheng782912/Javascript-study-notes/master/images/basics/clipboard-2.png)

<h3 id="5.4">传递参数</h3>

ECMAScript 中所有函数的参数都是按值传递的。

也就是说，把函数外部的值复制给函数内部的参数，就和把值从一个变量复制到另一个变量一样。

基本类型值的传递如同基本类型变量的复制一样，而引用类型值的传递，则如同引用类型变量的复制一样。

访问变量有按值和按引用两种方式，而**参数只能按值传递**

- **参数传递基本类型的值**: 被传递的值会被复制给一个局部变量（即命名参数，或者用ECMAScript 的概念来说，就是 arguments 对象中的一个元素

```JavaScript
function addTen(num){
    num += 10;  //不会影响函数外部的 count 变量
    return num; //参数 num 与变量 count 互不相识
}
var count = 20;
var result = addTen(count);
console.log(count); //20 没有变化
console.log(result);    //30
```

- **参数传递引用类型的值**: 会把这个值在内存中的地址复制给一个局部变量，因此这个局部变量的变化会反映在函数的外部

```JavaScript
function setName(obj){
    obj.name = "Nicholas",
    obj = new Object(),
    obj.name = "Greg"
}

var person = new Object();
setName(person);
console.log(person.name);   //"Nicholas"
```


<h3 id="5.5">数据自动转换的机制</h3>

```JavaScript
var a = "1" ; 		//number
var b = true ; 		//boolean

if(a == b){
	alert('相等');
} else {
	alert('不等');
} 
//相等

// == 表示 可以经过自动转换 比较的是数值 
// === 表示 可以经过自动转换 先比较值, 再比较数据类型
```

<h1 id="6">字符串</h1>

字符串可以存储一系列字符，如 "John Doe"。

字符串可以是插入到引号中的任何字符。你可以使用单引号或双引号：

```javascript
var carname = "Volvo XC60";
var carname = 'Volvo XC60';
```
你可以使用索引位置来访问字符串中的每个字符：

```javascript
var character = carname[7];
```

字符串的索引从 0 开始，这意味着第一个字符索引值为 [0],第二个为 [1], 以此类推。

你可以在字符串中使用引号，字符串中的引号不要与字符串的引号相同:

```javascript
var answer = "It's alright";
var answer = "He is called 'Johnny'";
var answer = 'He is called "Johnny"';
```

你也可以在字符串添加转义字符来使用引号：

```javascript
var x = 'It\'s alright';
var y = "He is called \"Johnny\"";
```

反斜杠( \ )是一个转义字符。 
- 转义字符将特殊字符转换为字符串字符
- 转义字符 ( \ ) 可以用于转义撇号，换行，引号，等其他特殊字符


<h1 id="7">数组</h1>

1. 定义了一个空数组:(常规)

```javascript
var myCars=new Array();
myCars[0]="Saab";      
myCars[1]="Volvo";
myCars[2]="BMW";

我们创建数组的同时，还可以为数组指定长度，长度可任意指定。
var myarray= new Array(8); //创建数组，存储8个数据。 
```

2. 定义时指定有n个空元素的数组：(简洁)

```javascript
var 数组名 =new Array(n);
var myCars=new Array("Saab","Volvo","BMW");
```

3. 定义数组的时候，直接初始化数据：(字面)

```javascript
var myCars=["Saab","Volvo","BMW"];
var myArray = [2, 8, 6]; 
var 数组名 = [<元素1>, <元素2>, <元素3>...];
```

请注意，如果通过索引赋值时，索引超过了范围，同样会引起Array大小的变化：

```javascript
var arr = [1, 2, 3];
arr[5] = 'x';
arr; // arr变为[1, 2, 3, undefined, undefined, 'x']
```

### 二维数组

二维数组的定义方法
1. 


```JavaScript
var myarr=new Array();  //先声明一维 

for(var i=0;i<2;i++){   //一维长度为2
   myarr[i]=new Array();  //再声明二维 
   for(var j=0;j<3;j++){   //二维长度为3
        myarr[i][j]=i+j;   // 赋值，每个数组元素的值为i+j
   }
 }
```

2.

```JavaScript
var Myarr = [[0 , 1 , 2 ],[1 , 2 , 3]]

myarr[0][1]=5; //将5的值传入到数组中，覆盖原有值。

说明: myarr[0][1] ,0 表示表的行，1表示表的列。
```

创建二维数组(一维长度3，二维长度6)，值为一维数组和二维数组索引值的积，如myarr[2][5]=2*5。

```JavaScript
var myarr = new Array();

for(var i=0;i<3;i++){
    myarr[i] = new Array();
    for(var j=0;j<6;j++){
        myarr[i][j] = i*j;
        document.write("myarr["+i+"]["+j+"]的值:"+myarr[i][j]+"<br>");
    }
}

/*
myarr[0][0]的值:0
myarr[0][1]的值:0
myarr[0][2]的值:0
myarr[0][3]的值:0
myarr[0][4]的值:0
myarr[0][5]的值:0
myarr[1][0]的值:0
myarr[1][1]的值:1
myarr[1][2]的值:2
myarr[1][3]的值:3
myarr[1][4]的值:4
myarr[1][5]的值:5
myarr[2][0]的值:0
myarr[2][1]的值:2
myarr[2][2]的值:4
myarr[2][3]的值:6
myarr[2][4]的值:8
myarr[2][5]的值:10
*/
```







<h1 id="8">流程控制语句</h1>

null、undefined、0、NaN和空字符串''视为false，其他值一概视为true

<h3 id="8.1">JS条件:</h3>

- `if` 语句 - 只有当指定条件为 true 时，使用该语句来执行代码
- `if...else` 语句 - 当条件为 true 时执行代码，当条件为 false 时执行其他代码
- `if...else if....else` 语句- 使用该语句来选择多个代码块之一来执行
- `switch` 语句 - 使用该语句来选择多个代码块之一来执行

当有很多种选项的时候，`switch`比`if else`使用更方便:
```javascript
switch(n)
{
    case 1:
        执行代码块 1
        break;
    case 2:
        执行代码块 2
        break;
    default:
        与 case 1 和 case 2 不同时执行的代码
}
```

<h3 id="8.2">JS循环：</h3>

- `for` - 循环代码块一定的次数
- `for/in` - 循环遍历对象的属性
- `while` - 当指定的条件为 true 时循环指定的代码块
- `do/while` - 同样当指定的条件为 true 时循环指定的代码块

### 1. for循环

```javascript
var x=1;
for(var i=1;i<=10;i++){
	x*=i;
}
console.log(x);
//3628800

if(x===3628800){
	console.log('1 * 2 * 3 * .... *10 = ' + x);
}else{
	console.log("计算错误");
}
//1 * 2 * 3 * .... *10 = 3628800
```

### 2. for/in循环 : 循环遍历对象的每个属性

```javascript
var o ={
	name:'Jack',
	age: 20,
	city: 'Beijing'
};
for(var key in o){
	console.log(key);
}
// 'name','age','city'
```

由于Array也是对象，而它的每个元素的索引被视为对象的属性，因此，for ... in循环可以直接循环出Array的索引：

```javascript
var a = ['A','B','C'];
for(var i in a){
	console.log(i);
	//'0','1','2'
	console.log(a[i]);
	//'A','B','C'
}
```
    for ... in对Array的循环得到的是String而不是Number

### 3. while循环

for循环在已知循环的初始和结束条件时非常有用。而忽略了条件的for循环容易让人看不清循环的逻辑，此时用while循环更佳。

while循环只有一个判断条件，条件满足，就不断循环，条件不满足时则退出循环。

比如我们要计算100以内所有奇数之和，可以用while循环实现：

```JavaScript
var x =0;
var n =99;
while(n>0){
	x = x+n;
	n = n-2;
}
x;
//2500
//在循环内部变量n不断自减，直到变为-1时，不再满足while条件，循环退出

```

### 4. Do...while循环

do while结构的基本原理和while结构是基本相同的，但是它保证循环体**至少被执行一次**。因为它是先执行代码，后判断条件，如果条件为真，继续循环。

```JavaScript
num= 1;
do
{
 console.log("数值为:" +  num);
 num++; //更新条件
}
while (num<=5)
//数值为:1
//数值为:2
//数值为:3
//数值为:4
//数值为:5

```

`用do { ... } while()循环要小心，循环体会至少执行1次，而for和while循环则可能一次都不执行。`

`break`的作用是跳出代码块, 所以 break 可以使用与循环和 switch 等.  

`continue` 的作用是进入下一个迭代, 所以 continue 只能用于循环的代码块。










