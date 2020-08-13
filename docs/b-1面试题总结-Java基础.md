# 1.Java String类为什么是final的？

1. 为了实现字符串池
2. 为了线程安全
3. 为了实现String可以创建HashCode不可变性

首先你要理解final的用途，在分析String为什么要用final修饰，final可以修饰类，方法和变量，并且被修饰的类或方法，被final修饰的类不能被继承，即它不能拥有自己的子类，被final修饰的方法不能被重写， final修饰的变量，无论是类属性、对象属性、形参还是局部变量，都需要进行初始化操作。
https://www.jianshu.com/p/9c7f5daac283