实例变量与线程安全
============================

···

public class MyThread extends Thread 
{
    private int count = 5;
    public MyThread(String name)
    {
        super();// Father class's initilization
        this.setName(name); // Set thread's name
    }
    @Override
    public void run()
    {
        super.run();
        while (count>0)
        {
            count--;
            Sout(this.currentThread().getName()+'  '+count); 
        }
    }
}

public class Run
{
    public static void main(String[] args)
    {
        MyThread a = new MyThread("A");  //Initialization
        MyThread b = new MyThread("B");
        MyThread c = new MyThread("C");
        a.start();
        b.start();
        c.start();
    }
}

···




