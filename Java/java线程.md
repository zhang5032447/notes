### java 线程3中方法

类`Thread`，接口`Runnable`，接口`Callable`

特点：

1. `Thread`本质上是实现了`Runnable`接口

2. `Callable`可以获取返回值和抛出异常

   ```java
   RunnableDemo runnableDemo = new RunnableDemo();
   Thread thread = new Thread(runnableDemo);
   thread.start();
   
   ExecutorService executorService = Executors.newFixedThreadPool(1);
   Future<String> future = executorService.submit(new CallableDemo());
   // future.get() 阻塞
   System.out.println(future.get());
   ```

   

生命周期：

1. NEW: 初始状态，线程被构建，但是还是没有用调用start方法

2. RUNNABLED: 运行状态，JAVA线程把操作系统中的就绪和运行两种状态统一称为“运行中”。

3. BLOCKED: 阻塞状态，表示线程进入等待状态，也就是线程因为某种原因放弃了CPU使用权，阻塞也分为几种情况。

4. WAITING: 等待状态

5. TIME_WAITING: 超时等待状态，超时以后自动返回。

6. TERMINATED: 终止状态，表示当前线程执行完毕。

   

### 线程使用

Thread.join()：保证线程执行的可见性.

Thread.interrupt() 中断阻塞状态 （sleep，wait，join）

Thread.interrupted() 中断标识复位

```java
public class InterruptDemo {
    private static int i;
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {
            try {
                Thread.sleep(1000);
                InterruptDemo.class.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
                Thread.interrupted();
            }
//            while (!Thread.currentThread().isInterrupted()) {i++;}
        });
        thread.start();
        thread.interrupt();
    }
}
```









