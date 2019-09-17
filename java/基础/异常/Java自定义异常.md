# Java自定义异常

### 创建异常类

自定义异常一定要继承Java中已有的异常类，最好是相似的，这里继承的是最基本的异常类`Exception`

```java
public class MyException extends Exception {
    MyException(){
        super();
        System.out.println("myException");
    }
    MyException(String s){
        super(s);
        System.out.println("myException, 带参数的构造方法");
    }
}
```

```java
public class ExceptionTest {

    public static void Test1() throws MyException {
        System.out.println("触发异常test1");
        throw new MyException();
    }

    public static void Test2() throws MyException {
        System.out.println("触发异常test2");
        throw new MyException("触发异常test2");
    }

    public static void main(String[] args) throws MyException {

//        Test1();
        Test2();

    }

}
```

