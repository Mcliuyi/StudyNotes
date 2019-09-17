# Java线程使用

## 创建线程

### Thread类

```java
Thread t = new Thread(obj);
t.start();
```

### ExecutorService类

```java
ExecutorService exec = Executors.newCachedThreadPool(); //创建线程池但没有限制
for(int i=0;i<5;i++){
  	exec.execute(Obj); //传入对象
}
exec.shutdown(); //等待线程完成后结束所有线程
```

```java
ExecutorService exec = Executors.newFixedThreadPool(5); //创建线程池,数量为5
        for(int i=0;i<5;i++){
            exec.execute(Obj;
        }
       exec.shutdown();
```

### 带返回值线程Callable接口

```java
class TaskWithResult implements Callable {

    private int id;

    TaskWithResult(int id){
        this.id = id;
    }


    @Override
    public String call() throws Exception {
        // 线程的返回值
        return "result of TaskWithResult " + id;
    }
}

public class CallableDemo{
    public static void main(String[] args){

        ExecutorService executorService = Executors.newCachedThreadPool();
        ArrayList<Future<String>> resluts = new ArrayList<Future<String>>();
        //Future<?>表示获取线程的结果，通过get获取
        for(int i=0;i<10;i++){
            resluts.add(executorService.submit(new TaskWithResult(i))); //必须使用submit进行提交
        }
        for(Future<String> fs : resluts){
            try {
                System.out.println(fs.get());
            }catch (Exception e){
                System.out.println(e);
            }finally {
                executorService.shutdown();
            }
        }

    }

}
```

### 设置优先级setPriority(int priority)/getPriority()

```java
class TaskWith implements Runnable {

    private int id;

    TaskWith(int id){
        this.id = id;
    }

    @Override
    public void run() {
        //设置现场的优先级
        Thread.currentThread().setPriority(id);

    }
}
```

