# 1.Java String类为什么是final的？

1. 为了实现字符串池
2. 为了线程安全
3. 为了实现String可以创建HashCode不可变性

首先你要理解final的用途，在分析String为什么要用final修饰，final可以修饰类，方法和变量，并且被修饰的类或方法，被final修饰的类不能被继承，即它不能拥有自己的子类，被final修饰的方法不能被重写， final修饰的变量，无论是类属性、对象属性、形参还是局部变量，都需要进行初始化操作。
https://www.jianshu.com/p/9c7f5daac283

# 2. 深浅拷贝？
- 浅拷贝：只复制当前对象，对该对象内部的引用不能复制。

- 深拷贝：对对象内部所有对象的引用均复制，每个引用对象创建一个实例并复制实例。

-  A 和对象 B，二者都是 ClassC 的对象，具有成员变量 a 和 b，现在对对象 A 进行拷贝赋值给 B，也就是 B.a = A.a; B.b = A.b;
    - 假设 a 是基础数据类型，b 是引用类型。
    
    - 这个时候改a没问题，改B.b的话那么A.b也变了，因为是浅拷贝。

- 浅拷贝实现 Cloneable 接口，并覆写 clone() 方法
- 深拷贝每个对象都需要实现 Cloneable 并重写 clone() 方法
- https://www.jianshu.com/p/94dbef2de298