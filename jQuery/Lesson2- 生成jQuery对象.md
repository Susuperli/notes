# 第二讲 生成jQuery对象

````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="../../jquery-3.5.1/jquery-3.5.1.min.js"></script>
</head>
<body>
    <ul>
        <li>1</li>
        <li>1</li>
        <li>1</li>
        <li>1</li>
    </ul>
</body>
<script>
    $(document).ready(function(){
        $("li").click(function(){
            $(this).css("background","#f00");
        })
    })
</script>
</html>
````

## 过滤选择器

### 基本过滤器

| [:first](https://www.runoob.com/jquery/sel-first.html) | $("p:first") | 第一个 <p> 元素                                              |
| ------------------------------------------------------ | ------------ | ------------------------------------------------------------ |
| :not                                                   | $("p:not")   | 除了他的元素                                                 |
| [:last](https://www.runoob.com/jquery/sel-last.html)   | $("p:last")  | 最后一个 <p> 元素                                            |
| [:even](https://www.runoob.com/jquery/sel-even.html)   | $("tr:even") | 所有偶数 <tr> 元素，索引值从 0 开始，第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。 |
| [:odd](https://www.runoob.com/jquery/sel-odd.html)     | $("tr:odd")  | 所有奇数 <tr> 元素，索引值从 0 开始，第一个元素是偶数 (0)，第二个元素是奇数 (1)，以此类推。 |

| [:eq(*index*)](https://www.runoob.com/jquery/sel-eq.html)    | $("ul li:eq(3)")       | 列表中的第四个元素（index 值从 0 开始） |
| ------------------------------------------------------------ | ---------------------- | --------------------------------------- |
| [:gt(*no*)](https://www.runoob.com/jquery/sel-gt.html)       | $("ul li:gt(3)")       | 列举 index 大于 3 的元素                |
| [:lt(*no*)](https://www.runoob.com/jquery/sel-lt.html)       | $("ul li:lt(3)")       | 列举 index 小于 3 的元素                |
| [:not(*selector*)](https://www.runoob.com/jquery/jq-sel-not.html) | $("input:not(:empty)") | 所有不为空的输入元素                    |

### 子元素过滤器

| [:first-child](https://www.runoob.com/jquery/jq-sel-firstchild.html) | $("p:first-child")         | 属于其父元素的第一个子元素的所有 <p> 元素                    |
| ------------------------------------------------------------ | -------------------------- | ------------------------------------------------------------ |
| [:first-of-type](https://www.runoob.com/jquery/sel-firstoftype.html) | $("p:first-of-type")       | 属于其父元素的第一个 <p> 元素的所有 <p> 元素                 |
| [:last-child](https://www.runoob.com/jquery/sel-lastchild.html) | $("p:last-child")          | 属于其父元素的最后一个子元素的所有 <p> 元素                  |
| [:last-of-type](https://www.runoob.com/jquery/sel-lastoftype.html) | $("p:last-of-type")        | 属于其父元素的最后一个 <p> 元素的所有 <p> 元素               |
| [:nth-child(*n*)](https://www.runoob.com/jquery/sel-nthchild.html) | $("p:nth-child(2)")        | 属于其父元素的第二个子元素的所有 <p> 元素                    |
| [:nth-last-child(*n*)](https://www.runoob.com/jquery/sel-nthlastchild.html) | $("p:nth-last-child(2)")   | 属于其父元素的第二个子元素的所有 <p> 元素，从最后一个子元素开始计数 |
| [:nth-of-type(*n*)](https://www.runoob.com/jquery/sel-nthoftype.html) | $("p:nth-of-type(2)")      | 属于其父元素的第二个 <p> 元素的所有 <p> 元素                 |
| [:nth-last-of-type(*n*)](https://www.runoob.com/jquery/sel-nthlastoftype.html) | $("p:nth-last-of-type(2)") | 属于其父元素的第二个 <p> 元素的所有 <p> 元素，从最后一个子元素开始计数 |
| [:only-child](https://www.runoob.com/jquery/sel-onlychild.html) | $("p:only-child")          | 属于其父元素的唯一子元素的所有 <p> 元素                      |
| [:only-of-type](https://www.runoob.com/jquery/sel-onlyoftype.html) | $("p:only-of-type")        | 属于其父元素的特定类型的唯一子元素的所有 <p> 元素            |

### 内容过滤器

| [:contains(*text*)](https://www.runoob.com/jquery/sel-contains.html) | $(":contains('Hello')") | 所有包含文本 "Hello" 的元素            |
| ------------------------------------------------------------ | ----------------------- | -------------------------------------- |
| [:has(*selector*)](https://www.runoob.com/jquery/sel-has.html) | $("div:has(p)")         | 所有包含有 <p> 元素在其内的 <div> 元素 |
| [:empty](https://www.runoob.com/jquery/jq-sel-empty.html)    | $(":empty")             | 所有空元素                             |
| [:parent](https://www.runoob.com/jquery/sel-parent.html)     | $(":parent")            | 匹配所有含有子元素或者文本的父元素。   |

### 可见性过滤器

| [:hidden](https://www.runoob.com/jquery/sel-hidden.html)   | $("p:hidden")      | 所有隐藏的 <p> 元素 |
| ---------------------------------------------------------- | ------------------ | ------------------- |
| [:visible](https://www.runoob.com/jquery/sel-visible.html) | $("table:visible") | 所有可见的表格      |

### 属性过滤器

| [[*attribute*\]](https://www.runoob.com/jquery/jq-sel-attribute.html) | $("[href]")                   | 所有带有 href 属性的元素                                     |
| ------------------------------------------------------------ | ----------------------------- | ------------------------------------------------------------ |
| [[*attribute*=*value*\]](https://www.runoob.com/jquery/sel-attribute-equal-value.html) | $("[href='default.htm']")     | 所有带有 href 属性且值等于 "default.htm" 的元素              |
| [[*attribute*!=*value*\]](https://www.runoob.com/jquery/sel-attribute-notequal-value.html) | $("[href!='default.htm']")    | 所有带有 href 属性且值不等于 "default.htm" 的元素            |
| [[*attribute*$=*value*\]](https://www.runoob.com/jquery/sel-attribute-end-value.html) | $("[href$='.jpg']")           | 所有带有 href 属性且值以 ".jpg" 结尾的元素                   |
| [[*attribute*\|=*value*\]](https://www.runoob.com/jquery/sel-attribute-prefix-value.html) | $("[title\|='Tomorrow']")     | 所有带有 title 属性且值等于 'Tomorrow' 或者以 'Tomorrow' 后跟连接符作为开头的字符串 |
| [[*attribute*^=*value*\]](https://www.runoob.com/jquery/sel-attribute-beginning-value.html) | $("[title^='Tom']")           | 所有带有 title 属性且值以 "Tom" 开头的元素                   |
| [[*attribute*~=*value*\]](https://www.runoob.com/jquery/sel-attribute-contains-value.html) | $("[title~='hello']")         | 所有带有 title 属性且值包含单词 "hello" 的元素               |
| [[*attribute**=*value*\]](https://www.runoob.com/jquery/sel-attribute-contains-string-value.html) | $("[title*='hello']")         | 所有带有 title 属性且值包含字符串 "hello" 的元素             |
| [[*name*=*value*\][*name2*=*value2*]](https://www.runoob.com/jquery/sel-multipleattribute-equal-value.html) | $( "input[id][name$='man']" ) | 带有 id 属性，并且 name 属性以 man 结尾的输入框              |

### 表单过滤器

| [:input](https://www.runoob.com/jquery/sel-input.html)       | $(":input")          | 所有 input 元素                                              |
| ------------------------------------------------------------ | -------------------- | ------------------------------------------------------------ |
| [:text](https://www.runoob.com/jquery/sel-input-text.html)   | $(":text")           | 所有带有 type="text" 的 input 元素                           |
| [:password](https://www.runoob.com/jquery/sel-input-password.html) | $(":password")       | 所有带有 type="password" 的 input 元素                       |
| [:radio](https://www.runoob.com/jquery/sel-input-radio.html) | $(":radio")          | 所有带有 type="radio" 的 input 元素                          |
| [:checkbox](https://www.runoob.com/jquery/sel-input-checkbox.html) | $(":checkbox")       | 所有带有 type="checkbox" 的 input 元素                       |
| [:submit](https://www.runoob.com/jquery/sel-input-submit.html) | $(":submit")         | 所有带有 type="submit" 的 input 元素                         |
| [:reset](https://www.runoob.com/jquery/sel-input-reset.html) | $(":reset")          | 所有带有 type="reset" 的 input 元素                          |
| [:button](https://www.runoob.com/jquery/sel-input-button.html) | $(":button")         | 所有带有 type="button" 的 input 元素                         |
| [:image](https://www.runoob.com/jquery/sel-input-image.html) | $(":image")          | 所有带有 type="image" 的 input 元素                          |
| [:file](https://www.runoob.com/jquery/sel-input-file.html)   | $(":file")           | 所有带有 type="file" 的 input 元素                           |
| [:enabled](https://www.runoob.com/jquery/sel-input-enabled.html) | $(":enabled")        | 所有启用的元素                                               |
| [:disabled](https://www.runoob.com/jquery/sel-input-disabled.html) | $(":disabled")       | 所有禁用的元素                                               |
| [:selected](https://www.runoob.com/jquery/sel-input-selected.html) | $(":selected")       | 所有选定的下拉列表元素                                       |
| [:checked](https://www.runoob.com/jquery/sel-input-checked.html) | $(":checked")        | 所有选中的复选框选项                                         |
| .selector                                                    | $(selector).selector | 在jQuery 1.7中已经不被赞成使用。返回传给jQuery()的原始选择器 |
| [:target](https://www.runoob.com/jquery/jq-sel-target.html)  | $( "p:target" )      | 选择器将选中ID和URI中一个格式化的标识符相匹配的<p>元素       |