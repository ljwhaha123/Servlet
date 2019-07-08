# Servlet
面试题
1.一次servlet的请求过程
  tomcat在启动之后，Servlet此时已经准备就绪，首先tomcat会加载web.xml配置文件，将配置信息封装到ServletConfig中，然后开始初始化Servlet
  容器，首先调用init(ServletConfig conf)方法，初始化Servlet容器，当用户请求过来的时候，
  首先由tomcat处理，由server转发给servlce，然后servlce继续转发给Connector，Connector将http请求中的请求行，请求体，请求体中的
  信息解析出来封装到HttpServletRequest中，继续生成HttpServletResponse，完成之后由Contailer处理Servlet，执行Servlet中的
  Servlce(HttpServletRequest req,HttpServletResponse res)方法，这个方法的主要作用就是判断请求是get还是post。如果是get。那么执行
  doget方法，如果是post，那么执行dopost方法。完成业务逻辑之后，再返回到Connector中封装相应的信息，最后Connector通过Socket将相应信息
  返回到浏览器。一次请求到此执行完毕
2.servet的生命周期
  生命周期由javax.servlet.Servlet接口中的init方法和servlce方法和destroy方法控制，初始化的时候执行init()方法，然后执行servlce()方法，通过doget或者dopost方法执行
  业务逻辑，然后执行destroy方法销毁容器
3.Servlet中forward和redirect的区别
  forward是转发的意思，直观的区别就是浏览器的地址不会发生改变，因为浏览器在发送一次请求之后，服务器会自己去查找用户要查找的资源文件，最后返回用户
  redirect是重定向的意思，直观的区别就是浏览器的地址会发生变化，执行顺序为当用户发送请求之后，服务器发现请求的资源文件在另外一个位置，那么服务器将资源文件的
  的路径发送给浏览器，让浏览器自己再重新发送一次请求。所以地址就会变化。
4.jsp和Servlet的区别和联系
  Servlet的应用逻辑是在Java文件中，并且完全从表示层中的HTML里分离开来。而JSP的情况是Java和HTML可以组合成一个扩展名为.jsp的文件。
  JSP侧重于视图，Servlet主要用于控制逻辑。
5.Cookie和Session的区别和联系
  区别：
     Cookie是工作在浏览器的，Session是工作在服务器的
     Cookie存放的数据是有大小限制的，Session是没有限制的
     Cookie中的数据是明文的，不安全，容易Cookie欺骗，Session在服务器中保存。是安全的，但是不能保存太多的数据，否则服务器性能会下降
  联系：
     例如用户在登录的时候，将信息封装到http中发送到服务器。服务器响应之后将用户名保存到session中，然后自动
     生成一个sessionid。唯一标识这个session，然后封装到Cookie中和页面信息一起返回给用户，这样session和Cookie就联系起来了
     当用户再访问的时候，浏览器会把更新后的Cookie发送到服务器，（因为http请求是无状态的，每一次请求之间都没有关系，所以如果不用这个sessionid来做一个标识的话，服务器没办法确定这是同一个用户的请求）
     服务器首先获取Cookie中的sessionid，查看服务器中有没有这个sessionid。如果有的话，说明该用户之前已经登录过，允许进行后续的操作
    
  Cookie如果不设置过期时间。用户在关闭浏览器的时候，Cookie中的值会清空，再次请求的时候将会重新登录，所以服务器端要设置Cookie的过期时间。这样，浏览器将会把这个sessionid保存在本地硬盘中，
  用户每次重新打开浏览器都不需要重新登录
  双方互相配合完成功能，如果其中一方过期，都不能完成功能
 
6.什么是Servlet
  Servlet就是用来处理动态页面。主要用来处理form表单提交的数据
7.Servlet的体系结构
  要实现Servlet必须直接或者间接的实现javax.servlet.Servlet接口，或者是继承javax.servlet.GenericServlet或者继承javax.servlet.HttpServlet
