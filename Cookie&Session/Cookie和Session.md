# Cookie

## Cookie的含义：

1. Cookie 是服务器通知客户端保存键值对的一种技术
2. 客户端有了Cookie之后，每次请求都发送给服务器
3. 每个Cookie的大小不能超过4kb

## Cookie 的创建

![](.\Cookie的创建.JPG)

```java
 //Servlet中的代码
    protected void createCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.创建cookie 对象
        Cookie cookie = new Cookie("key", "value1");
        //2.通知客户端保存Cookie
        response.addCookie(cookie);
        response.getWriter().write("Cookie创建成功");

    }
```

## 服务器获取Cookie

* 服务器获取客户端的 Cookie 只需要一行代码：req.getCookies():Cookie[]

```java
    protected void getCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.获取Cookie数组
        Cookie[] cookies = request.getCookies();
        //2.循环遍历
        for (Cookie cookie: cookies) {
            // getName 方法返回 Cookie 的 key（名）
            // getValue 方法返回 Cookie 的 value 值
             response.getWriter().write("Cookie[" + cookie.getName() + "=" + cookie.getValue() + "] <br/>");
        }

    }
```

* 获取指定Cookie的值

```java
public class CookieUtils {
    //获取指定cookie值的工具类
    public static Cookie getCookies(String name, Cookie[] cookies) {
        if (name == null || cookies == null || cookies.length == 0) {
            return null;
        }
        for (Cookie cookie : cookies) {
            if (name.equals(cookie.getName())) {
                return cookie;
            }
        }
        return null;
    }
}
```

```java
 protected void getCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.获取Cookie数组
        Cookie[] cookies = request.getCookies();
        //2.循环遍历
        for (Cookie cookie: cookies) {
            // getName 方法返回 Cookie 的 key（名）
            // getValue 方法返回 Cookie 的 value 值
             response.getWriter().write("Cookie[" + cookie.getName() + "=" + cookie.getValue() + "] <br/>");
        }

        //使用工具类获取指定的Cookie值
        Cookie key = CookieUtils.getCookies("key", cookies);

        // 如果不等于null，说明赋过值，也就是找到了需要的Cookie
        if (key != null) {
            response.getWriter().write("找到了需要的Cookie");
        }

    }
```

## Cookie值的修改

```java
protected void updateCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.获取Cookie数组
        Cookie[] cookies = request.getCookies();

        //2.使用工具类获取指定的Cookie值
        Cookie key = CookieUtils.getCookies("key", cookies);

        // 3.如果不等于null，说明赋过值，也就是找到了需要的Cookie
        if (key != null) {
            //4.调用setValue（）方法用于赋予新的Cookie值
            key.setValue("newValue");

            //5.调用response.addCookie()通知客户端修改
            response.addCookie(key);
        }

    }
```

## Cookie生命控制

* setMaxAge()
  * 正数：表示在指定秒数后国企
  * 负数：表示浏览器一关，Cookie就会被删除（默认值：-1）
  * 零：表示马上删除Cookie

```java
  protected void defaultCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1.浏览器关闭，销毁Cookie
        Cookie cookie = new Cookie("defaultLife", "defaultLife");
        cookie.setMaxAge(-1);
        response.addCookie(cookie);
    }

    protected void deleteCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //立即删除Cookie
        Cookie cookie = CookieUtils.getCookies("key", request.getCookies());
        cookie.setMaxAge(0);
        response.addCookie(cookie);

        response.getWriter().write("key 的 Cookie 已经被删除");
    }

    protected void oneHourCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //创建有效时长为1小时的Cookie
        Cookie cookie = new Cookie("oneHourCookie", "oneHourCookie");
        cookie.setMaxAge(60*60);
        response.addCookie(cookie);

        response.getWriter().write(" oneHourCookie的 Cookie 存活为1小时");
    }
```

## Cookie的有效Path的设置

* Cookie 的 path 属性可以有效的过滤哪些 Cookie 可以发送给服务器。哪些不发。 path 属性是通过请求的地址来进行有效的过滤。 

![](.\Cookie的Path.JPG)

```java
 protected void testPathCookie(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //创建有效时长为1小时的Cookie
        Cookie cookie = new Cookie("path1", "path1");
        //// getContextPath() ===>>>> 得到工程路径
        cookie.setPath(request.getContextPath() + "/abc");// ===>>>> /工程路径/abc
        response.addCookie(cookie);

        response.getWriter().write("创建了一个带有 Path 路径的 Cookie");
    }
```

