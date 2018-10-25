[window 对象](#1)

[navigator 对象](#2)

[screen 对象](#3)

[location 对象](#4)

[document 对象](#5)

[history 对象(不要使用)](#6)

<h1 id="1">window 对象</h1>

window对象不但充当全局作用域，而且表示浏览器窗口。

window对象有`innerWidth`和`innerHeight`属性，可以获取浏览器窗口的内部宽度和高度

内部宽高是指除去菜单栏、工具栏、边框等占位元素后，用于显示网页的净宽高

```javascript
console.log('window inner size: ' + window.innerWidth + ' x ' + window.innerHeight);

//window inner size: 1366 x 632
```

对应的，还有一个`outerWidth`和`outerHeight`属性，可以获取浏览器窗口的整个宽高。

<h1 id="2">navigator 对象</h1>

navigator对象表示浏览器的信息，最常用的属性包括：

-   navigator.appName：浏览器名称；
-   navigator.appVersion：浏览器版本；
-   navigator.language：浏览器设置的语言；
-   navigator.platform：操作系统类型；
-   navigator.userAgent：浏览器设定的User-Agent字符串。

```javascript
console.log('appName = ' + navigator.appName);
console.log('appVersion = ' + navigator.appVersion);
console.log('language = ' + navigator.language);
console.log('platform = ' + navigator.platform);
console.log('userAgent = ' + navigator.userAgent);

/*
appName = Netscape
appVersion = 5.0 (Windows)
language = zh-CN
platform = Win64
userAgent = Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:62.0) Gecko/20100101 Firefox/62.0
*/
```

请注意，navigator的信息可以很容易地被用户修改，所以JavaScript读取的值不一定是正确的。

很多初学者为了针对不同浏览器编写不同的代码，喜欢用if判断浏览器版本,但这样既可能判断不准确，也很难维护代码

正确的方法是充分利用JavaScript对不存在属性返回undefined的特性，直接用短路运算符||计算：

    var width = window.innerWidth || document.body.clientWidth;

<h1 id="3">screen 对象</h1>

screen对象表示屏幕的信息，常用的属性有：

-   screen.width：屏幕宽度，以像素为单位；
-   screen.height：屏幕高度，以像素为单位；
-   screen.colorDepth：返回颜色位数，如8、16、24。

```javascript
console.log('Screen size = ' + screen.width + ' x ' + screen.height);

//Screen size = 1366 x 768
```

<h1 id="4">location 对象</h1>

`location`对象表示当前页面的URL信息。例如，一个完整的URL：

    http://www.example.com:8080/path/index.html?a=1&b=2#TOP

可以用`location.href`获取。要获得URL各个部分的值，可以这么写：

```JavaScript
location.protocol; // 'http'
location.host; // 'www.example.com'
location.port; // '8080'
location.pathname; // '/path/index.html'
location.search; // '?a=1&b=2'
location.hash; // 'TOP'
```

要加载一个新页面，可以调用`location.assign()`。

如果要重新加载当前页面，调用`location.reload()`方法非常方便。

```JavaScript
if (confirm('重新加载当前页' + location.href + '?')) {
    location.reload();
} else {
    location.assign('/'); // 设置一个新的URL地址
}

//跳出确认框,点击确认就重新加载当前页面,点击取消就会调到新设置的页面
```

<h1 id="5">document 对象</h1>

`document`对象表示当前页面

由于HTML在浏览器中以DOM形式表示为树形结构，`document`对象就是整个DOM树的根节点

`document`的`title`属性是从HTML文档中的`<title>xxx</title>`读取的，但是可以动态改变：

```javascript
document.title = '努力学习JavaScript!';

//当前浏览器窗口的标题会改变
```

要查找DOM树的某个节点，需要从`document`对象开始查找。最常用的查找是根据ID和Tag Name。

我们先准备HTML数据：

```html
<dl id="drink-menu" style="border:solid 1px #ccc;padding:6px;">
    <dt>摩卡</dt>
    <dd>热摩卡咖啡</dd>
    <dt>酸奶</dt>
    <dd>北京老酸奶</dd>
    <dt>果汁</dt>
    <dd>鲜榨苹果汁</dd>
</dl>
```

用`document`对象提供的`getElementById()`和`getElementsByTagName()`可以按ID获得一个DOM节点和按Tag名称获得一组DOM节点：

```javascript
var menu = document.getElementById('drink-menu');
var drinks = document.getElementsByTagName('dt');
var i, s, menu, drinks;

menu = document.getElementById('drink-menu');
menu.tagName; // 'DL'

drinks = document.getElementsByTagName('dt');
s = '提供的饮料有:';
for (i=0; i<drinks.length; i++) {
    s = s + drinks[i].innerHTML + ',';
}
console.log(s);

//提供的饮料有:摩卡,酸奶,果汁,
```

`document`对象还有一个`cookie`属性，可以获取当前页面的Cookie。

Cookie是由服务器发送的key-value标示符

因为HTTP协议是无状态的，但是服务器要区分到底是哪个用户发过来的请求，就可以用Cookie来区分

当一个用户成功登录后，服务器发送一个Cookie给浏览器，例如`user=ABC123XYZ(加密的字符串)...`，此后，浏览器访问该网站时，会在请求头附上这个Cookie，服务器根据Cookie即可区分出用户。

Cookie还可以存储网站的一些设置，例如，页面显示的语言等等。

JavaScript可以通过`document.cookie`读取到当前页面的Cookie：

    document.cookie; // 'v=123; remember=true; prefer=zh'

由于JavaScript能读取到页面的Cookie，而用户的登录信息通常也存在Cookie中，这就造成了巨大的安全隐患，这是因为在HTML页面中引入第三方的JavaScript代码是允许的：


如果引入的第三方的JavaScript中存在恶意代码，则 网站1 将直接获取到 网站2 的用户登录信息。

为了解决这个问题，服务器在设置Cookie时可以使用`httpOnly`，设定了`httpOnly`的Cookie将不能被JavaScript读取

这个行为由浏览器实现，主流浏览器均支持`httpOnly`选项，IE从IE6 SP1开始支持。

为了确保安全，服务器端在设置Cookie时，应该始终坚持使用`httpOnly`。

<h1 id="6">history 对象(不要使用)</h1>

`history`对象保存了浏览器的历史记录，JavaScript可以调用`history`对象的`back()`或`forward ()`，相当于用户点击了浏览器的“后退”或“前进”按钮

这个对象属于历史遗留对象，对于现代Web页面来说，由于大量使用AJAX和页面交互，简单粗暴地调用`history.back()`可能会让用户感到非常愤怒。

任何情况，你都不应该使用`history`这个对象了。
