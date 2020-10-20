···
public class StringTest20201021
{
    void function()
    {
        String e = "";
        String greeting = "Hello";
        String s = greeting.substring(0,3); //length: 3-0 s:"Hel"
        String repeated = "Java".repeated(3);
        boolean a = "Hello".equals(greeting); // s.equals(t) 用于检测字符串s和字符串t是否相等，相等则返回true
        boolean b = "Hello".equals("hello"); //要想检测两个字符串是否相等，而不区分大小写，用equalsIgnoreCase方法
        /*为什么不能用 == 判断字符串是否相等？
        一定不要使用==运算符检测两个字符串是否相等，这个运算符只能够确定两个字符串是否存放在同一个位置上。
        当然，如果字符串在同一个位置上，它们必然相等。但是，完全有可能将内容相同的多个字符串副本放置在不同的位置上。
        *
        *
        * */

        /*空串“”是长度为0的字符串。可以调用以下代码检查一个字符串是否为空：
        if (str.length()==0)或 if (str.equals(""))
        空串是一个Java对象，有自己的串长度（0）和内容（空）。不过，String变量还可以存放一个特殊的值，名为null，表示目前没有任何对象与该变量关联。
        要检查一个字符串是否为null，要使用以下条件：
        if (str==null)
        有时要检查一个字符串既不是null也不是空串，这种情况下就需要使用以下条件：
        if (str !=null && str.length()!=0)
        首先要检查str不为null，如果在一个null值上调用方法，会出现错误。
        *
        *
        * */

        System.out.println();




    }












}
···
