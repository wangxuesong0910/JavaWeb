# Filter过滤器

## Filter之初体验

* Filetr工作的流程图

![](.\Filter工作流程图.JPG)

* Filter过滤器的使用步骤
  1. 编写一个类实现Filter接口
  2. 实现过滤方法 doFilter()
  3. 到web.xml 中去配置Filter 的拦截路径

```java
public class AdminFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {

    }

    /**
     * doFilter方法：专门用于拦截请求，可以作权限检查
     * @param servletRequest
     * @param servletResponse
     * @param filterChain
     * @throws IOException
     * @throws ServletException
     */
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;

        HttpSession session = httpServletRequest.getSession();
        Object user = session.getAttribute("user");
        //如果user == null,说明还没有登录
        if (user == null){
            servletRequest.getRequestDispatcher("/index.jsp").forward(servletRequest,servletResponse);
        }else {
            //让程序继续往下访问用户的目标资源
            filterChain.doFilter(servletRequest,servletResponse);
        }
    }

    @Override
    public void destroy() {

    }
}

```

```xml
<!--    filter标签用于配置一个Filter过滤器-->
    <filter>
<!--        给filter起一个别名-->
        <filter-name>AdminFilter</filter-name>
<!--        配置filter全类名-->
        <filter-class>xyz.bubudeai.FilterTest.AdminFilter</filter-class>
    </filter>

<!--    filter-mapping配置filter过滤器的拦截路径-->
    <filter-mapping>
<!--        filter-name 表示当前的拦截路径给哪个filter使用-->
        <filter-name>AdminFilter</filter-name>
        <!--url-pattern 配置拦截路径
         / 表示请求地址为：http://ip:port/工程路径/ 映射到 IDEA 的 web 目录
         /admin/* 表示请求地址为：http://ip:port/工程路径/admin/* -->
        <url-pattern>/admin/*</url-pattern>
    </filter-mapping>
```

## 完整的用户登录

* 结合上面所写的Filter过滤器，通过校验session中是否包含user值，来对用户登录进行校验

1. login.jsp页面 == 登录表单

   ```jsp
   这是登录页面。login.jsp 页面 <br>
   <form action="http://localhost:8080/11_Filter/loginServlet" method="get">
       用户名：<input type="text" name="username"/> <br>
       密 码：<input type="password" name="password"/> <br> <input type="submit" />
   ```

2. LoginServlet程序

   ```java
   public class LoginServlet extends HttpServlet {
       protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
   
       }
   
       protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           response.setContentType("text/html;charset=UTF-8");
           String username = request.getParameter("username");
           String password = request.getParameter("password");
   
           if ("wxs".equals(username) && "123456".equals(password)) {
               request.getSession().setAttribute("user",username);
               response.getWriter().write("登录成功");
           }else {
               request.getRequestDispatcher("/login.jsp").forward(request,response);
           }
       }
   }
   ```

   

## Filter的生命周期

1. 构造器方法
2. init 初始化方法
   * 第1、2步，在web工程启动的时候执行（Filter已经创建）

3. doFilter 过滤方法
   * 第3步，每次拦截到请求，就会执行

4. destory销毁
   * 第4步，停止web工程的时候，就会执行(停止web工程，也会销毁Filter过滤器)

## FilterConfig 类

> FilterConfig 类 见名知意，它是Filter 过滤器的配置文件类
>
> Tomcat 每次创建Filter 的时候，也会同时创建一个FilterConfig 类，这里包含了Filter配置文件的配置信息

* FilterConfig 类的作用是获取filter过滤器的配置内容
  1. 获取Filter 的名称 filter-name 的内容
  2. 获取在Filter中配置的init-param 初始化参数
  3. 获取ServletContext 对象

## FilterChain 过滤器链

* filter 过滤器
* Chain 链，链条
* FilterChain 就是过滤器链条（多个过滤器一起工作）

![](.\FilterChain过滤器链.JPG)

## Filter 的拦截路径

1. 精确匹配

   ```xml
   <url-pattern>/target.jsp</url-pattern> 
   以上配置的路径，表示请求地址必须为：http://ip:port/工程路径/target.jsp
   ```

