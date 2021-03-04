# jQuery

- 过滤器：在定位了dom对象后，根据一些条件筛选dom对象

  过滤器是一个字符串，用于筛选dom对象

  过滤器不能单独使用，必须要和选择器一起使用

  - 语法

    1. 选择第一个DOM对象，保留数组中第一个DOM对象

       `$("选择器:first")`

    2. 选最最后一个DOM对象，保留数组中最后的DOM对象

       `$("选择器:last")`

    3. 选择数组中指定的DOM对象

       `$("选择器:eq(数组索引)")`

    4. 选择数组中小于指定索引的所有DOM对象

       `$("选择器:lt(数组索引)")`

    5. 选择数组中大于指定索引的所有DOM对象

       `$("选择器:gt(数组索引)")`



- 表单属性过滤器

  根据表单中dom对象的状态情况，定位dom对象

  - 启用状态：enabled

    选择可用的文本框`$(":text:enabled")`

  - 不可用状态：disabled

    选择不可用的文本框`$(":text:disabled")`

  - 选择状态：checked

    复选框选中的元素`$(":checkbox:checked")`

  - 选择指定下拉列表的被选中元素

    `选择器>option:selected`

  ```html
  <!DOCTYPE html>
  <html>
  	<head>
  		<meta charset="utf-8">
  		<title>表单选择过滤器</title>
  		<script type="text/javascript" src="js/jquery-3.6.0.js"></script>
  		<script type="text/javascript">
  			$(function() {
  				$("#btn1").click(function() {
  					//获取所有可以使用的text
  					var obj = $(":text:enabled");
  					//设置jquery数组所有dom对象的value值
  					obj.val("预设值");
  				})
  
  				$("#btn2").click(function() {
  					//获取选中的cheakbox
  					var obj = $(":checkbox:checked");
  					for (var i = 0; i < obj.length; i++) {
  						alert(obj[i].value);
  					}
  				})
  
  				$("#btn3").click(function() {
  					//获取select选中的值
  					var obj = $("select>option:selected");
  					alert(obj.val());
  				})
  			})
  		</script>
  	</head>
  	<body>
  		<center>
  			<input type="text" id="txt1" value="text-1" /><br />
  			<input type="text" id="txt2" value="text-2" disabled="true" /><br />
  			<input type="text" id="txt3" value="text-3" /><br />
  			<input type="text" id="txt4" value="text-4" disabled/ /><br />
  			<hr width="60%" />
  			<input type="checkbox" value="A" checked>A<br />
  			<input type="checkbox" value="B" />B<br />
  			<input type="checkbox" value="C" />C<br />
  			<hr width="60%" />
  			<select id="1234">
  				<option value="1">1</option>
  				<option value="2">2</option>
  				<option value="3">3</option>
  				<option value="4">4</option>
  			</select><br />
  			<hr width="60%" />
  			<input type="button" value="设置可用的text值" id="btn1" /><br />
  			<button id="btn2">显示选选中的复选框的值</button><br />
  			<button id="btn3">显示选选中的下拉列表框的值</button><br />
  		</center>
  	</body>
  </html>
  ```

  

- 事件

  - jQuery中给dom对象绑定事件

    `$(选择器).监听事件名称(事件的处理函数);`

    - $(选择器)：定位dom对象，dom对象可以有多个，这些dom对象都绑定事件了
    - 事件名称：就是js中事件句柄去掉on的部分（如：click）
    - 事件的处理函数：就是一个function，当事件发生事时，执行这个函数的内容

    

