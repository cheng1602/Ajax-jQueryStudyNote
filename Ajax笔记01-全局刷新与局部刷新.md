# Ajax

- 全局刷新与局部刷新
  - 全局刷新：整个浏览器被新的数据覆盖，在网络中传输大量的数据，浏览器需要加载，渲染页面
  - 局部刷新：在浏览器的内部，发起请求，获取数据，改变页面中的部分内容。在其余的页面无需加载和渲染。网页中中数据传输量少，给用户的感觉好
  - Ajax是用来实现局部刷新的一种技术



- 异步请求对象

  *XMLHttpRequest*

  - 局部刷新使用的核心对象是异步对象，这个异步对象是存在浏览器内存中的，使用JavaScript语法创建和使用异步对象

  - 创建异步请求对象的语法

    `var xmlhttp = XMLHttpRequest();`

  - 回调

    当请求的状态变化时，异步对象会自动调用onreadstatechange事件对应的函数

  - 

- Ajax

   *Asynchronous JavaScript and XML* 异步的JavaScript和XML

  - Ajax是一种局部刷新的新方法（2003年左右），不是一种语言，主要包含JavaScript，DOM，CSS，XML等技术，核心是JavaScript和XML

  - JavaScript负责创建异步对象，发送请求，更新页面更新页面的DOM对象，Ajax请求需要服务器端的数据

  - XML是网络中传输的数据格式，现在主要被JSON替代

    

- Ajax异步实现步骤

  1. 创建异步对象

     `var xmlhttp = XMLHttpRequest();`

  2. onreadstatechange 事件

     - 给异步对象绑定事件获知请求对象的变化：

       当异步对象发起请求/获取数据都会触发这个事件

     - 这个事件需要指定一个函数，在函数中处理状态的变化

       `xmlhttp.onreadstatechange = function() {处理请求的状态变化}`

     - 异步对象的readyState属性

       表示异步对象请求状态的变化

       0：创建异步对象时 `XMLHttpRequest()`

       1：初始化异步请求对象 `xmlhttp.open()`

       2：发送请求 `xmlhttp.send()`

       3：从服务器端获取了数据（3是异步对象内部使用，获取了原始的数据）

       4：异步对象把接收的对象处理完成后（开发人员在4的时候处理数据，更新当前页面）

     - 异步对象的readyState属性

       表示网络请求的状况：200，404，500

       需要当status==200时，表示网络请求是成功的

       ```javascript
       xmlhttp.onreadstatechange = function() {
       	if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
       		//可以处理服务器端的数据，更新当前页面
       	}
       }
       ```

  3. 初始化异步请求对象

     - 异步的方法open()

       `xmlhttp.open("请求方式get|post","服务器端的访问地址",同步|异步请求（默认是true，异步请求）)`

       ```javascript
       xmlhttp.open("get","loginServlet?name=zs&pwd=123",true);
       ```

  4. 使用异步对象发送请求

     -  `xmlhttp.send()`

  5. 获取服务器端返回的数据

     - responseText属性

       ```javascript
       xmlhttp.onreadstatechange = function() {
       	if (xmlhttp.readyState == 4 && xmlhttp.status == 200) {
       		//获取服务器端返回的数据，更新当前页面
       		var data = xmlhttp.responseText;
       		document.getElementById('name').value = data;
       	}
       }
       ```




- 全局刷新练习

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>BMI计算</title>
  </head>
  <body>
  <center>
      <h1>全局刷新计算BMI</h1>
      <form action="two" method="get">
          姓名：<input type="text" name="n">
          体重：<input type="text" name="w">
          身高：<input type="text" name="h">
          <input type="submit" value="计算">
      </form>
  </center>
  
  </body>
  </html>
  ```

  ```java
  package com.example.controller;
  
  import javax.servlet.*;
  import javax.servlet.http.*;
  import java.io.IOException;
  
  public class TwoServlet extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //接收请求参数
          String sN = request.getParameter("n");
          String sH = request.getParameter("h");
          String sW = request.getParameter("w");
  
          //计算
          float h = Float.valueOf(sH);
          float w = Float.valueOf(sW);
          float bmi = w / (h * h);
  
          String msg = "";
          if (bmi <= 18.5){
              msg = "，较瘦。";
          }else if (bmi > 18.5 && bmi <=23.9){
              msg = "，正常。";
          }else if (bmi > 24){
              msg = "，较胖。";
          }
  
          //返回结果
          msg = "您好：" + sN + "，您的bmi值是，" + bmi + msg;
          request.setAttribute("msg",msg);
  
          //转发到新的页面
          request.getRequestDispatcher("/bmiresult.jsp").forward(request,response);
  
      }
  
  }
  ```

  ```html
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
  <head>
      <title>查询结果</title>
  </head>
  <body>
  <center>
      <h1>查询结果</h1>
      <h3>${msg}</h3>
  </center>
  
  </body>
  </html>
  ```

  ```java
  package com.example.controller;
  
  import javax.servlet.*;
  import javax.servlet.http.*;
  import java.io.IOException;
  import java.io.PrintWriter;
  
  public class TwoServlet extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //接收请求参数
          String sN = request.getParameter("n");
          String sH = request.getParameter("h");
          String sW = request.getParameter("w");
  
          //计算
          float h = Float.valueOf(sH);
          float w = Float.valueOf(sW);
          float bmi = w / (h * h);
  
          String msg = "";
          if (bmi <= 18.5){
              msg = "，较瘦。";
          }else if (bmi > 18.5 && bmi <=23.9){
              msg = "，正常。";
          }else if (bmi > 24){
              msg = "，较胖。";
          }
  
          //返回结果
          msg = "您好：" + sN + "，您的bmi值是，" + bmi + msg;
          request.setAttribute("msg",msg);
  
          //转发到新的页面
          //request.getRequestDispatcher("/bmiresult.jsp").forward(request,response);
  
          //使用HttpServletResponse输出数据
          response.setContentType("text/html;charset=utf-8");
          //获取PrintWriter
          PrintWriter pw = response.getWriter();
          //输出数据
          pw.println(msg);
          //清空缓存
          pw.flush();
          //关闭
          pw.close();
  
      }
  
  }
  ```