2. 后缀名匹配

   ```xml
   <url-pattern>*.html</url-pattern> 
   以上配置的路径，表示请求地址必须以.html 结尾才会拦截到
   <url-pattern>*.do</url-pattern> 
   以上配置的路径，表示请求地址必须以.do 结尾才会拦截到
   <url-pattern>*.action</url-pattern> 
   以上配置的路径，表示请求地址必须以.action 结尾才会拦截到
   ```

   * Filter 过滤器它只关心请求的地址是否匹配，不关心请求的资源是否存在！！！

3. 目录匹配

   ```xml
   <url-pattern>/admin/*</url-pattern> 
   以上配置的路径，表示请求地址必须为：http://ip:port/工程路径/admin/*
   ```




## ThreadLocal的使用

- ThreadLocal的作用，它可以解决多线程的数据安全问题
- ThreadLocal 它可以给当前线程关联一个数据（可以是普通变量，也可以是对象，也可以是数组，集合）
- ThreadLocal的特点
  1. Thread Local 可以为当前线程关联一个数据，（它可以像Map一样存取数据，key为当前线程）
  2. 每一个ThreadLocal对象，只能为当前线程关联一个数据，如果要为当前线程关联多个数据，就需要使用多个threadLocal 对象实例
  3. 每个ThreadLocal 对象实例定义的时候，一般都是static类型
  4. ThreadLocal中保存数据，在线程销毁后，会由JVM虚拟机自动释放
- 代码

```java
public class OrderService {

    public void createOrder(){
        String name = Thread.currentThread().getName();
        System.out.println("OrderService 当前线程[" + name + "]中保存的数据是：" + ThreadLocalTest.threadLocal.get());
    }
}

```

```java
public class ThreadLocalTest implements Runnable {
    public static ThreadLocal<Object>  threadLocal = new ThreadLocal<>();
    private static Random random = new Random();

    @Override
    public void run() {
        // 1. 在run方法中，随机生成一个变量（线程要关联的数据），然后已当前线程名为key保存到map中
        int i = random.nextInt(1000);

        //获取当前线程名
        String name = Thread.currentThread().getName();
        System.out.println("线程["+name+"]生成的随机数是：" + i);

        //将获得的随机数放置在threadLocal中
        threadLocal.set(i);

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        new OrderService().createOrder();

        //在run方法结束之前，以当前线程名获取出数据，并打印，查看是否可以取出操作
        Object o = threadLocal.get();
        System.out.println("在线程["+name+"]快结束时取出关联的数据是：" + o);
    }

    public static void main(String[] args) {
        for (int i = 0; i < 3; i++) {
            new Thread(new ThreadLocalTest()).start();
        }
    }
}
```

## 为什么使用ThreadLocal来修改代码？

> 为了确保所有的针对数据库的操作，都是用同一个Connection连接，用来保持数据库的完整性
>
> 通俗讲：用ThreadLocal来实现数据库的事务处理，确保全部操作都在同一个线程内的同一个Connection连接中完成

