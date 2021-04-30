# 第九讲 用css样式控制表格、表单

## 表格样式控制

border-collapse:separate（分开）|collapse（合并为单一表格），在table中设置。

margin:0 auto;表格居中。

text-align:center;文字居中。

## 表单样式

### 举例如下

````html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			*{
				margin: 0;
				padding: 0;
			}/*取消所有样式*/
			form{
				background-color: #ccc;
				width:400px;
				/*height: ;*/
				margin:40px auto 0 auto;/*整体居中*/
				padding: 15px 0;
			}
			.la{
				display: inline-block;
				width:80px;
				text-align: right;
				font-size: 14px;
				margin-right: 15px;
			}
			p{
				/*margin:15px 0;*/
			}
			.con{
				width:200px;
				height:20px;
				border: #000000 solid 1px;
				outline:none;/*去除输入框的样式*/
				padding-left: 5px;
				background:transparent;/*输入框和背景颜色相同*/
			}
			.las{
				margin-right: 20px;
				font-size: 12px;
			}/*使单选项距离拉开*/
			.las input{
				width:20px;
				height:20px;
				/*color:red;控制不了颜色*/
			}
			select{
				width: 100px;
				height: 20px;
				border: #000000 solid 1px;
			}
			textarea{
				width: 200px;
				height: 100px;
				padding-left: 5px ;
				padding-top: 5px;
				border: #000000 solid 1px;
				resize: none;/*禁止用户调节尺寸*/
			}
			.btn{
				text-align:center;
			}
			.btn input{
				width:80px;
				height: 25px;
				border:#000000 solid 1px;
				background-color: red;
				color:white;
			}
		</style>
	</head>
	<body>
		<form name="myform" action="#" method="post">
			<p><label class="la">用户名：</label><input type="text" name="username" class="con"/></p>
			<p><label class="la">密码：</label><input type="password" name="pwd" class="con"/></p>
			<p><label class="la">性别：</label>
			   <label class="las"><input type="radio" name="sex" value="man"/>男</label>
			   <label class="las"><input type="radio" name="sex" value="woman"/>女</label>
			</p>
			<p><label class="la">城市：</label>
			<select name="city">
				<option value="bj">北京</option>
				<option value="sh">上海</option>
				<option value="sz">深圳</option>
			</select>
			</p>
			<p><label class="la">介绍：</label>
			   <textarea>
				
			   </textarea>
			</p>
			<p class="btn">
				<input type="submit" value="注册"/>
			</p>
		</form>
	</body>
</html>

````

结果显示

![image-20201116114607253](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201116114607253.png)

## 补充

- outline
- resize
- 边界图片