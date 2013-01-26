#CSS

##语言

###类型选择符

- 若无必要，不要把元素名与`ID`或者`class`连在一起使用：

```css
/* Not recommended */
ul#example {}
div.error {}

/* Recommended */
#example {}
.error {}
```

###@import

- 禁止使用`@import`组织代码`CSS`代码，使用`LESS`等CSS预编译器除外。

###分号

- 每个属性声明后必须添加分号`;`[CSS语法](http://www.w3.org/TR/CSS21/syndata.html#q10)；

- 大括号之外不能写分号`;`。

###hack

- 尽量少用浏览器`hack`，可以考虑的一种方式：

```html
<!--[if lt IE 7 ]> <html class="ie6"> <![endif]-->
<!--[if IE 7 ]> <html class="ie7"> <![endif]-->
<!--[if IE 8 ]> <html class="ie8"> <![endif]-->
<!--[if IE 9 ]> <html class="ie9"> <![endif]-->
<!--[if (gt IE 9)|!(IE)]><!--> <html> <!--<![endif]-->
```

- `hack`样式需遵照一定的顺序。

###z-index

- 参照`z-index`规范。

###reset

- 使用通用的`reset`样式；

###清除浮动

- 原则上所有的浮动都需要做好清除浮动的工作，使用统一的清除浮动样式：

```csss
.clearfix:after {
    content: "020";
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

##风格

###格式

- 可用的两种`CSS`编写格式，在同一个文件中只能使用其中一种：

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

###命名

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

- 不建议将类命名为 `.class1`, `.box2`, `.class-one`，大多数情况下，这是偷懒的表现。事实上，几乎所有情况，我们都可以为他们取一个好名字。

###注释

- 模块注释，推荐使用下面这样的方式：

/*---------------- footer ----------------*/
...
/*---------------- /footer ----------------*/

###属性顺序

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

###class 和 ID

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

###属性

- 只要可能，尽量简写（高效且易于理解），注：全局样式不能使用简写，避免业务样式难于覆盖：

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

- 属性需要使用引号时使用单引号`"`，`URI`值无需使用单引号：

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

###无用样式

- 清除确定无用的样式。

###图片
    
- 切图时必须合理的压缩每张图片，提高页面加载速度，如果能用1像素的就切成1像素；

- 一般情况下，请保存为 `png-8` 格式，所有能保存为静态`gif`的图像，都应该保存为`png-8`格式；

- `png-24`与`jpg`都是一种压缩图像格式，但是与`jpg`不同，`png-24` 是无损压缩，因此不会降低图像的品质（比如jpg图像锐利边缘的噪点），这也是要求效果图使用`png-24`格式保存的原因；

- `jpg`作为一种有损压缩格式，在每次使用它压缩的时候，均会再次降低图像的品质。多次编辑同一个`jpg`图像，情况会变得越来越糟糕。所以一定要从设计师手中拿到无损格式的设计稿再进行工作。一般不应该为`jpg`格式，除非这个图像：色值远超过256色(鲜艳而华丽)，保存为索引颜色会出现明显的梯度变化（梯田），颜色抖动（点状渐变）；

- 一般`CSS`背景图不使用`jpg`格式的图像。

