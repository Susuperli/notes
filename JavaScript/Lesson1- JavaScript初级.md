#  第一讲 JavaScript初级

## JavaScript概述

### 在网站中的应用

* 网页中的特效，如，焦点图，二级菜单等。
* 表单嵌套。
* ajax。
* HTML5新增接口。

### js概念及其特点

- js是一种基于对象（object）和事件（event driven）驱动并具有安全性的脚本语言。

- 具有以下几个特点
  - 一种脚本语言。
  - 基于对象的语言。
  - 简单性。
  - 安全性。
  - 动态性。
  - 跨平台。

- JavaScript和Java的区别

  完全不同的两种语言。

- JScript和JavaScript。

  JScript是运行在IE游览器上的脚本语言，完全兼容JavaScript。

- EcmaScript是JavaScript的标准；

  JavaScript是ecmascript标准的实现。

## 嵌入方式

### 内嵌方式

````html 
<script type="text/javascript">
    JS代码
</script>
````

可以写在HTML的任何地方。

### 连接方式

首先将js代码保存成独立的js文件

````html
<script type="text/javascript" src="js.js"></script>
````

两个标记之间不能写任何东西。

### 注释方法

- 单行注释，//注释内容。
- 多行注释，/\*注释内容*/。

## JavaScript常用单词

1.	script脚本
2.	**variable** 变量 （JavaScript简写成 var 用来声明/创建变量）
3.	string 字符串
4.	boolean 布尔
5.	undefined 未定义
6.	null 空
7.	number 数字
8.	function 函数
9.	return 返回值
10.	if 如果
11.	else 否则
12.	switch 转换（编程语言中用于多选一结构）
13.	while 当….的时候
14.	do 做
15.	break 中断
16.	continue继续
17.	document 文档
18.	object 对象
19.	model模型
20.	**module**模块
21.	get获得
22.	element元素（也就是html标记）
23.	query 查询
24.	selector 选择器
25.	all全部
26.	parent 父
27.	children 儿子们
28.	node节点
29.	create创建
30.	**sibling** 其他兄弟
31.	next 下一个
32.	prev 上一个
33.	attribute 属性
34.	console 控制台
35.	log 日志（在JavaScript中，是在控制台打印表达式的意思）
36.	dir目录缩写（在JavaScript中，是在控制台打印对象的结构的意思）
37.	event事件
38.	array数组
39.	error错误
40.	throw 抛出
41.	new 新
42.	regular 规则
43.	expression 表达式 （JavaScript中简写为:regexp 正则表达式）
44.	infinity 无穷大
45.	call 调用
46.	caller 调用者
47.	callee 被调用者
48.	apply 应用
49.	this 这个（在JavaScript中代表当前环境对象）
50.	prototype 原型
51.	class类
52.	extends继承
53.	constructor 构造器
54.	super 超级
55.	try 监控
56.	catch 捕获
57.	finally 最终
58.	page页面
59.	offset 偏移量
60.	mouse 鼠标
61.	down 向下
62.	up 向上
63.	key 键
64.	focus焦点
65.	blur失去焦点
66.	click单击
67.	dblclick双击
68.	load装载
69.	unload卸载
70.	stop停止
71.	propagation 冒泡
72.	prevent 阻止
73.	default 默认
74.	true真
75.	false假
76.	ajax 阿贾克斯
77.	set 设置
78.	request请求
79.	content-type 内容类型
80.	application 应用程序
81.	encoded 已经编码的
82.	ready准备
83.	state状态（一般是枚举值）
84.	change改变
85.	status 状态（一般是状态变化）
86.	send发送
87.	data数据
88.	date日期
89.	time时间
90.	year年
91.	month月
92.	hour小时
93.	minute分
94.	second 秒
95.	interval 间隔
96.	timeout超时
97.	clear清除（JavaScript中用于清除时间间隔和超时器）
98.	scroll滚动
99.	scrollTo 滚动到
100.	scrollBy 滚动多少
101.	viewport 视口
102.	innerWidth 视口宽度
103.	insert 插入
104.	before前面
105.	after 后面
106.	append追加
107.	child儿子
108.	push 推（在JavaScript用于向数组尾部添加元素）
109.	pop 弹出（在JavaScript用于从数组尾部弹出元素）
110.	split将…分成若干部分（在JavaScript中，用于将字符串按照指定分隔符转换为数组）
111.	substring 字符串截取
112.	substr 字符串截取
113.	slice字符串截取
114.	splice 拼接（在Javascript中，用于插入、删除或替换数组的元素）
115.	lowercase 小写
116.	uppercase 大写
117.	index索引
118.	last最后
119.	compare比较
120.	match匹配
121.	replace 替换
122.	search搜索
123.	reverse反向
124.	shift移出
125.	unshift 移入
126.	sort排序
127.	floor 地板--底部
128.	ceil天花板—顶部
129.	add添加
130.	attach使附上
131.	argument实参
132.	global 全文的
133.	alert警告
134.	confirm 确定
135.	open打开
136.	window窗口
137.	prompt提示的内容
138.	history历史
139.	location定位
140.	back后退
141.	go去
142.	forward向前
143.	hash 锚点
144.	host主机
145.	hostname主机名
146.	port 端口
147.	protocol协议
148.	cookie小糕点
149.	response 响应
150.	network 网络