#### 1、与Runnable接口对比
```
 创建新类MyThread实现runnable接口
class MyThread implements Runnable{
 @Override
 public void run() {
 
 }
}
新类MyThread2实现callable接口
class MyThread2 implements Callable<Integer>{
 @Override
 public Integer call() throws Exception {
  return 200;
 } 
}
 面试题:callable接口与runnable接口的区别？
 
 答: （1）是否有返回值
       （2）是否抛异常
       （3）落地方法(重写方法)不一样，一个是run，一个是call

Runnable是java.lang包
Callable是java.util.concurrent包(JUC)下的接口
```
#### 2、使用
可知，Thread中的构造方法并没有Callable，所以直接替换Runnable是行不通的。
```
//错误行为
new Thread(new MyThread2(),"aa");
```
 可以寻找中间人，例如已知B认识A跟C，此时如果A想认识C，那么A只需要找B，则可以实现认识C，B就充当中间人 的角色，就有点像Java多态，并且一个类中可以实现多个接口

查看Runnable的API
![](https://upload-images.jianshu.io/upload_images/20318144-9341ad5ac14e8134.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
可知FutureTask实现了Runnable接口

查看FutureTask构造方法
![](https://upload-images.jianshu.io/upload_images/20318144-489a8488f4325ae7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
此时就可以进行使用
```
//实现方式
FutureTask<Integer> ft = new FutureTask<Integer>(new MyThread2());
new Thread(ft,"aa").start();
//获取返回值
ft.get();
```
 #### 3、代码
```
class MyThreadCallable implements Callable<Integer>{
    @Override
    public Integer call() throws Exception {
        TimeUnit.SECONDS.sleep(4);
        System.out.println(Thread.currentThread().getName()+ "===>come in callable");
        return 200;
    }
}
public class ThreadTest03 {
    public static void main(String[] args)throws Exception {
        Callable callable = new MyThreadCallable();
        FutureTask<Integer> futureTask = new FutureTask<>(callable);
        Thread thread = new Thread(futureTask,"AAA");
        thread.start();
        //isDone返回true则表示任务完成
        while (!futureTask.isDone()){
            System.out.println("Please wait....");
        }
        System.out.println(futureTask.get());
//        if (!futureTask.isDone()){
//            System.out.println("Please wait....");
//        }else {
//            System.out.println(futureTask.get());
//        }
        System.out.println(Thread.currentThread().getName());
    }
}
```
小节：
在主线程中需要执行比较耗时的操作时，但又不想阻塞主线程时，可以把这些作业交给Future对象在后台完成，
当主线程将来需要时，就可以通过Future对象获得后台作业的计算结果或者执行状态。

一般FutureTask多用于耗时的计算，主线程可以在完成自己的任务后，再去获取结果。

仅在计算完成时才能检索结果；如果计算尚未完成，则阻塞 get 方法。一旦计算完成，
就不能再重新开始或取消计算。get方法而获取结果只有在计算完成时获取，否则会一直阻塞直到任务转入完成状态，
然后会返回结果或者抛出异常。 

只计算一次
get方法放到最后

 
