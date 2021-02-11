# 谷歌Kaptcha验证码的实现

## 解决表单重复提交之验证码

* 表单重复提交的三种情况

  1. 提交完表单。服务器使用请求转来进行页面跳转。这个时候，用户按下功能键 F5，就会发起最后一次的请求。 

     造成表单重复提交问题。解决方法：使用重定向来进行跳转

  2. 用户正常提交服务器，但是由于网络延迟等原因，迟迟未收到服务器的响应，这个时候，用户以为提交失败， 

     就会着急，然后多点了几次提交操作，也会造成表单重复提交。

  3. 用户正常提交服务器。服务器也没有延迟，但是提交完成后，用户回退浏览器。重新提交。也会造成表单重复 

     提交。

![](.\表单重复提交的底层原理.JPG)

## 谷歌Kaptcha图片验证码的使用

1. 导入谷歌验证码的 jar 包 ：kaptcha-2.3.2.jar 
2. 在 web.xml 中去配置用于生成验证码的 Servlet 程序

```xml
<servlet> 
<servlet-name>KaptchaServlet</servlet-name> 
<servlet-class>com.google.code.kaptcha.servlet.KaptchaServlet</servlet-class>
</servlet> 
<servlet-mapping> 
<servlet-name>KaptchaServlet</servlet-name>
<url-pattern>/kaptcha.jpg</url-pattern>
</servlet-mapping>
```

3. 在表单中使用 img 标签去显示验证码图片并使用它

```html
<img src="http://localhost:8080/tmp/kaptcha.jpg" alt="" style="width: 100px; height: 28px;"> 
```

4. 在服务器获取谷歌生成的验证码和客户端发送过来的验证码比较使用。

```java
@Override 
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException { 
// 获取 Session 中的验证码 String token = (String) req.getSession().getAttribute(KAPTCHA_SESSION_KEY); 
// 删除 Session 中的验证码 
req.getSession().removeAttribute(KAPTCHA_SESSION_KEY); 
String code = req.getParameter("code"); 
// 获取用户名 
String username = req.getParameter("username");
if (token != null && token.equalsIgnoreCase(code)) { 
System.out.println("保存到数据库：" + username); 
resp.sendRedirect(req.getContextPath() + "/ok.jsp"); 
} else {
System.out.println("请不要重复提交表单");
} }
```

5. 验证码点击切换（避免因浏览器缓存只能切换一次）

```js
// 给验证码的图片，绑定单击事件 
$("#code_img").click(function () { 
// 在事件响应的 function 函数中有一个 this 对象。这个 this 对象，是当前正在响应事件的 dom 对象 
// src 属性表示验证码 img 标签的 图片路径。它可读，可写 
// alert(this.src);
this.src = "${basePath}kaptcha.jpg?d=" + new Date();
});
```

 

