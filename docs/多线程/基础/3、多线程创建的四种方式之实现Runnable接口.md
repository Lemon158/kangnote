#### 1、实现Runnable接口创建线程
步骤
1、自定义一个类实现java.lang包下的Runnable接口
2、重写run方法
3、将要在线程中执行的代码编写在run方法中
4、创建自定义类对象
5、创建Thread对象并将自定义对象作为参数传递给Thread的构造方法中
6、调用start方法启动线程
```java
/**
 * 多线程实现的第二种方法，实现Runnable接口
 *
 */

// 1.自定义一个类实现java.lang包下的Runnable接口
class MyRunnable implements Runnable {

    // 2.重写run方法
    @Override
    public void run() {
        // 3.将要在线程中执行的代码编写在run方法中
        for (int i = 0; i < 1000; i++) {
            System.out.println("实现Runnable");
        }
    }

}

public class ThreadTest02 {

    public static void main(String[] args) {
        // 4.创建上面自定义类的对象
        MyRunnable mr = new MyRunnable();

        // 5.创建Thread对象并将上面自定义类的对象作为参数传递给Thread的构造方法
        Thread t = new Thread(mr); 

        //6.调用start方法启动线程
        t.start();

        for (int i = 0; i < 1000; i++) {
            System.out.println("主方法");
        }
    }

}
```