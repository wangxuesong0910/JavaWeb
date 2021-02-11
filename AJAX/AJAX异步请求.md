# AJAX异步请求

> AJAX 即“**A***synchronous* **J***avascript* ***A****nd* **X***ML*”（异步 JavaScript 和 XML），是指一种创建交互式网页应用的网页开发技术

* ajax 是一种浏览器通过 js 异步发起请求，局部更新页面的技术。
* Ajax 请求的局部更新，浏览器地址栏不会发生变化,局部更新不会舍弃原来页面的内容

## 原生AJAX请求的示例

```java
   //servlet内容示例
   protected void ajaxServletRequest(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        System.out.println("接收到ajax异步请求");

        Gson gson = new Gson();

        Person person = new Person(1, "wxs");

        String s = gson.toJson(person);

        response.getWriter().write(s);
    }
```

```html
<html>
	<head>
		<meta http-equiv="pragma" content="no-cache" />
		<meta http-equiv="cache-control" content="no-cache" />
		<meta http-equiv="Expires" content="0" />
		<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
		<title>Insert title here</title>
		<script type="text/javascript">
			function ajaxRequest() {
// 				1、我们首先要创建XMLHttpRequest
				var xmlHttpRequest = new XMLHttpRequest();

// 				2、调用open方法设置请求参数
				xmlHttpRequest.open("GET","http://localhost:8080/12_JSON/ajaxServlet?action=ajaxServletRequest",true);

// 				4、在send方法前绑定onreadystatechange事件，处理请求完成后的操作。
				xmlHttpRequest.onreadystatechange = function(){
					if (xmlHttpRequest.readyState == 4 && xmlHttpRequest.status == 200){
						var jsonObj = JSON.parse(xmlHttpRequest.responseText);

						// 把响应的数据显示在页面上
						document.getElementById("div01").innerHTML = "编号：" + jsonObj.id + " , 姓名：" + jsonObj.name;
					}
				}

// 				3、调用send方法发送请求
				xmlHttpRequest.send();

			}
		</script>
	</head>
	<body>	
		<button onclick="ajaxRequest()">ajax request</button>
		<div id="div01">
		</div>
	</body>
</html>
```

## jQuery 中的AJAX请求

* $.ajax 方法
  * url  表示请求的地址
  * type  表示请求的类型GET或POST请求
  * data  表示发送给服务器的数据
    * 格式有两种：
      * 一：name=value&name=value
      * 二：{key：value}
  * success  请求成功，响应的回调函数
  * dataType  响应的数据类型(常用的数据类型有：text  表示纯文本，xml  表示xml数据，json  表示json对象)

```js
// ajax请求
				$("#ajaxBtn").click(function(){
					$.ajax({
						url:"http://localhost:8080/12_JSON/ajaxServlet",
						data:{action:"ajaxServletRequest"},
						// data:"action=ajaxServletRequest",
						type:"GET",
						success:function (data) {
							alert("服务器返回的数据是：" + data);
							$("#msg").html("编号：" + data.id + " , 姓名：" + data.name);
						},
						dataType:"json"
					});
				});
```

* $.get方法和$.post方法
  * url  请求的url地址
  * data  发送的数据
  * callback  成功的回调函数
  * type  返回的数据类型

```js
// ajax--get请求
$("#getBtn").click(function(){								  	    $.get("http://localhost:8080/12_JSON/ajaxServlet","action=ajaxServletRequest",function (data) {
						$("#msg").html("编号：" + data.id + " , 姓名：" + data.name);
                       },"json");
				});
				
// ajax--post请求
$("#postBtn").click(function(){
// post请求
   $.post("http://localhost:8080/12_JSON/ajaxServlet","action=ajaxServletRequest",function (data) {
						$("#msg").html("编号：" + data.id + " , 姓名：" + data.name);
					},"json");
				});

```

* $.getJSON方法
  * url  请求的url地址
  * data  发送给服务器的数据
  * callback  成功的回调函数

```js
	// ajax--getJson请求
				$("#getJSONBtn").click(function(){
					// 调用
					// alert("getJSON btn");
					$.getJSON("http://localhost:8080/12_JSON/ajaxServlet\",\"action=ajaxServletRequest","action=ajaxServletRequest",function (data) {
						$("#msg").html("编号：" + data.id + " , 姓名：" + data.name);
					});
				});
```

* 表单序列化  serialize()
  * serialize() 可以把表单中所有表单项的内容都获取到，并以name=value&name=value的形式进行拼接

```js
	// ajax请求
				$("#submit").click(function(){
					// 把参数序列化
					a$.getJSON("http://localhost:8080/12_JSON/ajaxServlet","action=ajaxServletRequest&"+$("#form01").serialize(),function (data) {
						$("#msg").html("编号：" + data.id + " , 姓名：" + data.name);
					});
				});
```

