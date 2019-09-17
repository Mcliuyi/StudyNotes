# MyBatis教程

## 1. 利用idea创建Maven项目

### 1.1 查看项目结构

```shell
|____pom.xml
|____mybatisdemo.iml
|____.idea
|____src
| |____test
| | |____java
| |____main
| | |____resources
| | |____java
```

### 1.2 添加maven依赖

```xml
<properties>
  			<mysql-connector-java.version>5.1.35</mysql-connector-java.version>
        <mybatis.version>3.4.5</mybatis.version>
        <junit.version>4.11</junit.version>
    </properties>
<dependencies>
    <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>${mybatis.version}</version>
   </dependency>
   <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>${mysql-connector-java.version}</version>
    </dependency>
  
   <!-- Lombok插件 需要在idea上安装插件才能导入，作用-->
  <dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.18</version>
  </dependency>
</dependencies>
```

### 1.1.1 Lombok插件

具体使用安装参考: https://blog.csdn.net/MOTUI/article/details/79012846

## 2. 构建SqlSessionFactory

**SqlSessionFactory**相当于一个工厂，用于创建sqlSession对象，而sqlSession用于操作数据库

### 2.1 通过xml构建

#### 2.1.1 在`resources`目录下创建xml文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!-- 注意该属性必须放在最前面，因为源码中设计是需要先加载此配置！ -->
    <properties resource="config.properties"/>

    <typeAliases>
        <!-- 此处配置的是sql查询后返回的类型所在包位置 -->
        <package name="cn.ly.generato.pojo"></package>
    </typeAliases>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="${driver}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>
		<!-- 配置sql映射文件 -->
    <mappers>
        <mapper resource="mybatis/UserMapper.xml"/>
    </mappers>
</configuration>
```

#### 2.1.2 创建`config.properties`同样在`resources`目录

```xml
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://127.0.0.1:3306/test?characterEncoding=utf8
username=root
password=root
```

## 3. 测试是否能连接数据库

### 3.1 在`test/java`目录下创建测试文件

如果运行不产生错误，则代表连接成功

```java
import lombok.extern.slf4j.Slf4j;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.InputStream;

@Slf4j
public class MybatisTest {

        @Test
        public void test() throws IOException {
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            SqlSessionFactory sqlSessionFactory =new SqlSessionFactoryBuilder().build(inputStream);
            // 获取SqlSession对象
            SqlSession session = sqlSessionFactory.openSession();
						session.close();
        }
}
```

## 4. 实现一个简单的增删改查

### 4.1  创建与数据表相对应的类

```java
package cn.ly.generato.pojo;

public class User {
    private int id;
    private String name;
    private int age;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

### 4.2 创建操作数据库的方法

```java
package cn.ly.generato.mapper;

import cn.ly.generato.pojo.User;

import java.util.List;

public interface UserMapper {

    int delete(int id);

    int insert(User user);

    int update(User user);

    User selectUser(int id);

    List<User> selectAll();
}
```

### 4.3 创建接口中方法对应的sql语句映射文件

```xml
<!-- UserMapper -->
<?xml version="1.0" encoding="UTF-8" ?>
        <!DOCTYPE mapper
                PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
                "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="cn.ly.generato.mapper.UserMapper">
    <!-- 如果不设置名称 默认返回类型使用类的小写 -->
<select id="selectUser" resultType="user">
        select * from user where id = #{id}
</select>

<select id="selectAll" resultType="user">
    select *  from user
</select>

<insert id="insert">
    insert into user(name,age) values (#{name},#{age})
</insert>

<delete id="delete">
    delete from user where id = #{id}
</delete>

<update id="update">
    update user set name = #{name} where id = #{id}
</update>
</mapper>

```

### 4.4 目录结构

```shell
|____src
| |____test
| | |____java
| | | |____MybatisTest.java
| |____main
| | |____resources
| | | |____mybatis-config.xml
| | | |____mybatis
| | | | |____UserMapper.xml
| | | |____config.properties
| | |____java
| | | |____cn
| | | | |____ly
| | | | | |____generato
| | | | | | |____mapper
| | | | | | | |____UserMapper.java
| | | | | | |____pojo
| | | | | | | |____User.java

```

## 5 测试增删改查代码

```java
@Slf4j
public class MybatisTest {

        @Test
        public void test() throws IOException {
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            SqlSessionFactory sqlSessionFactory =new SqlSessionFactoryBuilder().build(inputStream);
            SqlSession session = sqlSessionFactory.openSession();
            UserMapper userMapper = session.getMapper(UserMapper.class);
            try {
                User user = new User();
                user.setAge(11);
                user.setName("小王");
                // 查询
//                User user = userMapper.selectUser(1);
                // 插入
//                userMapper.insert(user);
//                session.commit();
//                log.info("user;{}",user);
                // 查询所有
//                List<User> users = userMapper.selectAll();
//                for(User u:users){
//                    log.info("user: " + u);
//                }
                // 删除
//                userMapper.delete(1);
//                session.commit();
                // 修改
                user.setId(5);
                user.setName("大王");
                userMapper.update(user);
                session.commit();
            }finally {
                session.close();
            }

        }
}
```

