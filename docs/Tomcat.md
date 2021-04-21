##### Tomcat



- Tomcat本质上是一个servlet容器。



- 用户在浏览器输入(localhost:8080/a/b)，Tomcat创建servlet，处理业务逻辑，并返回html流程：

  1. tomcat先在server.xml下的Context容器下找a目录对应的web服务路径，参考如下：

  ```xml
  // tomcat的server.xml
  <Context path = "/a" docBase = "/Users/linzeyang/Desktop/me/gitHub/myWebApp/target/testlzy.war"/>
  ```

  2. 找到服务路径后，去该路径下的web.xml文件找b目录对应的class地址，参考如下：

  ```xml
  // 服务的web.xml
      <servlet>
          <servlet-name>testS</servlet-name>
          <servlet-class>com.cecd.TestServlet</servlet-class>
      </servlet>
  
      <servlet-mapping>
          <servlet-name>testS</servlet-name>
          <url-pattern>/b</url-pattern>
      </servlet-mapping>
  ```

  3. 找到class地址后（com.cecd.TestServlet，该class必然实现servlet接口），tomcat利用反射机制创建servlet对象。

  4. 调用该class的init()方法
  5. 创建request,response对象，并调用service(request,response)方法，并在service方法中给浏览器做响应。

![tomcat流程](/Users/linzeyang/Desktop/shots/tomcat流程.png)