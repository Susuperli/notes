# 第八课 表格 

## 表格标记（块级）

### 基本语法

````html
<table>
    <tr>
        <td>内容</td>
    </tr>
        <tr>
        <td>内容</td>
    </tr>
        <tr>
        <td>内容</td>
    </tr>
</table>
````

#### \<table >中属性及其说明

- **border：增加边框，且默认为0，单位可设置像素。**
- **bordercolor：设定边框颜色。**
- bordercolorlight&bordercolordark：设置亮边或暗边颜色，仅IE支持。
- **width：表格宽度，可设置为像素宽度，也可以用百分号表示。**
- **height：表格高度，可设置为像素高度，但百分号表示意义不大。**
- **bgcolor：背景颜色。**
- **background：设置背景。**
- frame：边框样式。
- rules：设置内部边框样式。
- **cellspacing：设置单元格间距。**
- **cellpadding：设置单元格内边距（内容和边框的距离）。**
- **align：设置表格的水平对齐方式。**

#### \<tr>中属性及其说明（仅）

- align：单元格的水平对齐方式。
- valign：行内容的垂直对齐方式（top middle bottom）。
- **bgcolo**r：行的背景颜色。

#### \<td>中属性及其说明

- align:单元格内容的水平对齐。
- valign:垂直对齐。
- bgcolor：背景颜色。
- background：背景图片。
- **width&height:宽度和高度。**
- **rowspan：单元格跨行。**
- **colspan：单元格跨列。**

#### 补充说明

- 表格标题：\<caption>.....\</caption>,写在第一个\<tr>之前，在表格最上面且默认居中。
- 表头标记：\<th>,将第一行或是第一列的\<td>→\<th>,表格内的内容就会默认居中且加粗。

## 表格嵌套

 在\<td>中进行正常嵌套即可；嵌套的层次越多，网页加载的速度就越慢。







