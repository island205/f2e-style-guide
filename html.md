#HTML

##语言

###DOCTYPE

- 使用`HTML5`，即`<!DOCTYPE html>`，且必须出现在在`HTML`文档的最顶端。

###语义化

- 注意代码的语义化：

```html
<!-- Not recommended -->
<div onclick="goToRecommendations();">All recommendations</div>

<!-- Recommended -->
<a href="recommendations/">All recommendations</a>
```

###结构、表现与行为互相分离

- 禁止使用行内样式；

- 字体表现应该使用样式来实现，禁止使用`font`标签；

- `div`页面版式间距等均严格要求以`CSS`定义，不能使用`br`、`&nbsp;`等标记充当。

###alt

- 提供媒体文件（`img`等）的备用信息`alt`：

```html
<!-- Not recommended -->
<img src="spreadsheet.png">

<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

###type属性

- 可以省略`style`和`script`的`type`（HTML5已经把`text/css`和`text/javascript`作为默认值）：

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

###button标记

- 不推荐使用`<button></button>`标记；

- 要使用必须指明`button`的类型`type="button"`或者`type="submit"`。

###table

- 在合适的时候充分利用`<thead>`、`<tfoot>`、`<tbody>`和`<th>`这些与`table`相关的标记；

- 注意：`<tfoot>`放在`tbody`之前，以便在整个表格数据加载完之前先把表尾显示出来。

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

###iframe

- 尽量少使用`iframe`；

###Protocol

- 省略嵌入式资源的`Protocol`（建议）

```html
<!-- Not recommended --> 
<script src = "http://www.google.com/js/gweb/analytics/autotrack.js" > < /script> 
<!-- Recommended --> 
<script src="//www.google.com/js/gweb/analytics /autotrack.js"></script>
```

###Meta 规则

- 编码：`<meta charset="utf-8" />`，必须作为`head`标记的第一个子元素。

###HTML5

- 慎用HTML5中的新特性，可参考[caniuse.com](http://caniuse.com)。需要讨论，[html5shiv](https://github.com/aFarkas/html5shiv/blob/master/src/html5shiv.js)

- 业务中兼容HTML5，推荐使用HTML5特性。

###内联事件

- 禁止使用内联事件；

```html
<a onclick="return false" >a link</a>
```

###bool属性

- 推荐只写属性名
```html
/* Recommended */
<input type="text" name="bar" readony />
```

##风格

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
###缩进

- 缩进的最小单位是2个空格，不允许使用`tab`。


###大小写

- 必须采用小写。

###双引号

- 使用双引号`"`包裹属性值。


###标签闭合

```html
/* Recommended */
<div></div>

<input name="foo" type="submit" />
```
