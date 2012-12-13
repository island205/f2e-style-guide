#前端开发编码规范

##说明
> 本规范对前端开发过程中的一些基本原则和惯用法进行了归纳和总结，分为`javascript`、`HTML`、`CSS`三大块，每又分为`语言规范`与`编码风格`；
> 本规范不涉及具体的业务架构规范，其他规范会在其他文档中给出；
> 规范并非标准，一般情况下请严格遵守，特殊情况下灵活运用；
> 规范有一个从无到有，越来越好，越来越适用的过程；随着时间的推移和技术变迁，有些规范有错误，有些会过时，还有更多的新规范加进来；本规范也会一直处在不断革新的过程之中，有什么不对和不足的地方欢迎大家指出，一个大家达成共识，乐于使用的规范才是好的规范。

##目录
1. [目录](#目录)
2. [编码规范](#编码规范) 
    1. [JavaScript](#javascript)
        - [语言规范](#语言规范)
        - [编码风格](#编码风格)
    2. [HTML](#html)
    3. [CSS](#css)
    4. [图片](#图片)
  
3. [Code Review Check List](#code-review-checklist)  
    1. [JavaScript List](#javascript-list)
    2. [HTML List](#html-list)
    3. [CSS List](#css-list)
    4. [图片 List](#图片-list)  
4. [参考](#参考)
5. [贡献者](贡献者)

##编码规范

###JavaScript

####语言规范

#####变量

- 必须使用`var`关键字定义变量。

#####常量

- 使用大写字符，用下划线分隔，例如：`NAME_LIKE_THIS`；  
- 推荐使用这样的常量明明模式：`<常量类型>_<适用场景>_<具体作用>`，例如：  

```javascript
// 正则表达式_它用来 match 字符串_match email的
var
    REGEX_MATCHER_EMAIL = /```./,
    STR_WHITESPACE = " ";    // fill，优先级，规范/建议，作用域的不同要求 -> 
```

#####分号

- 推荐使用分号，但是不作检查。

#####等值比较

- 始终使用===和!==操作符会更好。==和!=操作符会做类型强制转换。特别是，不要使用==来和"假"值做比较。

#####Latedef

- 定义变量（或使用函数定义式）必须先定义后使用；推荐函数申明也先声明后使用。


#####嵌套函数（块）

- 可以使用
- 块嵌套不能超过20层

#####块内函数声明

- 不能在一个块内声明一个函数。不能写成：

```javascript
if (x) {
    function foo() {}
}
```

- 如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量:

```javascript
if (x) {
    var foo = function() {}
}
```
#####异常

- 可以使用异常

#####自定义异常

- 可以使用自定义异常，输出清晰的可读的异常信息

#####标准特性

- 优先使用标准特性，最大化可移植性和兼容性，尽量使用标准方法。例如优先使用`string.charAt(3)`，而不使用`string[3]`

#####没有必要分装基本类型

- 完全没必要对基础类型进行分装，有可能会引起问题：

```javascript
var x = new Boolean(false);
if (x) {
    alert('hi'); // Shows 'hi'.
}
```
- 可以用于类型转换：

```javascript
var x = Boolean(0);
if (x) {
    alert('hi'); // This will never be alerted.
}
typeof Boolean(0) == 'boolean';
typeof new Boolean(0) == 'object';
```
#####闭包

- 可以使用，但要小心。下面的代码会造成内存泄漏：

```javascript
function foo(element, a, b) {
    element.onclick = function () { /* uses a and b */
    };
}
```

- 尽管闭包没有使用`element`，但还是保留了对`element`、`a`、`b`的引用，同时`element`也引用了闭包，这就造成了循环引用，造成内存泄漏。可以将代码重构为：

```javascript
function foo(element, a, b) {
    element.onclick = bar(a, b);
}

function bar(a, b) {
    return function () { /* uses a and b */
    }
}
```

#####全局变量

- 不允许出现无必要的全局变量，通常使用一个即时执行的函数解决：

```javascript
(function(root){
    var global
    //...
})(this)
```
- 适当使用必要的全局变量作为命名空间组织代码

#####eval

- 只用于解析序列化字符串，处理XHR等从服务端请求得到的返回值

#####caller & callee

- 禁止使用`arguments.caller`和`arguments.callee`。

#####with

- 禁止使用

#####this

- 仅在对象构造器、方法和毕包中使用`this`

#####for-in迭代

- 只使用`for-in`来迭代`Object`，即所谓的`Map`或者`Hash`。用来迭代`Array`有时候会有问题：

```javascript
function printArray(arr) {
    for (var key in arr) {
        console.log(arr[key]);
    }
}

printArray([0, 1, 2, 3]); // This works.

var a = new Array(10);
printArray(a); // This is wrong.

a = document.getElementsByTagName('*');
printArray(a); // This is wrong.

a = [0, 1, 2, 3];
a.buhu = 'wine';
printArray(a); // This is wrong again.

a = new Array;
a[3] = 3;
printArray(a); // This is wrong again.
```
- 使用普通的`for`循环来迭代数组：

```javascript
function printArray(arr) {
    var l = arr.length;
    for (var i = 0; i < l; i++) {
        print(arr[i]);
    }
}
```

#####关联数组

- 不允许使用关联数组，即不要把`Array`当作`Object`来使用。

#####多行字符串

- 不允许像下面这边书写多行字符串，非`ECMAScript`规范：

```javascript
var myString = 'A rather long string of English text, an error message \
                actually that just keeps going and going -- an error \
                message to make the Energizer bunny blush (right through \
                those Schwarzenegger shades)! Where was I? Oh yes, \
                you\'ve got an error and all the extraneous whitespace is \
                just gravy.  Have a nice day.';
```

#####内置对象原型

- 不允许修改（除非参考[MDC](https://developer.mozilla.org/en/docs/JavaScript)）。

#####IE条件注释

- 不允许使用如下的写法：

```javascript
var f = function () {
    /*@cc_on if (@_jscript) { return 2* @*/ 3; /*@ } @*/
};
```

#####Ajax

- 使用Ajax，必须指明是`HTTP`使用`GET`，`POST`，如果使用`GET`，必须指明是否需要`cache`。
- 注意cache的情况


#####JSON与JavaScript对象字面量

- JSON中的对象属性必须加上引号`"`。

#####console & debugger

- 在提交的代码中不允许出现`console`、`debugger`。
- 开发时期的解决方案

#####JavaScript 1.5

- 慎用`JavaScript 1.5`以上的新特性，以[1.5](http://en.wikipedia.org/wiki/JavaScript#Versions)为准，example；`trim`。


#####控制元素的显隐藏

- 使用`hide`样式来控制元素的显隐

#####dataset

- 不推荐自定义属性，推荐使用`dataset`

#####template type

- 如果所使用的模板引擎有惯例，则沿用惯例，否则使用`text/template`

#####引号

- 字符串定义时推荐使用单引号`'`，关键字、保留字使用引号括起来

####编码风格

#####命名

- 常见的命名方式：`functionNamesLikeThis`, `variableNamesLikeThis`, `ClassNamesLikeThis`, `EnumNamesLikeThis`, `methodNamesLikeThis`和`SYMBOLIC_CONSTANTS_LIKE_THIS`。
- 私有的属性、变量或者方法以“`_`”开头
- 文件的命名包括小写字母、`-`、`_`（不能包含其他字符，且`-`优于`_`），使用`.js`结尾。
- 不能使用拼音。

#####推荐命名范式

- `dom`选择器调用的返回值以`$`开头，这是`jQuery`常用的方式：`$body = jQuery(document.body)`;
- `boolean`定义：比起`bEmpty`，更推荐使用`isEmpty`,`canExit`,`hasNext`这样的命名方法。推荐使用`is`、`can`、`has`这样的前缀作为这类变量的前缀。
- 函数或者方法推荐使用`动宾`或`动`结构，例如：

```javascript
function getBooks() {
    //...
}
//or

var books = {
    get: function(){
        //...
    }
}
```
- 比起`arrBooks`，更推荐使用`bookList`，比起`objStates`，更推荐使用`stateMap`。
- 推荐的一些回调函数（或对象）的范式：`wordHandler`、`changeListener`、`getBookCallback`、`onLoad`。也可以使用其他能够表达功能的命名方式 

#####字符串

- 单引号`'`优于双引号`"`（包含HTML的字符串）。

#####空格

- 关键字后面跟`(`(左圆括号)时应该用一个空格隔开。
- 方法名和方法的`(`(左圆括号)之间不要有空格。这利于区分关键字和方法调用。
- 所有的二元操作符，除了`.`(圆点)、`(`(左圆括号)和`[`(左中括号)，都应该使用一个空格来和操作数隔开。
- 一元操作符和操作数之间不应该使用空格隔开，除了操作符是一个单词时，如`typeof`。
- `for`语句控制部分的每个`;`(分号)应该在后面跟一个空格。
- 每个`,`(逗号)后面应该跟一个空格。


#####缩进

- 缩进的最小单位是4个空格，尽量不要使用tab，因为tab目前的标准还不统一，不同编辑器的空格数是不同的。如果你习惯了tab，请将你的编辑器tab键的默认设置设为4个空格。

#####注释

- 行内注释使用`//`，且注释号与注释内容之间一个空格，例如 `// this is a comment.`。
- 推荐使用两种注释方式，在同一个项目中只能使用其中一种：

1. [backbone](https://github.com/documentcloud/backbone/blob/master/backbone.js)所采用的`markdown`形式，可以使用 [docco](https://github.com/jashkenas/docco)生成文档:
  
```javascript
//     Backbone.js 0.9.2

//     (c) 2010-2012 Jeremy Ashkenas, DocumentCloud Inc.
//     Backbone may be freely distributed under the MIT license.
//     For all details and documentation:
//     http://backbonejs.org

// A module that can be mixed in to *any object* in order to provide it with
// custom events. You may bind with `on` or remove with `off` callback functions
// to an event; `trigger`-ing an event fires all callbacks in succession.
//
//     var object = {};
//     _.extend(object, Backbone.Events);
//     object.on('expand', function(){ alert('expanded'); });
//     object.trigger('expand');
//
var Events = Backbone.Events = {

  // Bind one or more space separated events, `events`, to a `callback`
  // function. Passing `"all"` will bind the callback to all events fired.
  on: function(events, callback, context) {
    if (_.isObject(events)) {
      for (key in events) {
        this.on(key, events[key], callback);
      }
      return this;
    }

    var calls, event, list;
    if (!callback) return this;

    events = events.split(eventSplitter);
    calls = this._callbacks || (this._callbacks = {});

    while (event = events.shift()) {
      list = calls[event] || (calls[event] = []);
      list.push(callback, context);
    }

    return this;
  }
}
```

2. [JSDoc](http://code.google.com/p/jsdoc-toolkit/)这种与`JavaDoc`类似的方式，例如：  

```javascript
// Copyright 2009 Google Inc. All Rights Reserved.

/**
 * @fileoverview Description of file, its uses and information
 * about its dependencies.
 * @author user@google.com (Firstname Lastname)
 */

/**
 * Class making something fun and easy.
 * @param {string} arg1 An argument that makes this more interesting.
 * @param {Array.<number>} arg2 List of numbers to be processed.
 * @constructor
 * @extends {goog.Disposable}
 */
project.MyClass = function(arg1, arg2) {
  // ...
};
goog.inherits(project.MyClass, goog.Disposable);

/**
 * Converts text to some completely different text.
 * @param {string} arg1 An argument that makes this more interesting.
 * @return {string} Some return value.
 */
project.MyClass.prototype.someMethod = function(arg1) {
  // ...
};

/**
 * Operates on an instance of MyClass and returns something.
 * @param {project.MyClass} obj Instance of MyClass which leads to a long
 *     comment that needs to be wrapped to two lines.
 * @return {boolean} Whether something occured.
 */
function PR_someMethod(obj) {
  // ...
}
```

#####代码风格

- 常见的块代码（`if/else/for/while/try`）格式（注意括号、大括号和换行）必须书写大括号

```javascript
//推荐的风格，有助于可读性
if (condition) {
    // 语句
}

while (condition) {
    // 语句
}

for (var i = 0; i < 100; i++) {
    // 语句
}

//更好的做法
var i,
	length = 100;

for (i = 0; i < length; i++) {
    // 语句
}

// 或者...

var i = 0,
    length = 100;

for (; i < length; i++) {
    // 语句
}

var prop;

for (prop in object) {
    // 语句
}

//不推荐下面这样的写法
if(condition) doSomething();

while(condition) iterating++;

for(var i = 0; i < 100; i++) someIterativeFn();


```
- 不推荐使用前置逗号

```javascript
//推荐
var hoo = {
    bar: "bar",
    foo: "foo",
    memo: "memo"
}

//不推荐
var hoo = {
    bar: "bar"
  	,foo: "foo"
  	,memo: "memo"
}
```
- 模块

```javascript
// 一个实用的模块
(function (global) {
    var Module = (function () {

        var data = "secret";

        return {
            // 这是一个布尔值
            bool: true,
            // 一个字符串
            string: "a string",
            // 一个数组
            array: [1, 2, 3, 4],
            // 一个对象
            object: {
                lang: "en-Us"
            },
            getData: function () {
                // 得到 `data` 的值
                return data;
            },
            setData: function (value) {
                // 返回赋值过的 `data` 的值
                return (data = value);
            }
        };
    })();

    // 其他一些将会出现在这里

    // 把你的模块变成全局对象
    global.Module = Module;

})(this);
```
- 构造器

```javascript
// 一个实用的构造器
(function (global) {

    function Ctor(foo) {

        this.foo = foo;

        return this;
    }

    Ctor.prototype.getFoo = function () {
        return this.foo;
    };

    Ctor.prototype.setFoo = function (val) {
        return (this.foo = val);
    };

    // 不使用 `new` 来调用构建函数，你可能会这样做：
    var ctor = function (foo) {
            return new Ctor(foo);
        };

    // 把我们的构建函数变成全局对象
    global.ctor = ctor;

})(this);
```

#####var

- 推荐在同一个地方定义多个变量，写一个`var`，合理分组：

```javascript
var build = Base._build,

    builtClass = build._ctor(main, cfg),
    buildCfg = build._cfg(main, cfg, extensions),

    _mixCust = build._mixCust,
    dynamic = builtClass._yuibuild.dynamic,

    i, l, extClass, extProto,
    initializer,
    destructor;
```

#####文件

- JavaScript程序应该作为一个 .js文件存储和发布，文件编码为`utf-8`。
- JavaScript代码不应该嵌入在HTML文件里，除非这些代码是一个单独的会话特有的或者是需要有后台开发工程师进行控制的。HTML里的JavaScript代码大大增加了页面的大小，并且很难通过缓存和压缩来缓解，同时也难以通过前端来维护。
- JavaScript文件应该在`body`里越靠后的位置越好，最好是放在最后面。这减少了由于加载`script`而导致的其它页面组件的延迟。


###HTML

####语言规范

#####DOCTYPE

- 使用`HTML5`，即`<!DOCTYPE html>`，且必须出现在在`HTML`文档的最顶端。

#####语义化

- 编写语义化的代码：

```html
<!-- Not recommended -->
<div onclick="goToRecommendations();">All recommendations</div>

<!-- Recommended -->
<a href="recommendations/">All recommendations</a>
```

#####结构、表现和行为分离

- 禁止使用行内样式
- 字体表现应该使用样式来实现，禁止使用`font`标签
- `div`页面版式间距等均严格要求以`CSS`定义

#####alt

- 提供媒体文件（`img`等）的替代`alt`：

```html
<!-- Not recommended -->
<img src="spreadsheet.png">

<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

#####type属性

- 可以省略`style`和`script`的`type`（HTML5已经把`text/css`和`text/javascript`作为默认值）。

```html
<!-- Not recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css" type="text/css">

<!-- Recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css">
<!-- Not recommended -->

<script src="//www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>

<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
```

#####button标记

- 不推荐使用`<button></button>`标记，要使用必须标明`button`的类型`type="button"`或者`type="submit"`。

#####table

- 在合适的时候充分利用`<thead>`、`<tfoot>`、`<tbody>`和`<th>`这些与`table`相关的标记，注意：`<tfoot>`放在`tbody`之前，以便在整个表格数据加载完之前先把表尾显示出来。

```html
<table summary="This is a chart of invoices for 2011.">
    <thead>
        <tr>
            <th scope="col">Table header 1</th>
            <th scope="col">Table header 2</th>
        </tr>
    </thead>
    <tfoot>
        <tr>
            <td>Table footer 1</td>
            <td>Table footer 2</td>
        </tr>
    </tfoot>
    <tbody>
        <tr>
            <td>Table data 1</td>
            <td>Table data 2</td>
        </tr>
    </tbody>
</table>
```

#####iframe

- 尽量少使用`iframe`

#####Protocol

- 省略嵌入式资源的`Protocol`（建议）

```html
<!-- Not recommended --> 
<script src = "http://www.google.com/js/gweb/analytics/autotrack.js" > < /script> 
<!-- Recommended --> 
<script src="//www.google.com/js/gweb/analytics /autotrack.js"></script>
```

#####Meta 规则

- 编码：`<meta charset="utf-8" />`，写在`title`之前。

#####HTML5

- 慎用HTML5中的新特性，可参考[caniuse.com](http://caniuse.com)。需要讨论，[html5shiv](https://github.com/aFarkas/html5shiv/blob/master/src/html5shiv.js)

- 业务中兼容HTML5，推荐使用HTML5特性。

#####内联事件

- 禁止使用内联事件

```html
<a onclick="return false" >a link</a>
```

####编码风格

#####格式化

- `block`、`list`、`table`元素都新起一行，缩进每一个子元素，例如：

```html
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>

<ul>
  <li>Moe </li>
  <li>Larry </li>
  <li>Curly </li>
</ul>

<table>
  <thead>
    <tr>
      <th scope="col">Income </th>
      <th scope="col">Taxes </th>
  <tbody>
    <tr>
      <td>$ 5.00</tr>
      <td>$ 4.50</tr>
</table>
```
#####缩进

- 缩进的最小单位是4个空格，尽量不要使用tab，因为tab目前的标准还不统一，不同编辑器的空格数是不同的。如果你习惯了tab，请将你的编辑器tab键的默认设置设为4个空格。


#####大小写

- 必须采用小写。

#####双引号

- 使用双引号`"`包裹属性值。


#####标签闭合

```html
/* Recommended */
<div></div>

<input name="foo" type="submit" />
```

#####bool属性

- 推荐只写属性名
```html
/* Recommended */
<input type="text" name="bar" readony />
```

###CSS

####语言规范

#####类型选择符

- 若无必要，不要把元素名与ID或者class连在一起使用：

```css
/* Not recommended */
ul#example {}
div.error {}

/* Recommended */
#example {}
.error {}
```

#####@import

- 禁止使用`@import`组织代码，使用`LESS`等CSS预编译器除外。

#####分号

- 每个属性声明后必须添加分号`;`[CSS语法](http://www.w3.org/TR/CSS21/syndata.html#q10)。
- 大括号之外不能写分号`;`；

#####CSS3

- 慎用CSS3的动画`transition`（chrome闪烁）


#####hack

- 尽量少用浏览器`hack`，可以考虑的一种方式：

```html
<!--[if lt IE 7 ]> <html class="ie6"> <![endif]-->
<!--[if IE 7 ]> <html class="ie7"> <![endif]-->
<!--[if IE 8 ]> <html class="ie8"> <![endif]-->
<!--[if IE 9 ]> <html class="ie9"> <![endif]-->
<!--[if (gt IE 9)|!(IE)]><!--> <html> <!--<![endif]-->
```

#####z-index

- z-index规范


#####reset

- 使用通用的reset

#####清除浮动

- 原则上所有的浮动都需要做好清除浮动的工作，使用同一的清除浮动样式：

```csss
.clearfix:after {
    content: " ";
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
}

/* 针对 Internet Explorer */
.clearfix {
    zoom: 1;
}
```

#####&nbsp;

- 禁止使用`&nbsp;`处理定位

####编码风格

#####代码风格

```css
// This is a good example!
.styleguide-format {
  border: 1px solid #0f0;
  color: #000;
  background: rgba(0,0,0,0.5);
}

//in a line
.styleguide-format{border: 1px solid #0f0;color: #000;background: rgba(0,0,0,0.5);}
```

#####命名

- 小写字母，使用短横线`-`链接单词：

```css
/* Not recommended: does not separate the words “demo” and “image” */
.demoimage {}

/* Not recommended: uses underscore instead of hyphen */
.error_status {}
/* Recommended */
#video-id {}
.ads-sample {}
```

- 不建议将类命名为 `.class1`, `.box2`, `.class-one`，大多数情况下，这是偷懒的表现。事实上，几乎所有情况，我们都可以为他们取一个好名字

#####注释

- 模块注释，推荐使用下面这样的方式：

/*---------------- footer ----------------*/
...
/*---------------- /footer ----------------*/

- 针对浏览器特殊处理的hack的注释：


#####属性顺序

- 推荐按照一定的顺序书写css。

```css
display || visibility
list-style : list-style-type || list-style-position || list-style-image
position
top || right || bottom || left
z-index
clear
float
 
width
max-width || min-width
height
max-height || min-height
overflow || clip
margin : margin-top || margin-right || margin-bottom || margin-left
padding : padding-top || padding-right || padding-bottom || padding-left
outline : outline-color || outline-style || outline-width
border
background : background-color || background-image || background-repeat || background-attachment || background-position
 
color
font : font-style || font-variant || font-weight || font-size || line-height || font-family
font : caption | icon | menu | message-box | small-caption | status-bar
text-overflow
text-align
text-indent
line-height
white-space
vertical-align
cursor
```

#####class 和 ID

- 说明元素的功能或者作用；

```css
/* Not recommended: meaningless */
#yee-1901 {}

/* Not recommended: presentational */
.button-green {}
.clear {}
/* Recommended: specific */
#gallery {}
#login {}
.video {}

/* Recommended: generic */
.aux {}
.alt {}
```
- 在能够表达清楚功能或者作用的前提下，名称越短越好：

```css
/* Not recommended */
#navigation {}
.atr {}

/* Recommended */
#nav {}
.author {}
```

#####属性

- 只要可能，尽量简写（高效且易于理解）：

```css
/* Not recommended */
border-top-style: none;
font-family: palatino, georgia, serif;
font-size: 100%;
line-height: 1.6;
padding-bottom: 2em;
padding-left: 1em;
padding-right: 1em;
padding-top: 0;

/* Recommended */
border-top: 0;
font: 100%/1.6 palatino, georgia, serif;
padding: 0 1em 2em;
```

- 值为"0"时，可以不指定单位（除非有必要）：

```css
margin: 0;
padding: 0;
```

- 值在-1到1之间时，可以省去0：

```css
font-size: .8em;
```

- 可以的话，请使用3位的十六进制：

```css
/* Not recommended */
color: #eebbcc;

/* Recommended */
color: #ebc;
```

- 属性需要使用引号时使用单引号`'`，`URI`值无需使用单引号：

```css
/* Not recommended */
@import url("//www.google.com/css/maia.css");

html {
  font-family: "open sans", arial, sans-serif;
}

/* Recommended */
@import url(//www.google.com/css/maia.css);

html {
  font-family: 'open sans', arial, sans-serif;
}
```

#####无用样式

- 清除无用样式（重要页面、奇妙的bug）

###图片
    
- 切图时必须合理的压缩每张图片，提高页面加载速度，如果能用1像素的就切成1像素
- 一般情况下，请保存为 `png-8` 格式，所有能保存为静态gif的图像，都应该保存为 png-8 格式
- png-24与jpg都是一种压缩图像格式，但是与jpg不同，`png-24` 是无损压缩，因此不会降低图像的品质（比如jpg图像锐利边缘的噪点），这也是要求效果图使用`png-24`格式保存的原因。
- jpg就不多说了。jpg作为一种有损压缩格式，在每次使用它压缩的时候，均会再次降低图像的品质。多次编辑同一个jpg图像，情况会变得越来越糟糕。所以一定要从设计师手中拿到无损格式的设计稿再进行工作。一般不应该为JPG格式，除非这个图像：色值远超过256色(鲜艳而华丽)，保存为索引颜色会出现明显的梯度变化（梯田），颜色抖动（点状渐变）
- 一般css背景图不使用 jpg 格式的图像


##Code Review CheckList

###JavaScript List
<table>
    <tr>
        <td>内容</td>
        <td>分数</td>
    </tr>
    <tr>
        <td>正确的缩进，最小缩进单位为4个空格</td>
        <td style="color:red">-1</td>
    </tr>
    <tr>
        <td>所有条件区域必须用花括号括起来</td>
        <td style="color:red">-2</td>
    </tr>
    <tr>
        <td>方法、变量都使用驼峰命名，类使用大驼峰(Pascal)命名</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>按库中的js模板书写js</td>
        <td style="color:green">+10</td>
    </tr>
    <tr>
        <td>无侵入式js，tracelog除外，有特例名。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>使用命名空间或闭包，禁止出现不必要的全局变量。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>方法、变量都使用驼峰命名，类使用大驼峰(Pascal)命名。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>变量声明应放在function的最上面，避免使用未声明的变量。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>常量名全部大写，单词分隔使用下划线。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>Bolean类型变量必须以is/has等判断词开头，str开头的必须是字符串，arr开头的必须是数组，num开头的必须是数字，obj开头的必须是对象。</td>
        <td style="color:red">-2</td>
    </tr>
    <tr>
        <td>获取和配置参数的函数必须以get set开头。</td>
        <td style="color:red">-2</td>
    </tr>
    <tr>
        <td>私有变量和方法如果不在闭包中，则以下划线开头。</td>
        <td style="color:red">+5</td>
    </tr>
    <tr>
        <td>关键字和保留字不能作为变量名。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>3个条件及以上的条件语句用switch代替`if else`。</td>
        <td style="color:red">-2</td>
    </tr>
    <tr>
        <td>使用{}代替new Object()；使用[]代替new Array()。</td>
        <td style="color:red">-2</td>
    </tr>
    <tr>
        <td>合理使用===和!==操作符。</td>
        <td style="color:red">-3</td>
    </tr>
    <tr>
        <td>不允许使用eval。</td>
        <td style="color:red">-3</td>
    </tr>
    <tr>
        <td>使用选择器时，能确定tagName的，必须加上tagName，例如".className"须写成"tagName.className"，"[attribute=xxx]"须写成"tagName[attribute=xxx]"。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>尽量少的重绘和重排，当需要给元素设置样式时，超过2个及2个以上时，采用className处理。</td>
        <td style="color:red">-3</td>
    </tr>
    <tr>
        <td>页面第三方广告（js引入的）必须采用无堵塞的方案接入。</td>
        <td style="color:red">-3</td>
    </tr>
    <tr>
        <td>防止重复提交（form、ajax）。</td>
        <td style="color:red">-3</td>
    </tr>
    <tr>
        <td>form验证需加在onsubmit上。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>一般情况下，DOMReady之前不能进行DOM操作。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>onerror事件必须消除onerror事件。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>使用".data()"读写自定义属性时需要转化成驼峰形式。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>不出现将造成线上bug的潜在js错误。此项为累计扣分，出现一次即扣相应分值，两次则扣两次，依此类推。但凡出现一次，均不予发布。</td>
        <td style="color:red">-5</td>
    </tr>
</table>

###HTML List

<table>
    <tr>
        <th>内容</th>
        <th>分数</th>
    </tr>
    <tr>
        <td>必须存在文档类型声明，新页面统一使用HTML5 DTD，且必须出现在HTML文档的最前面。</td>
        <td style="color:red">-10</td>
    </tr>
    <tr>
        <td>head部份格式正确，包含字符集meta和title。</td>
        <td style="color:red">-10</td>
    </tr>
    <tr>
        <td>外链CSS置于head里。</td>
        v<td style="color:red">-5</td>
    </tr>
    <tr>
        <td>不通过@import在页面上引入CSS。</td>
        v<td style="color:red">-5</td>
    </tr>
    <tr>
        <td>外链产品线级js置于head，页面级js置于页底。</td>
        v<td style="color:red">-5</td>
    </tr>
    <tr>
        <td>标签全部小写，包含属性，且自定义属性单词分隔用中横线。</td>
        v<td style="color:red">-3</td>
    </tr>
    <tr>
        <td>id、class名称全部小写，单词分隔使用中横线。</td>
        v<td style="color:red">-3</td>
    </tr>
    <tr>
        <td>属性值使用双引号。</td>
        v<td style="color:red">-3</td>
    </tr>
    <tr>
        <td>标签必须闭合，嵌套正确。</td>
        v<td style="color:red">-5</td>
    </tr>
    <tr>
        <td>行内标签不得包含块级标签。</td>
        v<td style="color:red">-5</td>
    </tr>
    <tr>
        <td>h类标签层次分明，依次递减。</td>
        v<td style="color:red">-5</td>
    </tr>
    <tr>
        <td>a标签加上title属性，除非作为功能点的a标签。</td>
        v<td style="color:red">-2</td>
    </tr>
    <tr>
        <td>img标签加上alt属性。</td>
        v<td style="color:red">-2</td>
    </tr>
    <tr>
        <td>text、radio、checkbox、textarea、select必须加name属性。</td>
        <td style="color:red">-10</td>
    </tr>
    <tr>
        <td>所有按钮必须用button（button/submit/reset）。</td>
        <td style="color:red">-5</td>
    </tr>
</table>

###CSS List

<table>
    <tr>
        <th>内容</th>
        <th>分数</th>
    </tr>
    <tr>
        <td>页面级别样式不使用id。</td>
        <td style="color:red">-3</td>
    </tr>
    <tr>
        <td>页面级别样式不能全局定义标签样式。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>不能定义内嵌样式style。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>CSS级联深度不能超过4层。</td>
        <td style="color:red">-2</td>
    </tr>
    <tr>
        <td>合理使用hack。</td>
        <td style="color:red">-3</td>
    </tr>
    <tr>
        <td>禁止使用星号（*）选择符，含选择符中带*号的hack。</td>
        <td style="color:red">-10</td>
    </tr>
    <tr>
        <td>禁止重写reset中定义的a标签的hover色。</td>
        <td style="color:red">-5</td>
    </tr>
    <tr>
        <td>禁止使用CSS表达式，fixed例外。</td>
        <td style="color:red">-5</td>
    </tr>
</table>

##参考

- [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
- [Google HTML/CSS Style Guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml)
- [github styleguide](https://github.com/styleguide)
- [书写具备一致风格、通俗易懂 JavaScript 的原则](https://github.com/rwldrn/idiomatic.js/tree/master/translations/zh_CN)

##贡献者
