# jQuery

jQuery是一款跨主流浏览器的JavaScript库，封装了JavaScript相关方法的调用，简化JavaScript对HTML DOM的操作

官网：https://jquery.com/

- 配置

  ```html
  <!DOCTYPE html>
  <html>
  	<head>
  		<meta charset="utf-8">
  		<title>开始</title>
  		<!-- 指定jQuery的库文件位置，使用相对路径，当前项目的js目录下的指定文件 -->
  		<script type="text/javascript" src="js/jquery-3.6.0.js"></script>
  		<script type="text/javascript">
  			/* 
  			1. $(document)，$是jQuery中的函数名称，document是函数的参数，将document对象变成jQuery函数库可以使用的对象
  			2. ready是jQuery中的函数，是准备的意思，当页面的dom对象加载成功后会执行ready函数的内容，相当于js中的onload事件
  			3. function()是自定义函数			
  			 */
  			//标准写法
  			$(document).ready(function(){
  				alert("jQuery!");
  			})
  			
  			// 简写写法
  			$(function(){
  				alert("e");
  			})
  		</script>
  	</head>
  	<body>
  	</body>
  </html>
  ```



- DOM对象与jQuery对象

  - DOM对象

    使用JavaScript的语法创建的对象，即js对象

    `var obj = document.getElementById("Text1");`

  - jQuery对象

    使用jQuery语法表示对象叫做jQuery对象。jQuery表示的对象都是数组

    `var jobj = $("#Text1");`

  - DOM对象与jQuery对象的相互转换

    - DOM对象转换为jQuery对象：`$(dom对象)`

      ```html
      <!DOCTYPE html>
      <html>
      	<head>
      		<meta charset="utf-8">
      		<title>DOM对象与jQuery对象的相互转换</title>
      		<script type="text/javascript" src="js/jquery-3.6.0.js"></script>
      		<script type="text/javascript">
      			function btnClick(){
      				// 获取dom对象
      				var obj = document.getElementById("btn");
      				// 使用dom的value属性，获取值的
      				alert("使用dom对象的属性："+obj.value);
      				// 把dom对象转换为jquery。使用jquery库中的函数
      				var jobj = $(obj);
      				//调用jquery中的函数，获取value的值
      				alert("使用jquery对象的属性："+jobj.val());
      			}
      		</script>
      	</head>
      	<body>
      		<input type="button" id="btn" value="提交" onclick="btnClick()" />
      	</body>
      </html>
      ```

    - jQuery对象转换为DOM对象：从数组中获取第一个对象，第一个对象就是dom对象使用[0]或者get[0]

      ```html
      <!DOCTYPE html>
      <html>
      	<head>
      		<meta charset="utf-8">
      		<title>DOM对象与jQuery对象的相互转换</title>
      		<script type="text/javascript" src="js/jquery-3.6.0.js"></script>
      		<script type="text/javascript">
      			function btnClick(){
      				// 使用jquery的语法，获取页面中的dom对象
      				var obj = $("#txt")[0];// 从数组中获取下标是0的dom对象
      				obj.value = obj.value * obj.value;
      				alert(obj.value);
      			}
      		</script>
      	</head>
      	<body>
      		<input type="button" value="计算平方" onclick="btnClick()" />
      		<input type="text" id="txt" value="请输入整数" />
      	</body>
      </html>
      ```



