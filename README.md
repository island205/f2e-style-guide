#前端开发编码规范

##目录
1. [目录](#目录)
2. [编码规范](#编码规范) 
    1. [JavaScript](#javascript)
        - [语言规范](#语言规范)
        - [编码风格](#编码风格)
    2. [HTML](#html)
    3. [CSS](#css)
  
3. [Code Review Check List](#code-review-checklist)  
    1. [JavaScript](#javascript)
    2. [HTML](#html)
    3. [CSS](#css)  
4. [参考](#参考)

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

#####嵌套函数

- 可以使用

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
#####eval

- 只用于解析序列化字符串，处理XHR等从服务端请求得到的返回值

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

- 不允许修改。

#####IE条件注释

- 不允许使用如下的写法：

```javascript
var f = function () {
    /*@cc_on if (@_jscript) { return 2* @*/ 3; /*@ } @*/
};
```

####编码风格

#####命名

- 常见的命名方式：`functionNamesLikeThis`, `variableNamesLikeThis`, `ClassNamesLikeThis`, `EnumNamesLikeThis`, `methodNamesLikeThis`和`SYMBOLIC_CONSTANTS_LIKE_THIS`。
- 私有的属性、变量或者方法以“`_`”开头
- 文件的命名包括小写字母、`-`、`_`（不能包含其他字符，且`-`优于`_`），使用`.js`结尾。

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

- [backbone](https://github.com/documentcloud/backbone/blob/master/backbone.js) [docco](https://github.com/jashkenas/docco)
- [JSDoc](http://code.google.com/p/jsdoc-toolkit/)
- [YUIDoc](http://yui.github.com/yuidoc/syntax/index.html)
- .....

#####代码风格

- 常见的块代码（`if/else/for/while/try`）格式（注意括号、大括号和换行）

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

#####文件

- JavaScript程序应该作为一个 .js文件存储和发布，文件编码为`utf-8`。
- JavaScript代码不应该嵌入在HTML文件里，除非这些代码是一个单独的会话特有的或者是需要有后台开发工程师进行控制的。HTML里的JavaScript代码大大增加了页面的大小，并且很难通过缓存和压缩来缓解，同时也难以通过前端来维护。
- JavaScript文件应该在`body`里越靠后的位置越好，最好是放在最后面。这减少了由于加载`script`而导致的其它页面组件的延迟。


###HTML

###CSS

##Code Review CheckList

###JavaScript

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

</table>

###HTML
###CSS

##参考
