
[DOM 节点](#2)

[DOM 方法](#3)

[DOM 属性](#4)
-   [childNodes与children 区别](#4.1)
-   [firstChild与firstElementChild区别](#4.2)

[DOM 访问](#5)

[DOM 修改](#6)

[DOM 事件](#7)
-   [DOM EventListener](#7.1)

[DOM 导航](#8)

W3C DOM 标准被分为 3 个不同的部分：

-   核心 DOM - 针对任何结构化文档的标准模型
-   XML DOM - 针对 XML 文档的标准模型
-   HTML DOM - 针对 HTML 文档的标准模型

DOM 是 Document Object Model（文档对象模型）的缩写。




<h1 id="1">HTML DOM </h1>

HTML DOM 是:

-   HTML 的标准对象模型
-   HTML 的标准编程接口
-   W3C 标准

HTML DOM 定义了所有 HTML 元素的对象和属性，以及访问它们的方法。

**换言之，HTML DOM 是关于如何获取、修改、添加或删除 HTML 元素的标准。**


通过 HTML DOM，可访问 JavaScript HTML 文档的所有元素。

当网页被加载时，浏览器会创建页面的文档对象模型（Document Object Model）。 

HTML DOM 模型被构造为对象的树：

![](https://raw.githubusercontent.com/zheng782912/Javascript-study-notes/master/images/DOM/pic_htmltree.gif) 

通过可编程的对象模型，JavaScript 获得了足够的能力来创建动态的 HTML。 

-   JavaScript 能够改变页面中的所有 HTML 元素
-   JavaScript 能够改变页面中的所有 HTML 属性
-   JavaScript 能够改变页面中的所有 CSS 样式
-   JavaScript 能够对页面中的所有事件做出反应

<h1 id="2">DOM 节点</h1>

根据 W3C 的 HTML DOM 标准，HTML 文档中的所有内容都是节点：

-   整个文档是一个文档节点
-   每个 HTML 元素是元素节点
-   HTML 元素内的文本是文本节点
-   每个 HTML 属性是属性节点
-   注释是注释节点

### 节点父、子和同胞

节点树中的节点彼此拥有层级关系。

父（parent）、子（child）和同胞（sibling）等术语用于描述这些关系。父节点拥有子节点。同级的子节点被称为同胞（兄弟或姐妹）。

-   在节点树中，顶端节点被称为根（root）
-   每个节点都有父节点、除了根（它没有父节点）
-   一个节点可拥有任意数量的子
-   同胞是拥有相同父节点的节点

下面的图片展示了节点树的一部分，以及节点之间的关系：

![](https://raw.githubusercontent.com/zheng782912/Javascript-study-notes/master/images/DOM/dom_navigate.gif)

操作一个DOM节点实际上就是这么几个操作：

-   更新：更新该DOM节点的内容，相当于更新了该DOM节点表示的HTML的内容；
-   遍历：遍历该DOM节点下的子节点，以便进行进一步操作；
-   添加：在该DOM节点下新增一个子节点，相当于动态增加了一个HTML节点；
-   删除：将该节点从HTML中删除，相当于删掉了该DOM节点的内容以及它包含的所有子节点。

<h1 id="3">DOM 方法</h1>

方法是我们可以在节点（HTML 元素）上执行的动作。

### 编程接口
可通过 JavaScript （以及其他编程语言）对 HTML DOM 进行访问。

所有 HTML 元素被定义为对象，而编程接口则是对象方法和对象属性。

方法是您能够执行的动作（比如添加或修改元素）。

属性是您能够获取或设置的值（比如节点的名称或内容）。

### HTML DOM 对象 - 方法和属性

一些常用的 HTML DOM 方法：

-   getElementById(id) - 获取带有指定 id 的节点（元素）
-   appendChild(node) - 插入新的子节点（元素）
-   removeChild(node) - 删除子节点（元素）

一些常用的 HTML DOM 属性：

-   innerHTML - 节点（元素）的文本值
-   parentNode - 节点（元素）的父节点
-   childNodes - 节点（元素）的子节点列表
-   attributes - 节点（元素）的属性节点

一些 DOM 对象方法

方法    |   描述
----    |   ----
getElementById()|返回带有指定 ID 的元素。
getElementsByTagName()|返回包含带有指定标签名称的所有元素的节点列表（集合/节点数组）。
getElementsByClassName()|返回包含带有指定类名的所有元素的节点列表。
appendChild()|把新的子节点添加到指定节点。
removeChild()|删除子节点。
replaceChild()|替换子节点。
insertBefore()|在指定的子节点前面插入新的子节点。
createAttribute()|创建属性节点。
createElement()|创建元素节点。
createTextNode()|创建文本节点。
getAttribute()|返回指定的属性值。
setAttribute()|把指定属性设置或修改为指定的值。

在操作一个DOM节点前，我们需要通过各种方式先拿到这个DOM节点

由于ID在HTML文档中是唯一的，所以`document.getElementById()`可以直接定位唯一的一个DOM节点。`document.getElementsByTagName()`和`document.getElementsByClassName()`总是返回一组DOM节点。要精确地选择DOM，可以先定位父节点，再从父节点开始选择，以缩小范围。

```JavaScript
// 返回ID为'test'的节点：
var test = document.getElementById('test');

// 先定位ID为'test-table'的节点，再返回其内部所有tr节点：
var trs = document.getElementById('test-table').getElementsByTagName('tr');

// 先定位ID为'test-div'的节点，再返回其内部所有class包含red的节点：
var reds = document.getElementById('test-div').getElementsByClassName('red');

// 获取节点test下的所有直属子节点:
var cs = test.children;

// 获取节点test下第一个、最后一个子节点：
var first = test.firstElementChild;
var last = test.lastElementChild;
```

严格地讲，我们这里的DOM节点是指`Element`，但是DOM节点实际上是`Node`，在HTML中，`Node`包括`Element`、`Comment`、`CDATA_SECTION`等很多种，以及根节点`Document`类型，但是，绝大多数时候我们只关心`Element`，也就是实际控制页面结构的`Node`，其他类型的`Node`忽略即可。根节点`Document`已经自动绑定为全局变量`document`。

```html
<!-- HTML结构 -->
<body>
    <div id="test-div">
        <div class="c-red">
            <p id="test-p">JavaScript</p>
            <p>Java</p>
        </div>
        <div class="c-red c-green">
            <p>Python</p>
            <p>Ruby</p>
            <p>Swift</p>
        </div>
        <div class="c-green">
            <p>Scheme</p>
            <p>Haskell</p>
        </div>
    </div>
</body>
```
请选择出指定条件的节点：

```javascript
// 选择<p>JavaScript</p>:
var js = document.getElementById("test-p");

// 选择<p>Python</p>,<p>Ruby</p>,<p>Swift</p>:
var arr = document.getElementsByClassName('c-red c-green')[0].getElementsByTagName('p');

// 选择<p>Haskell</p>:
var haskell = document.getElementById('test-div').lastElementChild.lastElementChild;
//var haskell = document.getElementsByClassName("c-green")[1].lastElementChild
```

<h1 id="4">DOM 属性</h1>

属性是节点（HTML 元素）的值，您能够获取或设置。


### nodeName 属性
nodeName 属性规定节点的名称。

-   nodeName 是只读的
-   元素节点的 nodeName 与标签名相同 
-   属性节点的 nodeName 与属性名相同
-   文本节点的 nodeName 始终是 #text
-   文档节点的 nodeName 始终是 #document

**注释：nodeName 始终包含 HTML 元素的大写字母标签名**

```html
<body>
    <p id="demo">请点击按钮来获得 body 元素子节点的节点名。</p>

    <button onclick="myFunction()">试一下</button>

    <p><b>注释：</b>元素中的空格被视作文本，而文本被视作文本节点。</p>
</body>
```

```javascript
function myFunction(){
    var txt="";
    var c=document.body.childNodes; //返回元素子节点的 NodeList
    
    for (i=0; i<c.length; i++){
        txt=txt + c[i].nodeName + "<br>";
    };
    
    var x=document.getElementById("demo");  
    x.innerHTML=txt;
}
```
![](https://raw.githubusercontent.com/zheng782912/Javascript-study-notes/master/images/DOM/nodeName.gif)

### nodeValue 属性

nodeValue 属性规定节点的值。

-   元素节点的 nodeValue 是 undefined 或 null
-   文本节点的 nodeValue 是文本本身
-   属性节点的 nodeValue 是属性值

```javascript
//<p id="intro">Hello World!</p>

x=document.getElementById("intro");
document.write(x.childNodes[0].nodeValue);
//元素内的文本节点被视作文本节点，因此我们返回p元素的首个子节点（childNodes[0]）的节点值。

//document.write(x.firstChild.nodeValue);
//P元素第一个子节点firstChild的节点值

/*
Hello World!
Hello World! 
*/
```

### nodeType 属性

nodeType 属性返回节点的类型。nodeType 是只读的。

比较重要的节点类型有：

元素类型|NodeType
----|----
元素|1
属性|2
文本|3
注释|8
文档|9

<h3 id="4.1">childNodes与children 区别</h3>

**1. childNodes属性**

标准的，它返回指定元素的子元素集合，包括html节点，所有属性，文本。可以通过nodeType来判断是哪种类型的节点，只有当nodeType==1时才是元素节点，2是属性节点，3是文本节点。如果代码中有换行、空格就会增加文本节点，这样用它来返回真正的子节点就会不准确，具体见下面的例子

除了IE9和Firefox，其他浏览器都支持通过childNodes[i]获取第i个子节点。

如果一定要用这个方法（毕竟他是W3C标准），就要增加一个判断子节点类型过程：

```javascript
    function getFirst(elem){  
        for(var i=0,e;e=elem.childNodes[i++];){  
            if(e.nodeType==1)  
                return e;  
        }         
    } 
```

节点列表不是一个数组！

节点列表看起来可能是一个数组，但其实不是。

你可以像数组一样，使用索引来获取元素。

节点列表无法使用数组的方法： valueOf(), pop(), push(), 或 join() 。

大部分浏览器的 querySelectorAll() 返回 NodeList 对象

    pcoll=document.querySelectorAll("p")

    plist=document.getElementsByTagName("p")

以上 pcoll 返回的就是固定的值。

而获取 plist 后, 若 html 页面有变化且刚好添加或移除了 p 标签, 此时plist也会跟着变。
    
**2. children属性**

非标准的，它返回指定元素的子元素集合。经测试，它只返回html节点，甚至不返回文本节点。且在所有浏览器下表现惊人的一致。和childNodes一样，在firefox下不支持()取集合元素。因此如果想获取指定元素的第一个html节点，可以使用children[0]来替代上面的getFirst函数。需注意children在IE中包含注释节点。

**返回指定元素的子元素集合，只包括元素节点，不包括文本节点。**

除了IE9和Firefox，其他浏览器都支持通过children[i]获取第i个子节点。

注意：children在IE中包含注释节点。

<h3 id="4.2">firstChild与firstElementChild区别</h3>

**1. firstChild属性：**

获取指定元素的第一个子节点，可以是元素节点，也可以是文本节点。

**2. firstElementChild属性：**

获取指定元素的第一个子元素节点，不会检测到文本节点。

- 问题：若父元素与第一个子元素之间存在空白节点，firstChild获取到的将是空白节点而不是第一个子元素。


- 解决：使用firstElementChild属性。


- 问题：IE6/7/8中不支持firstElementChild属性。


- 解决：使用children[0]属性。

### 总结+示例：

对于DOM元素

children是指DOM Object类型的子对象，不包括tag之间隐形存在的TextNode；

childNodes包括tag之间隐形存在的TextNode对象。

如果想获取到指定元素的子元素节点，最好使用children方法，childNodes方法及firstChild方法在现代浏览器中都会把空白节点检测出来，所以推荐以后使用children方法来替代childNodes。

具体看一下针对children和childNodes在chrome环境下的测试：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
</head>
<body>
<div id="div" class="div">
 <span id="span" class="span">
 </span>
</div>
</body>
<script type="text/javascript">
 
    function test() {
        var o = document.getElementById("div");
        var child = o.children;
        console.log("div.children运行结果:");
        for(i = 0; i < child.length; i++){
            console.log(child[i].tagName);
        }
 
        console.log("");
        child = o.childNodes;
        console.log("div.childNodes运行结果:");
        for(i = 0; i < child.length; i++){
            console.log(child[i].tagName);
        }
 
    }
 
    test();
 
</script>
</html>

测试结果如下：

/////////////////////////////////////////////////

div.children运行结果:

SPAN

/////////////////////////////////////////////////

div.childNodes运行结果:

undefined

SPAN

undefined

```
上面childNodes集合的结果中有两个undefined节点，这两个就是nodeType=3的TextNode。

如果把HTML代码写成如下样式，那么children和childNodes的结果就没有差别了。

```html
<div id="div" class="div"><span id="span" class="span"></span></div>
```





<h1 id="5">DOM 访问</h1>

访问 HTML DOM - 查找 HTML 元素。

### getElementById() 方法

getElementById() 方法返回带有指定 ID 的元素：
    
    node.getElementById("id");

### getElementsByTagName() 方法

getElementsByTagName() 返回带有指定标签名的所有元素。

    node.getElementsByTagName("tagname");

返回的并不是一个数组只是元素的集合,可以用索引来拿访问,但是无法使用数组的方法.

### getElementsByClassName() 方法

如果您希望查找带有相同类名的所有 HTML 元素，请使用这个方法：

    document.getElementsByClassName("intro");

上面的例子返回包含 class="intro" 的所有元素的一个列表：

**注释：getElementsByClassName() 在 Internet Explorer 5,6,7,8 中无效。**

<h1 id="6">DOM 修改</h1>

修改 HTML = 改变元素、属性、样式和事件。

修改 HTML DOM 意味着许多不同的方面：

-   改变 HTML 内容
-   改变 CSS 样式
-   改变 HTML 属性
-   创建新的 HTML 元素
-   删除已有的 HTML 元素
-   改变事件（处理程序）

### 改变 HTML 输出流

`document.write()` 可用于直接向 HTML 输出流写内容

绝对不要在文档(DOM)加载完成之后使用 document.write()。这会覆盖该文档。






### 创建&改变 HTML 内容 - 更新

**1. innerHTML 属性**

获取元素内容的最简单方法是使用 innerHTML 属性。

可以修改一个DOM节点的文本内容

还可以直接通过HTML片段修改DOM节点内部的子树

```javascript
//<p id="intro">Hello World!</p>

var txt=document.getElementById("intro").innerHTML; //获取
document.write(txt);

/*
Hello World!
Hello World!
*/

------------------------------------------
//设置

// 获取<p id="p-id">...</p>
var p = document.getElementById('p-id');
// 设置文本为abc:
p.innerHTML = 'ABC'; // <p id="p-id">ABC</p>
// 设置HTML:
p.innerHTML = 'ABC <span style="color:red">RED</span> XYZ';
// <p>...</p>的内部结构已修改

```

用`innerHTML`时要注意，是否需要写入HTML。如果写入的字符串是通过网络拿到了，要注意对字符编码来避免XSS攻击。

**2. 另一种修改节点文本的方法(IE<9不支持)**

修改`innerText`或`textContent`属性，这样可以自动对字符串进行HTML编码，保证无法设置任何HTML标签:

```JavaScript
// 获取<p id="p-id">...</p>
var p = document.getElementById('p-id');
// 设置文本:
p.innerText = '<script>alert("Hi")</script>';
// HTML被自动编码，无法设置一个<script>节点:
// <p id="p-id">&lt;script&gt;alert("Hi")&lt;/script&gt;</p>

```
两者的区别在于读取属性时，`innerText`不返回隐藏元素的文本，而`textContent`返回所有文本。另外注意**IE<9不支持`textContent`**。

### 改变 HTML 属性

    document.getElementById(id).attribute=新属性值

```javascript
// <img id="image" src="smiley.gif">

 document.getElementById("image").src="landscape.jpg";
```


### 改变 HTML 样式(CSS) - 更新

    document.getElementById(id).style.property=新样式 

DOM节点的`style`属性对应所有的CSS，可以直接获取或设置。因为CSS允许`font-size`这样的名称，但它并非JavaScript有效的属性名，所以需要在JavaScript中改写为驼峰式命名`fontSize`：


```JavaScript
// 获取<p id="p-id">...</p>
var p = document.getElementById('p-id');
// 设置CSS:
p.style.color = '#ff0000';
p.style.fontSize = '20px';
p.style.paddingTop = '2em';
```

### 创建新的 HTML 元素 - 插入

**1. appendChild() - 将新元素作为父元素的最后一个子元素进行添加**

**2. insertBefore(newElement, referenceElement) - 子节点会插入到referenceElement之前**

如需向 HTML DOM 添加新元素，您首先必须创建该元素（元素节点），然后把它追加到已有的元素上。

```html
<div id="d1">
<p id="p1">This is a paragraph.</p>
<p id="p2">This is another paragraph.</p>
</div>

<script>
//创建了一个新的 <p> 元素
var para=document.createElement("p");   

//如需向 <p> 元素添加文本，您首先必须创建文本节点
var node=document.createTextNode("This is new.");

//然后您必须向 <p> 元素追加文本节点
para.appendChild(node);

//或者直接使用 para.innerText = "This is new";

var element=document.getElementById("d1");

//必须向已有元素追加这个新元素
element.appendChild(para);
</script>

/*
This is a paragraph.

This is another paragraph.

This is new.
*/
```

### 删除已有的 HTML 元素

如需删除 HTML 元素，您必须清楚该元素的父元素：

```html
<div id="div1">
    <p id="p1">This is a paragraph.</p>
    <p id="p2">This is another paragraph.</p>
</div>

<script>
var parent=document.getElementById("div1");
var child=document.getElementById("p1");
parent.removeChild(child);
</script>

//This is another paragraph.
```
**常用的解决方法：找到您需要删除的子元素，然后使用 `parentNode` 属性来查找其父元素**

```JavaScript
var child=document.getElementById("p1");
child.parentNode.removeChild(child);
```
当你遍历一个父节点的子节点并进行删除操作时，要注意，children属性是一个只读属性，并且它在子节点变化时会实时更新。

```html
<div id="parent">
    <p>First</p>
    <p>Second</p>
</div>
```
当我们用如下代码删除子节点时：
```JavaScript
var parent = document.getElementById('parent');
parent.removeChild(parent.children[0]);
parent.removeChild(parent.children[1]); // <-- 浏览器报错
```
浏览器报错：`parent.children[1]`不是一个有效的节点。
原因就在于,当`<p>First</p>`节点被删除后，`parent.children`的节点数量已经从2变为了1，索引[1]已经不存在了。

因此，删除多个节点时，要注意`children`属性时刻都在变化。



### 替换 HTML 元素 - replaceChild()

```html
<div id="div1">
    <p id="p1">This is a paragraph.</p>
    <p id="p2">This is another paragraph.</p>
</div>

<script>
var para=document.createElement("p");
var node=document.createTextNode("This is new.");
para.appendChild(node);

var parent=document.getElementById("div1");
var child=document.getElementById("p1");
parent.replaceChild(para,child);
</script>

/*
This is new.
This is another paragraph.
*/
```

<h1 id="7">DOM 事件</h1>

HTML DOM 允许 JavaScript 对 HTML 事件作出反应。。

HTML 事件的例子：

-   当用户点击鼠标时
-   当网页已加载时
-   当图片已加载时
-   当鼠标移动到元素上时
-   当输入字段被改变时
-   当 HTML 表单被提交时
-   当用户触发按键时
-   ......

**注意：事件通常与函数配合使用，当事件发生时函数才会执行。**

### onload 和 onunload 事件

当用户进入或离开页面时，会触发 onload 和 onunload 事件。

onload 事件可用于检查访客的浏览器类型和版本，以便基于这些信息来加载不同版本的网页。

onload 和 onUnload 事件也常被用来处理用户进入或离开页面时所建立的 cookies。例如，当某用户第一次进入页面时，你可以使用消息框来询问用户的姓名。姓名会保存在 cookie 中。当用户再次进入这个页面时，你可以使用另一个消息框来和这个用户打招呼："Welcome John Doe!"。

### onFocus, onBlur 和 onChange 事件

onFocus、onBlur 和 onChange 事件通常相互配合用来验证表单。

onchange 事件常用于输入字段的验证。

下面的例子展示了如何使用 onchange。当用户改变输入字段的内容时，将调用 upperCase() 函数。

### onmouseover 和 onmouseout 事件

onmouseover 和 onmouseout 事件可用于在鼠标指针移动到或离开元素时触发函数,创建“动态的”按钮.

### onmousedown、onmouseup 以及 onclick 事件

`onmousedown`、`onmouseup` 以及 `onclick` 事件是鼠标点击的全部过程。首先当某个鼠标按钮被点击时，触发 `onmousedown` 事件，然后，当鼠标按钮被松开时，会触发 `onmouseup` 事件，最后，当鼠标点击完成时，触发 `onclick` 事件。

<h3 id="7.1">DOM EventListener - addEventListener()</h3>

在用户点击按钮时触发监听事件：

    document.getElementById("myBtn").addEventListener("click", displayDate);

addEventListener() 方法用于向指定元素添加事件句柄。

addEventListener() 方法添加的事件句柄不会覆盖已存在的事件句柄。

你可以向一个元素添加多个事件句柄。

你可以向同个元素添加多个同类型的事件句柄，如：两个 "click" 事件。

你可以向任何 DOM 对象添加事件监听，不仅仅是 HTML 元素。如： window 对象。

addEventListener() 方法可以更简单的控制事件（冒泡与捕获）。

当你使用 addEventListener() 方法时, JavaScript 从 HTML 标记中分离开来，可读性更强， 在没有控制HTML标记时也可以添加事件监听。


你可以使用 `removeEventListener()` 方法来移除事件的监听。

    element.addEventListener(event, function, useCapture);

第一个参数是事件的类型 (如 "click" 或 "mousedown").

第二个参数是事件触发后调用的函数。

第三个参数是个布尔值用于描述事件是冒泡还是捕获。该参数是可选的。

**注意:不要使用 "on" 前缀。 例如，使用 "click" ,而不是使用 "onclick"。**


```javascript
//当用户点击元素时弹出 "Hello World!" :
--------------------------------------------
//<button id="myBtn">点我</button>
document.getElementById("myBtn").addEventListener("click", function(){
    alert("Hello World!");
});
```

```javascript
//你可以向同个元素添加不同类型的事件：
----------------------------------------------
//<button id="myBtn">点我</button>
//<p id="demo"></p>

var x = document.getElementById("myBtn");
x.addEventListener("mouseover", myFunction);
x.addEventListener("click", mySecondFunction);
x.addEventListener("mouseout", myThirdFunction);
function myFunction() {
    document.getElementById("demo").innerHTML += "Moused over!<br>"
}
function mySecondFunction() {
    document.getElementById("demo").innerHTML += "Clicked!<br>"
}
function myThirdFunction() {
    document.getElementById("demo").innerHTML += "Moused out!<br>"
}

```

事件传递有两种方式：冒泡与捕获。

事件传递定义了元素事件触发的顺序。 如果你将 \<p> 元素插入到 \<div> 元素中，用户点击 \<p> 元素, 哪个元素的 "click" 事件先被触发呢？

在 **冒泡** 中，内部元素的事件会先被触发，然后再触发外部元素，即： \<p> 元素的点击事件先触发，然后会触发\<div> 元素的点击事件。

在 **捕获** 中，外部元素的事件会先被触发，然后才会触发内部元素的事件，即： \<div> 元素的点击事件先触发 ，然后再触发 \<p> 元素的点击事件。

`addEventListener()` 方法可以指定 `"useCapture" `参数来设置传递类型：

    addEventListener(event, function, useCapture);

默认值为 false, 即冒泡传递，当值为 true 时, 事件使用捕获传递。

 `removeEventListener()` 方法移除由 `addEventListener()` 方法添加的事件句柄:

**注意： IE 8 及更早 IE 版本，Opera 7.0及其更早版本不支持 addEventListener() 和 removeEventListener() 方法。但是，对于这类浏览器版本可以使用 `detachEvent()` 方法来添加和移除事件句柄:**

    element.attachEvent(event, function);
    element.detachEvent(event, function);


#### 跨浏览器解决方法:

```JavaScript
var x = document.getElementById("myBtn");
if (x.addEventListener) {                    // 所有主流浏览器，除了 IE 8 及更早版本
    x.addEventListener("click", myFunction);
} else if (x.attachEvent) {                  // IE 8 及更早版本
    x.attachEvent("onclick", myFunction);
}
```



<h1 id="8">DOM 导航</h1>

通过 HTML DOM，您能够使用节点关系在节点树中导航。

### HTML DOM 节点列表

`getElementsByTagName()` 方法返回节点列表。节点列表是一个节点数组。

**注释：下标号从 0 开始。**

### HTML DOM 节点列表长度

length 属性定义节点列表中节点的数量。

您可以使用 length 属性来循环节点列表：

### 导航节点关系

您能够使用三个节点属性：`parentNode`、`firstChild` 以及 `lastChild` ，在文档结构中进行导航。

firstChild 属性可用于访问元素的文本：

元素和元素之间的空格也算文本.

```javascript
//<p id="intro">Hello World!</p>

x=document.getElementById("intro");
document.write(x.firstChild.nodeValue);

/*
Hello World!
Hello World! 
*/
-----------------------------------------------
//<p id="intro"><b>Hello World!</b></p>

x=document.getElementById("intro");
document.write(x.firstChild.innerHTML); 
//p元素firstChild是b不是文本所以要用innerHTML

/*
Hello World!
Hello World! 
*/
-------------------------------------------------
//<p id="intro"> <b>Hello World!</b></p>

x=document.getElementById("intro");
document.write(x.firstChild.nodeValue); 
//因为p元素firstChild是空格所以它的nodeValue是空

// Hello World!

```

### DOM 根节点

这里有两个特殊的属性，可以访问全部文档：

-   document.documentElement - 全部文档
-   document.body - 文档的主体

### childNodes 和 nodeValue

除了 `innerHTML` 属性，您也可以使用 `childNodes` 和 `nodeValue` 属性来获取元素的内容。

`childNodes` 元素节点,文本节点(换行,空格)都算的.可以用`children`代替.

```JavaScript
//<p id="intro">Hello World!</p>

var txt=document.getElementById("intro").childNodes[0].nodeValue;
document.write(txt);

/*
Hello World!
Hello World! 
*/
```