- 选择器

  选择器是一个字符串，用来定位dom对象，以此通过jquery的函数操作dom

  - 常用的选择器

    1. id选择器：`$("#dom对象的id值")`

       通过dom对象的id定位dom对象

    2. class选择器：`$(".class样式名")`

       class表示css中的样式，使用样式的名称定位dom对象

    3. 标签选择器：`$("标签名称")`

       使用标签名称定位dom对象

    4. 所有选择器：`$("*")`

    ```html
    <!DOCTYPE html>
    <html>
    	<head>
    		<meta charset="utf-8">
    		<title>选择器</title>
    		<style type="text/css">
    			div{
    				background-color: darkseagreen ;
    				width: 12.5rem;
    				height: 12.5rem;
    			}
    		</style>
    		<script type="text/javascript" src="js/jquery-3.6.0.js"></script>
    		<script type="text/javascript">
    			function fun1(){
    				//id选择器
    				var obj = $("#one");
    				//使用jquery中改变样式的函数
    				obj.css("background","beige")
    			}
    			function fun2(){
    				//class选择器
    				var obj = $(".two");
    				obj.css("background","beige");
    			}
    			function fun3(){
    				//标签选择器
    				var obj = $("div");//数组中有三个对象
    				//jquery的操作都是操作数组中的全部成员
    				//所以是给所有的div设置背景色
    				obj.css("background","aquamarine");
    			}
    			function fun4(){
    				//所有选择器
    				var obj = $("*");
    				obj.css("width","15rem");
    				obj.css("background","beige");
    			}
    			function fun5(){
    				//组合选择器
    				var obj = $("#one,span");
    				obj.css("width","20rem");
    				obj.css("background","red");
    			}
    		</script>
    	</head>
    	<body>
    		<div id="one">id-one-div</div>
    		<br />
    		<div class="two">class-two-div</div>
    		<br />
    		<div>div</div>
    		<br />
    		<span>span标签</span>
    		<br />
    		<input type="button" value="id选择器" onclick="fun1()" />
    		<input type="button" value="class选择器" onclick="fun2()" />
    		<input type="button" value="标签选择器" onclick="fun3()" />
    		<input type="button" value="所有选择器" onclick="fun4()" />
    		<input type="button" value="组合选择器" onclick="fun5()" />
    	</body>
    </html>
    ```

  - 表单选择器

    表单相关元素选择器是指文本框、单选框、复选框、下拉列表等元素的选择方式

    该方法无论是否邨彩表单<form>均可做出相应的选择。表单选择器是为了能够更加容易地操作表单，表单选择器是根据元素类型来定义的

    - 语法：`$(":type属性值")`

      例如：`$(":text")`

    ```html
    <!DOCTYPE html>
    <html>
    	<head>
    		<meta charset="utf-8">
    		<title>表单选择器</title>
    		<script type="text/javascript" src="js/jquery-3.6.0.js"></script>
    		<script type="text/javascript">
    			function readTest() {
    				//表单选择器
    				var obj = $(":text")[0];
    				alert(obj.value);
    				var obj2 = $(":text");
    				alert(obj2.val());
    
    			}
    
    			function readRadio() {
    				var obj = $(":radio"); //数组，目前有两个对象
    				//循环数组，数组中的成员是dom对象，可以dom的属性或者函数
    				for (var i = 0; i < obj.length; i++) {
    					//从数组值获取成员，使用下标的方式
    					var dom = obj[i];
    					//使用dom对象的属性，获取value值
    					alert(dom.value);
    				}
    			}
    
    			function readCheckbox() {
    				var obj = $(":checkbox");
    				for (var i = 0; i < obj.length; i++) {
    					//从数组值获取成员，使用下标的方式
    					var dom = obj[i];
    					//转换为jquery函数调用val()方法
    					var jobj = $(dom);
    					alert(jobj.val());
    				}
    			}
    		</script>
    	</head>
    	<body>
    		<center>
    			<input type="text" value="text" /><br />
    			<hr width="60%" />
    			<input type="radio" value="man" />man<br />
    			<input type="radio" value="wowan" />woman<br />
    			<hr width="60%" />
    			<input type="checkbox" value="a" />A<br />
    			<input type="checkbox" value="b" />B<br />
    			<input type="checkbox" value="c" />C<br />
    			<hr width="60%" />
    			<input type="button" value="读取text" onclick="readTest()" />
    			<input type="button" value="读取radio" onclick="readRadio()" />
    			<input type="button" value="读取checkbox" onclick="readCheckbox()" />
    		</center>
    	</body>
    </html>
    ```

    