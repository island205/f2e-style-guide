#前端开发编码规范

##编码规范

###JavaScript

####语言规范

#####变量

必须使用`var`关键字定义变量。

#####常量

使用大写字符，用下划线分隔，例如：`NAME_LIKE_THIS`；  
推荐使用这样的常量明明模式：`<常量类型>_<适用场景>_<具体作用>`，例如：  
    
	...javascript
    // 正则表达式_它用来 match 字符串_match email的
    var
        REGEX_MATCHER_EMAIL = /..../,
        STR_WHITESPACE = " ";    // fill，优先级，规范/建议，作用域的不同要求 -> 
        jay
	...

#####分号

推荐使用分号，但是不作检查。

#####嵌套函数

可以使用

#####块内函数声明

不能在一个块内声明一个函数。不能写成：

    ...javascript
    if (x) {
        function foo() {}
    }
    ...

如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量:

    ...javascript
    if (x) {
        var foo = function() {}
    }
    ...

###HTML
###CSS

##Code Review CheckList
###JavaScript
###HTML
###CSS