## 练习--免输入用户名登录

```java
//Servlet
public class LoginServlet extends HttpServlet {
    

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String username = req.getParameter("username");
        String password = req.getParameter("password");

        if ("wxs".equals(username) && "123".equals(password)){
            //登录成功
            Cookie cookie = new Cookie("username", username);
            cookie.setMaxAge(60*60);
            resp.addCookie(cookie);
            System.out.println("登录成功");
        }else {
            System.out.println("登录失败");
        }
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}

```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 22485
  Date: 2021/1/28
  Time: 11:32
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<form action="http://localhost:8080/10_cookiesession/loginServlet" method="get">
    用户名：<input type="text" name="username" value="${cookie.username.value}"> <br>
    密码：<input type="password" name="password"> <br>
    <input type="submit" value="登录">
</form>
</body>
</html>

```

# Session

1. Session 就是一个接口（HttpSession）
2. Session 就是会话，它是用来维护一个客户端和服务器之间关联的一种技术
3. 每个客户端都有自己的一个Session会话
4. Session 会话中，我们经常用来保存用户登录之后的信息

### Session域数据的获取

```java
protected void createOrGetSession(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //创建和获取Session会话对象
        /**
         * request.getSession()
         * 第一次调用是：创建 Session 会话
         * 之后调用都是：获取前面创建好的 Session 会话对象。
         */
        HttpSession session = request.getSession();
        //判断当前Session会话，是否是新创建出来的
        /**
         * isNew();判断到底是不是刚创建出来的（新的）
         * true 表示刚创建
         * false 表示获取之前创建
         */
        boolean isNew = session.isNew();
        //获取Session会话的唯一标识ID
        /**
         * 每个会话都有一个身份证号。
         * 也就是 ID 值。而且这个 ID 是唯一的。
         * getId() 得到 Session 的会话 id 值。
         */
        String id = session.getId();
        response.getWriter().write("得到的Session，它的id是：" + id + " <br /> ");
        response.getWriter().write("这个Session是否是新创建的：" + isNew + " <br /> ");

    }
```

### Session的声明周期

1. Session 默认的超时时长是多少?

   * Session 默认的超时时间长为 30 分钟。 

     因为在 Tomcat 服务器的配置文件 web.xml中默认有以下的配置，它就表示配置了当前 Tomcat 服务器下所有的 Session 

     超时配置默认时长为：30 分钟。 

     <session-config> 

     <session-timeout>30</session-timeout> 

     </session-config>

```xml
<!--如果说。你希望你的 web 工程，默认的 Session 的超时时长为其他时长。你可以在你自己的 web.xml 配置文件中做 以上相同的配置。就可以修改你的 web 工程所有 Seession 的默认超时时长。-->
<!--表示当前 web 工程。创建出来 的所有 Session 默认是 20 分钟 超时时长-->
<session-config> 
<session-timeout>20</session-timeout>
</session-config>
```

2. Servlet示例代码

   ```java
       protected void life3(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           //线获取Session对象
           HttpSession session = request.getSession();
   
           //让当前Session3秒后超市
           /**
            * public void setMaxInactiveInterval(int interval) 设置 Session 的超时时间（以秒为单位），
            * 超过指定的时长，Session 就会被销毁。
            * 值为正数的时候，设定 Session 的超时时长。
            * 负数表示永不超时（极少使用）
            */
           session.setMaxInactiveInterval(3);
   
           response.getWriter().write("当前 Session 已经设置为 3 秒后超时");
   
       }
   
       protected void deleteNow(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           //线获取Session对象
           HttpSession session = request.getSession();
   
           //让当前Session3秒后超市
           //public void invalidate() 让当前 Session 会话马上超时无效。
           session.invalidate();
   
           response.getWriter().write("当前 Session 立即超时");
   
       }
   
       protected void defaultLife(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           // 获取了Session的默认超时时长
           //public int getMaxInactiveInterval()获取 Session 的超时时间
           int maxInactiveInterval = req.getSession().getMaxInactiveInterval();
   
           resp.getWriter().write("Session的默认超时时长为：" + maxInactiveInterval + " 秒 ");
   
       }
   ```

   

