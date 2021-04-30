# 第十讲 jQuery中基本方法

jQuery中工具函数的写法都是：$.函数名()

- $.trim(str)

  返回：string；

  说明：去掉字符串首尾空格

- $.each(obj,callback)

  说明：

  通用例遍方法，可用于例遍对象和数组。

  **不同于例遍 jQuery 对象的 $().each() 方法，此方法可用于例遍任何对象。**

  回调函数拥有两个参数：第一个为对象的成员或数组的索引，第二个为对应变量或内容。

  如果需要退出 each 循环可使回调函数返回 false，其它返回值将被忽略。

- $.grep( array, callback, [invert\] )

  **返回值: Array**

  **说明:**

  使用过滤函数过滤数组元素。

  此函数至少传递两个参数：待过滤数组和过滤函数。过滤函数必须返回 true 以保留元素或 false 以删除元素。

  ![jq10grep](D:\0-Link\naotes\picture\jq10grep.png)

  **讲解:**

  默认invert为false, 即过滤函数返回true为保留元素. 如果设置invert为true, 则过滤函数返回true为删除元素.

  ````js
  $.grep( [0,1,2], function(n,i){    //n是指数组值，i是指索引值
  return n > 0;
  });
  //results:[1,2]
  ````

- $.map( array, callback )

  **返回值:**Array

  **说明:**

  将一个数组中的元素转换到另一个数组中。

  作为参数的转换函数会为每个数组元素调用，而且会给这个转换函数传递一个表示被转换的元素作为参数。

  转换函数可以返回转换后的值、null（删除数组中的项目）或一个包含值的数组，并扩展至原始数组中。

  ![jq10map](D:\0-Link\naotes\picture\jq10map.png)

  ````js
  var arr = [ "a", "b", "c", "d", "e" ] ；
  $("div").text(arr.join(", "));
  arr = $.map(arr, function(n, i){ return (n.toUpperCase() + i); });
  $("p").text(arr.join(", "));
  arr = jQuery.map(arr, function (a) { return a + a; });
  alert(arr.join(", "));
  //alert  A0A0, B1B1, C2C2, D3D3, E4E4
  ````

- $.merge(arr1,arr2)

  将两个数组合成一个新的数组。
  
- 遍历数组

  ![JQ10](D:\0-Link\naotes\picture\JQ10.png)

- 

