

内置对象特点:

1. 由JSP规范提供,不用编写者实例化。

2. 通过Web容器实现和管理

3. 所有JSP页面均可使用

4. 只有在脚本元素的表达式或代码段中才可使用(<%=使用内置对象%>或<%使用内置对象%>)

 常用内置对象:

1. 输出输入对象:request对象、response对象、out对象

2. 通信控制对象:pageContext对象、session对象、application对象

3. Servlet对象:page对象、config对象

4. 错误处理对象:exception对象

 

对象常用方法说明:

1.out对象(数据流 javax.servlet.jsp.jspWriter)

| 方法名         | 说明                              |
| -------------- | --------------------------------- |
| print或println | 输出数据                          |
| newLine        | 输出换行字符                      |
| flush          | 输出缓冲区数据                    |
| close          | 关闭输出流                        |
| clear          | 清除缓冲区中数据,但不输出到客户端 |
| clearBuffer    | 清除缓冲区中数据,输出到客户端     |
| getBufferSize  | 获得缓冲区大小                    |
| getRemaining   | 获得缓冲区中没有被占用的空间      |
| isAutoFlush    | 是否为自动输出                    |

2.request对象(请求信息 javax.servlet.http.HttpServletrequest)

| 方法名               | 说明                                                         |
| -------------------- | ------------------------------------------------------------ |
| isUserInRole         | 判断认证后的用户是否属于某一成员组                           |
| getAttribute         | 获取指定属性的值,如该属性值不存在返回Null                    |
| getAttributeNames    | 获取所有属性名的集合                                         |
| getCookies           | 获取所有Cookie对象                                           |
| getCharacterEncoding | 获取请求的字符编码方式                                       |
| getContentLength     | 返回请求正文的长度,如不确定返回-1                            |
| getHeader            | 获取指定名字报头值                                           |
| getHeaders           | 获取指定名字报头的所有值,一个枚举                            |
| getHeaderNames       | 获取所有报头的名字,一个枚举                                  |
| getInputStream       | 返回请求输入流,获取请求中的数据                              |
| getMethod            | 获取客户端向[服务器](http://www.23book.net/Server/Index.htm)端传送数据的方法 |
| getParameter         | 获取指定名字参数值                                           |
| getParameterNames    | 获取所有参数的名字,一个枚举                                  |
| getParameterValues   | 获取指定名字参数的所有值                                     |
| getProtocol          | 获取客户端向[服务器](http://www.23book.net/Server/Index.htm)端传送数据的协议名称 |
| getQueryString       | 获取以get方法向[服务器](http://www.23book.net/Server/Index.htm)传送的查询字符串 |
| getRequestURI        | 获取发出请求字符串的客户端地址                               |
| getRemoteAddr        | 获取客户端的IP地址                                           |
| getRemoteHost        | 获取客户端的名字                                             |
| getSession           | 获取和请求相关的会话                                         |
| getServerName        | 获取[服务器](http://www.23book.net/Server/Index.htm)的名字   |
| getServerPath        | 获取客户端请求文件的路径                                     |
| getServerPort        | 获取[服务器](http://www.23book.net/Server/Index.htm)的端口号 |
| removeAttribute      | 删除请求中的一个属性                                         |
| setAttribute         | 设置指定名字参数值                                           |

 

3.response对象(响应 javax.servlet.http.HttpServletResponse)

| 方法名          | 说明                               |
| --------------- | ---------------------------------- |
| addCookie       | 添加一个Cookie对象                 |
| addHeader       | 添加Http文件指定名字头信息         |
| containsHeader  | 判断指定名字Http文件头信息是否存在 |
| encodeURL       | 使用sessionid封装URL               |
| flushBuffer     | 强制把当前缓冲区内容发送到客户端   |
| getBufferSize   | 返回缓冲区大小                     |
| getOutputStream | 返回到客户端的输出流对象           |
| sendError       | 向客户端发送错误信息               |
| sendRedirect    | 把响应发送到另一个位置进行处理     |
| setContentType  | 设置响应的MIME类型                 |
| setHeader       | 设置指定名字的Http文件头信息       |

4.session对象(会话 javax.servlet.http.HttpSession)

| 方法名                 | 说明                                    |
| ---------------------- | --------------------------------------- |
| getAttribute           | 获取指定名字的属性                      |
| getAttributeNames      | 获取session中全部属性名字,一个枚举      |
| getCreationTime        | 返回session的创建时间                   |
| getId                  | 获取会话标识符                          |
| getLastAccessedTime    | 返回最后发送请求的时间                  |
| getMaxInactiveInterval | 返回session对象的生存时间单位千分之一秒 |
| invalidate             | 销毁session对象                         |
| isNew                  | 每个请求是否会产生新的session对象       |
| removeAttribute        | 删除指定名字的属性                      |
| setAttribute           | 设定指定名字的属性值                    |

5.pageContext对象(页面上下文 javax.servlet.jsp.PageContext)

| 方法名            | 说明                                 |
| ----------------- | ------------------------------------ |
| forward           | 重定向到另一页面或Servlet组件        |
| getAttribute      | 获取某范围中指定名字的属性值         |
| findAttribute     | 按范围搜索指定名字的属性             |
| removeAttribute   | 删除某范围中指定名字的属性           |
| setAttribute      | 设定某范围中指定名字的属性值         |
| getException      | 返回当前异常对象                     |
| getRequest        | 返回当前请求对象                     |
| getResponse       | 返回当前响应对象                     |
| getServletConfig  | 返回当前页面的ServletConfig对象      |
| getServletContext | 返回所有页面共享的ServletContext对象 |
| getSession        | 返回当前页面的会话对象               |

 

6.application对象(应用程序 javax.servlet.ServletContext)

| 方法名            | 说明                                  |
| ----------------- | ------------------------------------- |
| getAttribute      | 获取应用对象中指定名字的属性值        |
| getAttributeNames | 获取应用对象中所有属性的名字,一个枚举 |
| getInitParameter  | 返回应用对象中指定名字的初始参数值    |
| getServletInfo    | 返回Servlet编译器中当前版本信息       |
| setAttribute      | 设置应用对象中指定名字的属性值        |

7.config对象(Servlet的配置信息 javax.servlet.ServletConfig)

| 方法名                | 说明                                 |
| --------------------- | ------------------------------------ |
| getServletContext     | 返回所执行的Servlet的环境对象        |
| getServletName        | 返回所执行的Servlet的名字            |
| getInitParameter      | 返回指定名字的初始参数值             |
| getInitParameterNames | 返回该JSP中所有的初始参数名,一个枚举 |

8.page对象(当前JSP的实例,java.lang.object)

它代表JSP被编译成Servlet,可以使用它来调用Servlet类中所定义的方法

9.exception对象(运行时的异常,java.lang.Throwable)

被调用的错误页面的结果,只有在错误页面中才可使用,

即在页面指令中设置:<%@page isErrorPage=“true”%>

 

Request(Javax.servlet.ServletRequest)它包含了有关浏览器请求的信息.通过该对象可以获得请求中的头信息、Cookie和请求参数。

Response(Javax.servlet.ServletResponse)作为JSP页面处理结果返回给用户的响应存储在该对象中。并提供了设置响应内容、响应头以及重定向的方法(如cookies,头信息等)

Out(Javax.servlet.jsp.JspWriter)用于将内容写入JSP页面实例的输出流中,提供了几个方法使你能用于向浏览器回送输出结果。

pageContext(Javax.servlet.jsp.PageContext)描述了当前JSP页面的运行环境。可以返回JSP页面的其他隐式对象及其属性的访问,另外,它还实现将控制权从当前页面传输至其他页面的方法。

Session(javax.servlet.http.HttpSession)会话对象存储有关此会话的信息,也可以将属性赋给一个会话,每个属性都有名称和值。会话对象主要用于存储和检索属性值。

Application(javax.servle.ServletContext)存储了运行JSP页面的servlet以及在同一应用程序中的任何Web组件的上下文信息。

Page(Java.lang.Object)表示当前JSP页面的servlet实例

Config(javax.servlet.ServletConfig)该对象用于存取servlet实例的初始化参数。

Exception(Javax.lang.Throwable)在某个页面抛出异常时,将转发至JSP错误页面,提供此对象是为了在JSP中处理错误。只有在错误页面中才可使用<%@page isErrorPage=“true”%>

 

| **Jsp**内置对象 | **功能**                                                     | **主要方法**                                                 |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| out             | 向客户端输出数据                                             | print() println() flush() clear() isAutoFlush() getBufferSize()   close() ………… |
| request         | 向客户端请求数据                                             | getAttributeNames() getCookies() getParameter() getParameterValues() setAttribute() getServletPath() ………….. |
| response        | 封装了jsp产生的响应,然后被发送到客户端以响应客户的请求       | addCookie() sendRedirect() setContentType()flushBuffer() getBufferSize() getOutputStream()sendError() containsHeader()…………… |
| application     |                                                              |                                                              |
| config          | 表示Servlet的配置,当一个Servlet初始化时,容器把某些信息通过此对象传递给这个Servlet | getServletContext() getServletName() getInitParameter()   getInitParameterNames()…………… |
| page            | Jsp实现类的实例,它是jsp本身,通过这个可以对它进行访问         | flush()………                                                   |
| pagecontext     | 为JSP页面包装页面的上下文。管理对属于JSP中特殊可见部分中己经命名对象的该问 | forward() getAttribute() getException() getRequest() getResponse()   getServletConfig()getSession() getServletContext() setAttribute()removeAttribute() findAttribute() …………… |
| session         | 用来保存每个用户的信息,以便跟踪每个用户的操作状态            | getAttribute() getId()   getAttributeNames() getCreateTime() getMaxInactiveInterval()invalidate() isNew() |
| exception       | 反映运行的异常                                               | getMessage()…………                                             |



####  内置对象说明

1. `out`对象(输出对象)

   作用：动态的向JSP页面输出字符流，从而把动态内容转换为html形式展示

   常用方法：`print/println, write`

   > print()和println()方法可将各种类型的数据转换成字符串的形式输出，而write()方法只能输出字符、字符数组和字符串等与字符相关的数据。

2. `request`对象(请求对象)

   1. 每个request对象封装着一次用户的请求，并且所有的请求参数都被封装在request对象中，因此request对象是获取请求参数的重要途径。

   2. 作用域：

      > **request** 指在一次请求的全过程中有效，即从http请求到服务器处理结束，返回响应的整个过程，存放在**HttpServletRequest**对象中。在这个过程中可以使用forward方式跳转多个jsp。在这些页面里你都可以使用这个变量。**request**里的变量可以跨越forward前后的两页。但是只要刷新页面，它们就重新计算了。 

   3. 常用方法

      1. `getParameter(String name)`获取名字为name请求参数

         ```jsp
         #demo.jsp
         <from method="get" action="getPara.jsp">
         <input value="world" name="hello">
         <input type="summbit" vaule="提交">
         </from>
         ```

         ```jsp
         #getPara.jsp
         <%
         	String v = requests.getParameter("hello");
         	//v的值就是world
         %>
         ```

      2. getParameterValues(String name)`获取客户端中参数名为name的所有值

      3. `getCookies()`返回客户端的所有cookie对象，结果是一个cookie数组

      4. 更多方法：https://blog.csdn.net/windy8833/article/details/5356252

3. `response`对象(响应对象)

   1. 常用方法解析：http://www.51gjie.com/javaweb/825.html

4. `session`对象(会话对象)

   1. 表示浏览器与服务器之间的一次会话。一次会话指的是从客户端浏览器链接服务器开始，到服务器会话过期或用户主动退出后，会话结束。这个过程中可以有多次请求与响应

   2.  如果把变量放到session里，就说明它的作用域是session，它的有效范围是当前会话。 所谓当前会话，就是指从用户打开浏览器开始，到用户关闭浏览器这中间的过程。这个过程可能包含多个请求响应。也就是说，只要用户不关浏览器，服务器就有办法知道这些请求是一个人发起的，整个过程被称为一个会话（session），而放到会话中的变量，就可以在当前会话的所有请求里使用。 

   3. 作用域

      > **Session**是用户全局变量，在整个会话期间都有效。只要页面不关闭就一直有效（或者直到用户一直未活动导致会话过期，默认session过期时间为30分钟，或调用HttpSession的invalidate()方法）。存放在HttpSession对象中 。**session**的变量一直在累加，开始还看不出区别，只要关闭浏览器，再次重启浏览器访问这页，session里的变量就重新计算了。

   4. 常用方法

      >  **public void setAttribute(String name, Object value)** 
      > 使用指定的名称和值来产生一个对象并绑定到session中
      >
      > **public Object getAttribute(String name)**
      > 返回session对象中与指定名称绑定的对象，如果不存在则返回null

   5. 其他方法

      http://www.runoob.com/jsp/jsp-session.html

   6. 用处：相当于缓存机制，例如：用户购物时，因为无法确定用户是否需要，可以先保存到session，当确认需要时再存入数据库

5. `application`对象(应用程序上下文对象)

   1. 表示当前程序运行的环境，随着服务器的开启而产生，服务器关闭则销毁，即：存储的变量不手动删除则会一直存在，除非重启服务器。

   2. 作用域为整个web容器，即只要服务没关闭，在服务内的任意位置内都可以进行访问。(相当于全局变量，随着主函数的产生而产生，贯穿整个程序的生命周期)

   3. 常用方法

      >  **public void setAttribute(String name, Object value)** 
      > 使用指定的名称和值来产生一个对象并绑定到session中
      >
      > **public Object getAttribute(String name)**
      > 返回session对象中与指定名称绑定的对象，如果不存在则返回null

   4. 其他方法

      > ```
      > String getAttribute(String name) 根据属性名称获取属性值。
      > Enumeration getAttributeNames() 获取所有的属性名称。
      > void setAttribute(String name, Object object) 设置属性，指定属性名称和属性值。
      > void removeAttribute(String name) 根据属性名称删除对应的属性。
      > ServletContext getContext(String uripath) 获取指定URL的ServletContext对象。
      > String getContextPath() 获取当前Web应用程序的根目录。
      > String getInitParameter(String name) 根据初始化参数名称，获取初始化参数值。
      > int getMajorVersion() 获取Servlet API的主版本号。
      > int getMinorVersion() 获取Servlet API的次版本号。
      > String getMimeType(String file) 获取指定文件的MIME 类型。
      > String getServletInfo() 获取当前Web服务器的版本信息。
      > String getServletContextName() 获取当前Web应用程序的名称。
      > void log(String message) 将信息写入日志文件中。
      > ```

   5. 作用：用户登录时，记住登录状态