* 下面针对原有的一个订单模块的代码实现事务管理

  1. 原代码

  ```java
  //德鲁伊数据库连接池
  public class DruidJDBC {
      private static DruidDataSource source;
      static {
          try {
              Properties properties = new Properties();
              InputStream is = DruidJDBC.class.getClassLoader().getResourceAsStream("DruidJDBC.properties");
  
              properties.load(is);
  
              source = (DruidDataSource)DruidDataSourceFactory.createDataSource(properties);
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  
      //获取数据库连接池Druid
      public static Connection getConnection() {
          Connection connection = null;
          try {
              connection = source.getConnection();
          } catch (Exception e) {
              e.printStackTrace();
          }
          return connection;
      }
  
      //关闭连接1
      public static void closeConn(Connection connection, Statement ps){
          try {
              if (connection!=null)
              connection.close();
          } catch (SQLException e) {
              e.printStackTrace();
          }
          try {
              if (ps!=null)
              ps.close();
          } catch (SQLException e) {
              e.printStackTrace();
          }
      }
  ```

  ```java
  //BaseDao中对数据库进行的操作
  
  //使用DBUtils操作数据库
      private QueryRunner run = new QueryRunner();
  
      //通用增删改(DBUtils版本)
      public void update(String sql,Object...args){
  
              Connection connection = DruidJDBC.getConnection();
          try {
              run.update(connection,sql,args);
          } catch (Exception e) {
              e.printStackTrace();
          }finally {
              DruidJDBC.closeConn(connection,null);
          }
  
      }
  ```

  ```java
  //OrderServlet的操作
  public class OrderServlet extends BaseServlet {
      private OrderService orderService = new OrderServiceImpl();
      protected void createOrder(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          //先获取Cart购物车对象
          Cart cart = (Cart) request.getSession().getAttribute("cart");
  
          //获取Userid
          User loginUser = (User) request.getSession().getAttribute("user");
  
          if (loginUser == null){
              request.getRequestDispatcher("/pages/user/login.jsp").forward(request,response);
              return;
          }
  
  
          Integer userId = loginUser.getId();
  
          //调用 orderService.createOrder(Cart,Userid);生成订单
          String orderId = orderService.createOrder(cart, userId);
  
          //request.setAttribute("orderId",orderId)
          //请求转发到/pages/cart/checkout.jsp
          // req.getRequestDispatcher("/pages/cart/checkout.jsp").forward(req, resp);
          request.getSession().setAttribute("orderId",orderId);
  
          response.sendRedirect(request.getContextPath()+"/pages/cart/checkout.jsp");
  
      }
  }
  ```

  ```java
  public abstract class BaseServlet  extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
         doPost(req, resp);
      }
      @Override
      protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          req.setCharacterEncoding("UTF-8");
          String action = req.getParameter("action");
          try {
              // 获取action业务鉴别字符串，获取相应的业务 方法反射对象
              Method method = this.getClass().getDeclaredMethod(action, HttpServletRequest.class, HttpServletResponse.class);
  //            System.out.println(method);
              // 调用目标业务 方法
              method.invoke(this, req, resp);
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```

  

  * 使用ThreadLocal实现事务管理后的代码(注意修改之处与之前的区别)

  ```java
  //JDBC工具类
  
  private static DruidDataSource source;
      //获取ThreadLocal对象（*************）
      private static ThreadLocal<Connection> conns = new ThreadLocal<Connection>();
      static {
          try {
              Properties properties = new Properties();
              InputStream is = DruidJDBC.class.getClassLoader().getResourceAsStream("DruidJDBC.properties");
  
              properties.load(is);
  
              source = (DruidDataSource)DruidDataSourceFactory.createDataSource(properties);
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  
      //获取数据库连接池Druid
      public static Connection getConnection() {
          Connection connection = conns.get();//（*********）
          if (connection ==  null){
              try {
                  //数据库连接池中获取连接
                  connection = source.getConnection();
  
                  //保存到ThreadLocal对象中，供后面的JDBC操作使用
                  conns.set(connection);
  
                  //设置为手动管理事务
                  connection.setAutoCommit(false);
              } catch (SQLException e) {
                  e.printStackTrace();
              }
          }
          return connection;
      }
  
  
      /**
       * 提交事务，并关闭释放连接
       */
      public static void commitAndClose(){
          Connection connection = conns.get();
  
          if (connection != null){//如果不等于null，说明之前使用过连接，操作过数据库（*****）
              try {
                  connection.commit();//提交事务
              } catch (SQLException e) {
                  e.printStackTrace();
              }finally {
                  try {
                      connection.close();
                  } catch (SQLException e) {
                      e.printStackTrace();
                  }
              }
  
          }
          // 一定要执行 remove 操作，否则就会出错。（因为 Tomcat 服务器底层使用了线程池技术）
          conns.remove();
      }
  
      /**
       *回滚事务，并关闭释放连接
       */
      public static void rollbackAndClose(){
          Connection connection = conns.get();
  
          if (connection != null){ //如果不等于null，说明之前使用过的连接，操作过数据库(*****)
              try {
                  connection.rollback();
              } catch (SQLException e) {
                  e.printStackTrace();
              }finally {
                  try {
                      connection.close();
                  } catch (SQLException e) {
                      e.printStackTrace();
                  }
              }
  
          }
  // 一定要执行 remove 操作，否则就会出错。（因为 Tomcat 服务器底层使用了线程池技术）
          conns.remove();
      }
  
  ```

  ```java
  public abstract class BaseDao {
      //使用DBUtils操作数据库
      private QueryRunner run = new QueryRunner();
  
      //通用增删改(DBUtils版本)
      public void update(String sql,Object...args){
  
              Connection connection = DruidJDBC.getConnection();
          try {
              run.update(connection,sql,args);
          } catch (Exception e) {
              e.printStackTrace();
  
              //修改之处，将此处捕获的异常，抛出
              throw new RuntimeException(e);
          }
  
      }
  
      //通用查询（DBUtils版）
      //查询一条记录
      public <T> T queryForOne(Class<T> clazz,String sql,Object...args){
  
          Connection connection = DruidJDBC.getConnection();
          try {
              //**BeanHandler：**将结果集中的第一行数据封装到一个对应的JavaBean实例中。
              BeanHandler<T> beanHandler = new BeanHandler<>(clazz);
  
              //public Object query(Connection conn, String sql, ResultSetHandler rsh,Object... params) throws SQLException：
              // 执行一个查询操作，在这个查询中，对象数组中的每个元素值被用来作为查询语句的置换参数。
              // 该方法会自行处理 PreparedStatement 和 ResultSet 的创建和关闭。
              T t = run.query(connection, sql, beanHandler, args);
              return t;
          } catch (SQLException e) {
              e.printStackTrace();
              throw new RuntimeException(e);
          }
      }
  
      //查询多条记录
      public <T> List<T> queryAll(Class<T> clazz,String sql,Object...args){
          Connection connection = DruidJDBC.getConnection();
          try {
              //BeanListHandler：**将结果集中的每一行数据都封装到一个对应的JavaBean实例中，存放到List里。
              BeanListHandler<T> beanListHandler = new BeanListHandler<>(clazz);
  
              List<T> query = run.query(connection, sql, beanListHandler, args);
  
              return query;
          } catch (SQLException e) {
              e.printStackTrace();
              throw new RuntimeException(e);
          }
      }
  
      //查询单个值
      public Object queryForsingleValue(String sql,Object...args){
          Connection connection = DruidJDBC.getConnection();
          try {
  
              ScalarHandler scalarHandler = new ScalarHandler();
              Object query = run.query(connection, sql, scalarHandler, args);
              return query;
          } catch (SQLException e) {
              e.printStackTrace();
              throw new RuntimeException(e);
          }
      }
  
  
  
  }
  
  ```

  ```java
  public abstract class BaseServlet  extends HttpServlet {
      @Override
      protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
         doPost(req, resp);
      }
      @Override
      protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
          req.setCharacterEncoding("UTF-8");
          String action = req.getParameter("action");
          try {
              // 获取action业务鉴别字符串，获取相应的业务 方法反射对象
              Method method = this.getClass().getDeclaredMethod(action, HttpServletRequest.class, HttpServletResponse.class);
  //            System.out.println(method);
              // 调用目标业务 方法
              method.invoke(this, req, resp);
          } catch (Exception e) {
              e.printStackTrace();
  
              /**
               * 修改之处：一定记得把BaseServlet中的异常往外抛给Filter过滤器
               */
              //把异常抛给Filter过滤器
              throw  new RuntimeException(e);
          }
      }
  
  
  }
  
  ```

  ```java
  public class TransactionFilter implements Filter {
      public void destroy() {
      }
  
      public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
          try {
              chain.doFilter(req, resp);
              /**
               * 提交事务
               */
              DruidJDBC.commitAndClose();
          } catch (IOException e) {
              e.printStackTrace();
          } catch (ServletException e) {
              /**
               * 回滚事务
               */
              DruidJDBC.rollbackAndClose();
              e.printStackTrace();
          }
  
  
      }
  
      public void init(FilterConfig config) throws ServletException {
  
      }
  
  }
  
  ```

  



