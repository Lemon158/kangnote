#### 1、继承Thread类创建线程
在Java里面，开发者可以创建线程，这样在程序执行的过程中，如果CPU空闲了，就会执行线程中的内容

>Java是单继承，资源宝贵，要用接口方式

#### 2、步骤
1、自定义一个类，继承java.lang包下的Thread类
2、重写run方法
3、将要在线程中执行的代码编写 在run方法中
4、创建自定义类对象
5、使用start方法启动线程

```java
/**
 * 多线程实现的第一种方法，继承Thread 
 *
 */

//1.自定义一个类，继承java.lang包下的Thread类
class MyThread extends Thread {
    //2.重写run方法
    public void run() {        
        //3.将要在线程中执行的代码编写在run方法中
        for(int i = 0; i < 1000; i++) {        
            System.out.println("monkey");
        }
    }
}

public class ThreadTest01 extends Thread {

    public static void main(String[] args) {
        //4.创建上面自定义类的对象
        //创建一个线程
        MyThread mt = new MyThread();        

        //5.调用start方法启动线程
        mt.start();                            

        //将循环的次数设置多一些，否则还没等到CPU切换就已经打印完成了
        for(int i = 0; i < 1000; i++) {
            System.out.println("1024");
        }
    }

}
```

