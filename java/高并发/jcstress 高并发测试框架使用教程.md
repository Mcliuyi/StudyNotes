# jcstress 高并发测试框架使用教程

## 1. 创建Maven项目

### 1.1 修改pom文件

```xml
<project xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://maven.apache.org/POM/4.0.0"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.jcstress.learning</groupId>
    <artifactId>jcstress</artifactId>
    <version>1.0</version>
    <packaging>jar</packaging>
    <name>JCStress learning sample</name>

    <!--
       This is the demo/sample template build script for building concurrency tests with JCStress.
       Edit as needed.
    -->

    <prerequisites>
        <maven>3.0</maven>
    </prerequisites>

    <dependencies>
        <dependency>
            <groupId>org.openjdk.jcstress</groupId>
            <artifactId>jcstress-core</artifactId>
            <version>${jcstress.version}</version>
        </dependency>
        <dependency>
            <groupId>org.openjdk.jcstress</groupId>
            <artifactId>jcstress-samples</artifactId>
            <version>${jcstress.version}</version>
        </dependency>
    </dependencies>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>

        <!--
            jcstress version to use with this project.
          -->
        <jcstress.version>0.5</jcstress.version>

        <!--
            Java source/target to use for compilation.
          -->
        <javac.target>8</javac.target>

        <!--
            Name of the test Uber-JAR to generate.
          -->
        <uberjar.name>jcstress-learning</uberjar.name>
    </properties>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                <configuration>
                    <compilerVersion>${javac.target}</compilerVersion>
                    <source>${javac.target}</source>
                    <target>${javac.target}</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-clean-plugin</artifactId>
                <version>3.1.0</version>
                <configuration>
                    <filesets>
                        <fileset>
                            <directory>${basedir}/results</directory>
                            <followSymlinks>false</followSymlinks>
                        </fileset>
                        <fileset>
                            <directory>${basedir}</directory>
                            <includes>
                                <include>jcstress-results*</include>
                            </includes>
                            <followSymlinks>false</followSymlinks>
                        </fileset>
                    </filesets>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.2</version>
                <executions>
                    <execution>
                        <id>main</id>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <finalName>${uberjar.name}</finalName>
                            <transformers>
                                <transformer
                                        implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <mainClass>org.openjdk.jcstress.Main</mainClass>
                                </transformer>
                                <transformer
                                        implementation="org.apache.maven.plugins.shade.resource.AppendingTransformer">
                                    <resource>META-INF/TestList</resource>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

</project>

```

## 2. 创建测试类或者使用官方Demo

### 2.1 使用官方demo

官方demo[下载地址](http://hg.openjdk.java.net/code-tools/jcstress/file/tip/jcstress-samples/src/main/java/org/openjdk/jcstress/samples), GitHub的demo[示例](https://github.com/jwoschitz/jcstress-examples)

### 2.2 自己创建测试类

```java
public class TestJMM {
		
  	// 指定使用并发测试
    @JCStressTest
    // 预测的结果与类型，附加描述信息
    @Outcome(id = {"0, 1", "1, 0", "1, 1"}, expect = ACCEPTABLE, desc = "Trivial under sequential consistency")
    @Outcome(id = "0, 0", expect = ACCEPTABLE_INTERESTING, desc = "Violates sequential consistency")
    // 标注需要测试的类
    @State
    public static class PlainExecutionOrder {
        int x, y;
        int i, j;
				
      	// 标记方法使用多线程
        @Actor
        public void actor1(II_Result r) {
            x = 1;
            r.r2 = y;
        }

        @Actor
        public void actor2(II_Result r) {
            y = 1;
            r.r1 = x;
        }

    }
}
```

## 3 打包并启动

**必须使用`mvn clean install`打包成jar包否则会缺失文件无法运行**

### 3.1 启动命令

```sh
java -XX:+UnlockDiagnosticVMOptions -XX:+WhiteBoxAPI -XX:-RestrictContended -jar target/jcstress-learning.jar -v -t TestJMM.PlainExecutionOrder
```



参考文章:

https://www.jianshu.com/p/aa0e7d0bf158

https://wiki.openjdk.java.net/display/CodeTools/jcstress

https://github.com/jwoschitz/jcstress-examples

https://github.com/jerzykrlk/jcstress-gradle-plugin

https://stackoverflow.com/questions/53458367/running-first-jcstress-test