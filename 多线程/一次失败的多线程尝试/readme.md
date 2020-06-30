一次失败的多线程尝试
=========================
```
import org.apache.commons.io.FileUtils;
import org.apache.commons.io.filefilter.FileFilterUtils;
import java.io.File;
import java.io.IOException;
import java.net.URL;
public class ThreadTest extends Thread
{
        private static String url;
        private static String name;
        public ThreadTest(String url,String name)
        {
                this.url = url;
                this.name = name ;
        }
        @Override
        public void run()
        {
                WebDownLoader webDownLoader = new WebDownLoader();
                webDownLoader.downloader(url,name);
                System.out.println("File downloaded"+"  "+name);
        }
        public static void main(String[] args) {
                ThreadTest threadTest1 = new ThreadTest(url="http://attach.bbs.miui.com/forum/201105/17/113554rnu40q7nbgnn3lgq.jpg",name="1.jpg");
                ThreadTest threadTest2 = new ThreadTest(url="http://e.hiphotos.baidu.com/zhidao/pic/item/b64543a98226cffc7a951157b8014a90f703ea9c.jpg",name="2.jpg");
                ThreadTest threadTest3 = new ThreadTest(url="http://attach.bbs.miui.com/forum/201111/21/205700txzuacubbcy91u99.jpg",name="3.jpg");
                threadTest1.start();
                threadTest2.start();
                threadTest3.start();
        }
}
class WebDownLoader
{
        public void downloader(String url,String name)
        {
                try
                {
                        FileUtils.copyURLToFile(new URL(url),new File(name));
                }
                catch (IOException e)
                {
                        e.printStackTrace();
                        System.out.println("IO something wrong,downloader");
                }
        }
}
```

##   从一次尝试看多线程实现流程

&#8195;&#8195;&#8195;暂且把包含主要结构和main函数的类称为主类，把存放具体实现方法的类称为工具类。

&#8195;&#8195;&#8195;主类可以通过继承Thread类来实现多线程，继承后必须要对run()进行重写，在run()中写入想要多线程进行的操作，如本例中在run()内实例化工具类WebDownLoader，并调用其中的downloader方法。主类中在main()中实例化本类，并调用对象下的start()方法，这个start()方法会使得run()中提前写入的操作运行。

&#8195;&#8195;&#8195;深入解释：Thread.java类中的start()方法通知“线程规划器”此线程已经准备就绪，等待调用线程对象的run()方法。这个过程其实就是让系统安排一个时间来调用Thread中的run()方法，也就是使线程得到运行，启动线程，具有异步执行的效果。如果调用代码thread.run()就不是异步执行了，而是同步，那么此线程对象并不交给“线程规划器”来进行处理，而是由main主线程来调用run()方法，也就是必须等run()方法中的代码执行完后才可以执行后面的代码。

&#8195;&#8195;&#8195;上述文字可用于思考多线程的原理问题，也可以用于回答start()方法和run()方法的区别问题。结合《从操作系统到线程与进程》一文，可以推断，上述的线程规划器，其实就是操作系统内的调度器。这一推断不知是否正确，仅仅是作者本人的思考结果。
