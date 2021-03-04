# jQuery

- 事件

  - jQuery中给dom对象绑定事件

    `$(选择器).监听事件名称(事件的处理函数);`

    - $(选择器)：定位dom对象，dom对象可以有多个，这些dom对象都绑定事件了
    - 事件名称：就是js中事件句柄去掉on的部分（如：click）
    - 事件的处理函数：就是一个function，当事件发生事时，执行这个函数的内容

  - on事件绑定

    `$(选择器).on(事件名称,事件的处理函数);`



- AJAX

  1. `$.ajax()`：jquery中实现ajax的核心函数
  2. `$.post()`：使用post方式做ajax请求
  3. `$.get()`：使用get方式做ajax请求

  - `$.ajax()`参数是一个json的结构

    `$.ajax({json数组})`

    1. async：是一个boolean类型的值，默认是true，表示异步请求，可以省略async这个配置项

    2. contentType：一个字符串，表示从浏览器发送服务器的参数的类型，可以省略不写

    3. data：可以是字符串、数组、json，表示请求的参数和参数值，常用的是json格式的数据

    4. dataType：表示期望从服务器端返回的数据格式，可选的有：xml，html，text，json

       当我们使用`$.ajax()`发送请求时，会把dataType的值发送给服务器，那么服务器就可以返回你需要的数据格式

    5. error：一个function，表示当请求发生错误时，执行的函数

       `error:function(){发生错误时执行}`

    6. sucessr：一个function，请求成功后从服务端返回了数据，会执行success指定的函数

    7. url：请求的地址

    8. type：请求的方式，get或者post，不用区分大小写，默认是get方式

    ```javascript
    $(function (){
            $("#is").click(function (){
                //获取dom的value值
                var staffId = $("#id").val();
                alert(staffId);
                //发起ajax请求
                $.ajax({
                    url:"link",
                    data:{
                        "iid":staffId
                    },
                    dataType:"json",
                    success:function (resp){
                        alert(resp);
                        $("#ri").val(resp.id);
                        $("#rn").val(resp.name);
                        $("#rd").val(resp.did);
                        $("#rt").val(resp.date);
                    }
    
                })
    
            })
        })
    ```

    ```java
    import javax.servlet.http.*;
    import java.io.IOException;
    import java.io.PrintWriter;
    
    public class LinkServlet extends HttpServlet {
        @Override
    
        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    
            //默认值{}：表示json格式的数据
            String json = "{}";
    
            //处理get请求
            String sId = request.getParameter("iid");
            System.out.println("接收到:" + sId);
    
            String remsg = "未查询到结果。";
            //访问dao，查询数据库
            if( sId != null && sId.trim().length() > 0 ){
                JDBC j = new JDBC();
                Staff staff = j.staticSearch(sId);
                //需要使用jackson把Staff对象转换为json
                ObjectMapper om = new ObjectMapper();
                json = om.writeValueAsString(staff);
            }else{
                remsg = "请输入查询内容。";
            }
    
            //使用HttpServletResponse输出数据
            //指定服务器端（servlet）返回给浏览器的是json格式的数据
            response.setContentType("application/json;charset=utf-8");
            PrintWriter pw = response.getWriter();
            pw.println(json);//输出数据，付给ajax中responseText属性
            pw.flush();
            pw.close();
        }
    }
    ```

    

