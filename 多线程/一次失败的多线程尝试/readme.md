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
