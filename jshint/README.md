#Geting start with JSHint

> JSHint是一个优秀的JavaScript代码检查工具，使用它能够规范代码的编写，可以保持一个良好的代码风格。基于[前端开发规范](https://github.com/island205/codingguide/blob/master/README.md)，结合JSHint的可配置项，我们使用如下的规则对代码进行检查：

##配置

- [下载](https://raw.github.com/island205/codingguide/master/jshint/.jshintrc)或复制下面的内容到`.jshintrc`文件。

```json
{
    // evn
    "browser": true,
    //"devel": true,
    "jquery": true,
    "mootools": true,

    // global
    "globals": {
        "DP": false,
        "exports": false,
        "require": false,
        "module": false,
        "define": false,
        "seajs": false
    },
    // grammar
    "undef": true,
    "eqeqeq": true,
    "eqnull": true,
    "trailing": true,
    // "es5":true,
    "scripturl": true,
    "loopfunc": true,

    // name
    "camelcase": true,
    "newcap": true,

    // error
    "unused": true,

    // style
    "curly": true,
    "asi": true,
    "immed": true,
    "latedef": true,
    "noarg": true,
    "noempty": true,
    "quotmark": "single",
    "maxdepth": 20,
    "boss": true,
    "indent": 4
}
```

##Check List（规则说明）

<table>
    <tr>
        <th>规则</th>
        <th>说明</th>
    </tr>
    <tr>
        <td>`"browser":true`</td>
        <td>现代浏览器环境，不会对`document`、`navigator`等之类的浏览器内置全局变量产生警告，但不包括`console`、`alert`。</td>
    </tr>
    <tr>
        <td>`//"devel":true`</td>
        <td>该选项不建议开启，开启就是打开开发模式，即可以使用`console`、`alert`等的调试函数，但这些函数往往会在上线后造成问题。</td>
    </tr>
    <tr>
        <td>
        `"jquery":true, "mootools":true`
        </td>
        <td>不会对以上这两个库引入的全局变量产生警告。</td>
    </tr>
    <tr>
        <td>`"globals"`</td>
        <td>`DP`不解释；开启`CommonJS`标准，可以`require`等；`seajs`不解释；</td>
    </tr>
    <tr>
        <td>`"undef": true`</td>
        <td>不允许使用未定义的变量。</td>
    </tr>
    <tr>
        <td>`"eqeqeq": true`</td>
        <td>阻止使用`==`、`!=`。</td>
    </tr>
    <tr>
        <td>`"eqnull":true`</td>
        <td>可以仅且可以使用`== null`来检查一个变量是`null`或者`undefined`。</td>
    </tr>
    <tr>
        <td>`"trailing":true`</td>
        <td>不允许在行末出现多余的无效的空白字符。</td>
    </tr>
    <tr>
        <td>`"scripturl":true`</td>
        <td>允许在代码中使用`javascript:...`。</td>
    </tr>
    <tr>
        <td>`"loopfunc":true`</td>
        <td>允许在循环中出现函数定义。</td>
    </tr>
    <tr>
        <td>`"camelcase":true "newcap":true `</td>
        <td>变量使用驼峰，构造函数首字母大写，常量大写字母单词+`_`。</td>
    </tr>
    <tr>
        <td>`"unused":true`</td>
        <td>不允许出现定义但未使用的变量。</td>
    </tr>
    <tr>
        <td>`"curly":true`</td>
        <td>`if\for\function`等必须使用大括号。</td>
    </tr>
    <tr>
        <td>`"asi":true`</td>
        <td>可以不写分号。</td>
    </tr>
    <tr>
        <td>`"immed":true`</td>
        <td>不允许这样写`fun = function () { return function () {} }()`，要这样`fun = (function () {return function () {} })()`。前者容易混淆，不知道是一个函数定义，还是返回一个函数。</td>
    </tr>
    <tr>
        <td>`"latedef":true`</td>
        <td>变量、函数先定义，后使用。</td>
    </tr>
    <tr>
        <td>`"noarg":true`</td>
        <td>不允许使用`arguments.callee`和`arguments.caller`。</td>
    </tr>
    <tr>
        <td>`"noempty":true`</td>
        <td>不允许出现空的块，例如: `if (condition){ //do sth } else { }`。</td>
    </tr>
    <tr>
        <td>`"quotmark":"single"`</td>
        <td>字符串使用单引号`'`。</td>
    </tr>
    <tr>
        <td>`"maxdept":20`</td>
        <td>块嵌套层数不作限制，但如果超过20层，定为代码存在问题。</td>
    </tr>
    <tr>
        <td>`"boss":true`</td>
        <td>允许出现真假判断的地方出现赋值，例如：for (var i = 0, person; person = people[i]; i++) {}，但不推荐`if (a = 10) {}`。</td>
    </tr>
    <tr>
        <td>`"indent":4`</td>
        <td>使用4个空格缩进。</td>
    </tr>
</table>

##编辑器支持

###sublime

1. [Sublime Package Control](http://wbond.net/sublime_packages/package_control/installation)
2. 使用 package install 安装 JSHint 插件
3. 安装Node
4. 安装jshint，例如：`npm install -g jshint`
5. 添加配置文件（即`.jshintrc）到`pwd`或者其祖先级目录，比如说你的js源码在D:盘的某个文件夹中，那可以放在D:下面。（也可以放到用户目录下面）

可参考：

- https://github.com/jshint/jshint
- https://github.com/uipoet/sublime-jshint

###vim

再续……

