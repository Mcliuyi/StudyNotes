# IDEA使用Maven创建SpringMVC项目

## 1. 创建新的Maven项目

选中maven项目并创建

![创建maven](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/create_maven.jpg)

### 1.1 设置包名和项目名

可以设置为相同的

![设置包名和项目名](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/create_maven2.jpg)

### 1.2 添加配置键值对

> name: archetypeCatalog 
>
> value: internal

目的: 为了加快创建spring项目

如果配置了国内镜像的maven则可以跳过这一步

添加成功后，一直点`next`下一步直到项目创建完成即可

![添加键值对](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/addKeyValue.jpg)

### 1.3 配置阿里云镜像(可选)

打开maven的安装目录下的`conf`目录

编辑文件`setting.xml`

添加下列配置

```xml
<mirror>
        <id>nexus-aliyun</id>
        <mirrorOf>central</mirrorOf>
        <name>Nexus aliyun</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
#pom.xlm
<repositories>
        <repository>
            <id>nexus-aliyun</id>
            <name>Nexus aliyun</name>
            <url>http://maven.aliyun.com/nexus/content/groups/public</url>
        </repository>
    </repositories>
```

## 2.  配置SpringMVC

### 2.1 等待Maven将项目创建完成

创建完成后会显示一下信息

![创建完成](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/createFinal.jpg)

#### 2.1.1 创建完成后的目录结构

![目录结构](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/path.jpg)

### 2.2 补充目录结构

#### 2.2.1 添加resources和java目录

在`main`目录下创建`resources`目录和`java`

#### 2.2.2 设置项目跟路径配置文件路径

`java`目录设置为`Sources root`

![设置目录结构](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/setSourcesRoot.jpg)

`resources`目录设置为`Resources root`

![设置Resources](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/setResourcesRoot.jpg)

### 2.3 导入SpringMVC依赖包

在`pom.xml`文件中添加springmvc的依赖包，创建不一样效果的springmvc项目，配置文件会有所不同，可针对性去百度搜索。下面是使用jsp做前后端不分离的配置文件

```xml
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <spring.version>5.0.2.RELEASE</spring.version>
    <!-- 锁定spring版本这样在下面配置时不需要每个Spring包都指定版本,只需使用${spring.version}即可 -->
  </properties> 

<dependencies>
    <!-- Spring -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aspects</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jms</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context-support</artifactId>
      <version>${spring.version}</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>${spring.version}</version>
    </dependency>

    <!-- jsp servlet 配置 -->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>2.5</version>
      <scope>provided</scope>
    </dependency>

    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.2</version>
      <scope>provided</scope>
    </dependency>
</dependencies>
```

### 2.4 配置`web.xml`文件

```xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>

  <servlet>
    <servlet-name>springmvc</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <!-- 指定加载的配置文件 ，通过参数contextConfigLocation加载-->
     <init-param>
         <param-name>contextConfigLocation</param-name>
         <param-value>classpath:springmvc.xml</param-value>
     </init-param>
      <load-on-startup>1</load-on-startup>
  </servlet>

  <servlet-mapping>
      <!-- 前端控制器，拦截所有请求 -->
    <servlet-name>springmvc</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>

```

### 2.5 添加SpringMvc的配置文件

在`resources`目录下添加spring的配置文件，如果没有`Spring Config`的选项，不要着急，是因为刚刚配置的spring包还没有导入，点击左下角有个弹窗`import change`的选项，等待导入完成后就有`Spring Config`的选项了

![addxml](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/addSpringXml.jpg)

#### 2.5.1 添加配置内容

以下配置文件均是针对jsp的，如果是想创建ssm架构会有细微差距

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/task
       http://www.springframework.org/schema/task/spring-task.xsd
       http://www.springframework.org/schema/mvc
       http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- 设置默认配置方案 -->
    <mvc:annotation-driven />
    <!-- 包扫描，将注解的类注入com.demo为你的包路径, java目录下的，如果还没创建包的话会报错，可以先创建 -->
    <context:component-scan base-package="com.demo"/>

    <!-- 视图解析器 -->
    <bean class="org.springframework.web.servlet.view.UrlBasedViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.InternalResourceView"/>
        <!-- 前缀（目录） -->
        <property name="prefix" value="/WEB-INF/page/" />
        <!-- 后缀（文件名） -->
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>

```

### 2.6 添加启动项

![succes](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/addproject.png)

![final](https://ly-markdown.oss-cn-shenzhen.aliyuncs.com/final.jpg)

