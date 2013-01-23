#JavaScript 编码规范


##语言规范

###变量

- 必须使用`var`关键字定义变量；
- 定义变量（或使用函数定义式）必须先定义后使用；推荐函数也先声明后使用。
- 不能在一个块内声明一个函数。不能写成：

```javascript
if (x) {
    function foo() {}
}
```
- 不允许出现全局变量，通常使用一个即时执行的函数解决：

```javascript
(function(root){
    var global
    //...
})(this)
```

- 如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量:

```javascript
if (x) {
    var foo = function() {}
}
```

###命名

- 使用大写字符，用下划线分隔，例如：`NAME_LIKE_THIS`；  
- 推荐使用这样的常量明明模式：`<常量类型>_<适用场景>_<具体作用>`，例如：  

```javascript
// 正则表达式_它用来 match 字符串_match email的
var
    REGEX_MATCHER_EMAIL = /```./,
    STR_WHITESPACE = " ";    // fill，优先级，规范/建议，作用域的不同要求 -> 
```

- 常见的命名方式：`functionNamesLikeThis`, `variableNamesLikeThis`, `ClassNamesLikeThis`, `EnumNamesLikeThis`, `methodNamesLikeThis`和`SYMBOLIC_CONSTANTS_LIKE_THIS`。
- 私有的属性、变量或者方法以“`_`”开头
- 文件的命名包括小写字母、`-`、`_`（不能包含其他字符，且`-`优于`_`），使用`.js`结尾。
- 不能使用拼音。

###推荐命名范式

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


###分号

- 推荐使用分号

###等值比较

- 推荐使用===和!==操作符；特别地，不要使用==来和"假"值做比较。

###异常

- 可以使用异常
- 可以使用自定义异常，但必须输出清晰的可读的异常信息

###标准特性

- 不允许使用非标准的特性
- 优先使用标准特性，最大化可移植性和兼容性，尽量使用标准方法。例如优先使用`string.charAt(3)`，而不使用`string[3]`
- 慎用`JavaScript 1.5`以上的新特性，以[1.5](http://en.wikipedia.org/wiki/JavaScript#Versions)为准，example；`trim`。

###内置对象原型

- 不允许修改内置对象的原型
- 框架开发中如何能够完美实现现有标准，可修改内置对象原型，可参考[MDC](https://developer.mozilla.org/en/docs/JavaScript)。

###eval

- 只用于解析序列化字符串，处理XHR等从服务端请求得到的返回值

###caller & callee

- 禁止使用`arguments.caller`和`arguments.callee`。

###with

- 禁止使用

###this

- 仅在对象构造器、方法和毕包中使用`this`

###for-in迭代

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

###关联数组

- 不推荐把数组当作Hash使用，即不推荐使用字符串key存取值。

```javascript
var
list = []

// 不推荐
list['travel'] = function (travler) {
    var
    i
    for (i = 0; i < this.length; i++) {
        travler(this[i])
    }
}

// 推荐
function travelArray(list, traveler) {
    var
    i
    for (i = 0; i < list.length; i++) {
        traveler(list[i])
    }
}
```

###多行字符串

- 不允许像下面这边书写多行字符串，非`ECMAScript`规范：

```javascript
var myString = 'A rather long string of English text, an error message \
                actually that just keeps going and going -- an error \
                message to make the Energizer bunny blush (right through \
                those Schwarzenegger shades)! Where was I? Oh yes, \
                you\'ve got an error and all the extraneous whitespace is \
                just gravy.  Have a nice day.';
```


###Ajax

- 使用Ajax，必须指明是`HTTP`使用`GET`，`POST`，如果使用`GET`，必须指明是否需要`cache`。
- 注意cache的情况


###JSON与JavaScript对象字面量

- JSON中的对象属性必须加上双引号`"`；
- JavaScript对象字面量除去以下这两种情况（必须使用引号），不允许使用关键字/保留字作为属性名：
    - css({'float': 'left'})
    - createElement('div', {'class': 'container'})

###console & debugger

- 在提交的代码中不允许出现`console`、`debugger`。

###控制元素的显隐藏

- 使用`hide`样式来控制元素的显隐

###dataset

- 不推荐自定义属性，推荐使用`dataset`

###template type

- 如果所使用的模板引擎有惯例，则沿用惯例，否则使用`text/dp-tpl`

###引号

- 字符串推荐使用单引号`'`



##编码风格

###空格

- 关键字后面跟`(`(左圆括号)时应该用一个空格隔开。
- 方法名和方法的`(`(左圆括号)之间不要有空格。这利于区分关键字和方法调用。
- 所有的二元操作符，除了`.`(圆点)、`(`(左圆括号)和`[`(左中括号)，都应该使用一个空格来和操作数隔开。
- 一元操作符和操作数之间不应该使用空格隔开，除了操作符是一个单词时，如`typeof`。
- `for`语句控制部分的每个`;`(分号)应该在后面跟一个空格。
- 每个`,`(逗号)后面应该跟一个空格。


###缩进

- 缩进的最小单位是4个空格，尽量不要使用tab，因为tab目前的标准还不统一，不同编辑器的空格数是不同的。如果你习惯了tab，请将你的编辑器tab键的默认设置设为4个空格。

###注释

- 行内注释使用`//`，且注释号与注释内容之间必须包含一个空格，例如 `// this is a comment.`。
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

###常见的块代码（`if/else/for/while/try`）格式（注意括号、大括号和换行）必须书写大括号

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
###不推荐使用前置逗号

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
###模块

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
###构造器

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

###var

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

###文件

- JavaScript程序应该作为一个 .js文件存储和发布，文件编码为`utf-8`。
- JavaScript代码不应该嵌入在HTML文件里，除非这些代码是一个单独的会话特有的或者是需要有后台开发工程师进行控制的。HTML里的JavaScript代码大大增加了页面的大小，并且很难通过缓存和压缩来缓解，同时也难以通过前端来维护。
- JavaScript文件应该在`body`里越靠后的位置越好，最好是放在最后面。这减少了由于加载`script`而导致的其它页面组件的延迟。


