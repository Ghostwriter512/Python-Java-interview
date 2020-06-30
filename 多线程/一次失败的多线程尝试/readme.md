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