- 函数

  - val

    操作数组中DOM对象的value属性

    `$(选择器).val()`：无参数调用形式，读取数组中第一个DOM对象的value属性值

    `$(选择器).val(值)`：有参数形式调用，对数组中所有DOM对象的value属性值进行统一赋值

  - text

    操作数组中所有DOM对象的【文字显示内容属性】

    `$(选择器).text()`：读取数组中所有DOM对象的文字显示内容，拼接为一个字符串返回

    `$(选择器).text(值)`：有参数形式调用，统一赋值

  - attr

    对val，text之外的其他属性操作

    `$(选择器).attr("属性名")`：获取DOM数组第一个对象的属性值

    `$(选择器).attr("属性名","值")`：将数组中所有的DOM对象的属性设为新值

  - remove

    `$(选择器).remove()`：将数组中所有DOM对象及其子对象删除

  - empty

    `$(选择器).empty()`：将数组中所有DOM对象的子对象删除

  - append

    为数组中所有DOM对象添加子对象

    `$(选择器).append("<button>动态新增的按钮</button>")`

  - html

    设置或返回被选元素的内容（innerHTML）

    `$(选择器).html()`：无参数调用，获取DOM数组中第一个匹配元素的内容

    `$(选择器).html(值)`：有参数调用，用书设置DOM数组中所有元素的内容

    ```html
    <!DOCTYPE html>
    <html>
    	<head>
    		<meta charset="utf-8">
    		<title>函数</title>
    		<script type="text/javascript" src="js/jquery-3.6.0.js"></script>
    		<script type="text/javascript">
    			$(function() {
    				$("#btn1").click(function() {
    					//使用remove：删除父和子所有的DOM对象
    					$("select").remove();
    				})
    				$("#btn2").click(function() {
    					//使用empty：删除子DOM对象
    					$("select").empty();
    				})
    				$("#btn3").click(function() {
    					//使用append：增加DOM对象
    					$("#div-1").append("<button>动态新增的按钮</button>");
    				})
    				$("#btn4").click(function() {
    					//使用html函数：获取数组中第一个dom对象的文本值（innerHTML）
    					alert($("span").html());
    				})
    				$("#btn5").click(function() {
    					$("span").html("<button>动态新增的按钮</button>");
    				})
    			})
    		</script>
    	</head>
    	<body>
    		<center>
    			<select id="1234">
    				<option value="1">1</option>
    				<option value="2">2</option>
    				<option value="3">3</option>
    				<option value="4">4</option>
    			</select><br />
    			<select id="ABCD">
    				<option value="A">A</option>
    				<option value="B">B</option>
    				<option value="C">C</option>
    				<option value="D">D</option>
    			</select><br />
    			<hr width="60%" />
    			<span>span<b>标签1</b></span><br />
    			<span>span标签2</span>
    			<hr width="60%" />
    			<div id="div-1">~~div-1~~</div>
    			<button id="btn1">使用remove删除</button><br />
    			<button id="btn2">使用empty删除</button><br />
    			<button id="btn3">使用append增加DOM对象</button><br />
    			<button id="btn4">获取第一个DOM的文本值</button><br />
    			<button id="btn5">设置所有span标签的文本值</button><br />
    		</center>
    	</body>
    </html>
    ```

  - each

    each是对数组，JSON和DOM数组等的遍历，对每个元素调用一次函数

    - `$.each(要遍历的对象,function(index,element){处理程序})`

    - `jQuery对象.each(function(index,element){处理程序})`

      (index：数组下标；element：数组对象)

      ```html
      <!DOCTYPE html>
      <html>
      	<head>
      		<meta charset="utf-8">
      		<title>each函数</title>
      		<script type="text/javascript" src="js/jquery-3.6.0.js"></script>
      		<script type="text/javascript">
      			$(function() {
      				$("#btn1").click(function() {
      					//循环普通数组
      					var arr = ["abc", "bcd", "cde"];
      					$.each(arr, function(index, element) {
      						alert(index + "!" + element);
      					})
      				})
      				$("#btn2").click(function() {
      					//循环JSON
      					var json = {
      						"name": "jack",
      						"age": 20
      					}
      					$.each(json, function(index, element) {
      						alert("index:" + index + "/element:" + element);
      					})
      				})
      				$("#btn3").click(function() {
      					//循环DOM数组
      					var domArr = $(":text");
      					$.each(domArr, function(index, element) {
      						alert("index:" + index + "/element:" + element.value);
      					})
      
      				})
      				$("#btn4").click(function() {
      					//循环DOM数组
      					$(":text").each(function(index, element) {
      						alert("index:" + index + "/element:" + element.value);
      					});
      				})
      
      			})
      		</script>
      	</head>
      	<body>
      		<center>
      			<input type="text" value="abc" />
      			<input type="text" value="def" />
      			<input type="text" value="ghi" />
      			<hr width="60%" />
      			<button id="btn1">循环普通数组</button><br />
      			<button id="btn2">循环JSON</button><br />
      			<button id="btn3">循环DOM数组</button><br />
      			<button id="btn4">循环jquery对象</button><br />
      
      
      		</center>
      	</body>
      </html>
      
      ```

      

