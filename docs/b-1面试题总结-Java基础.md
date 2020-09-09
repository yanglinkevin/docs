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

# 3. == 与 equals(重要)
- ==判断的是两个对象地址是不是相等，也就是判断两个对象是不是同一个。

- equals在没有覆盖的情况下，等价于==
- 覆盖了equals方法，一般就是重写看内容相等不。

# 4. StringBuffer和StringBuilder, String
- String有final修饰，不可变
- StringBuffer和StringBuilder可变。

- StringBuffer对方法加锁了，线程安全， StringBuider没有加锁，非线程安全。
- 对String类型进行改变时，每次都会生成一个新的String对象，然后将指针指向新的String对象。 而StringBuffer和StringBuilder都是对对象本身进行操作。

# 5. 成员变量， 局部变量
- 成员变量
    - 全局变量 无static修饰的话 就是实例变量， 只要对象被当作引用，实例变量就将存在
    
    - 静态变量 有static修饰 就是类变量。其生命周期取决于类的生命周期。类被垃圾回收机制彻底回收时才会被销毁

        ```java 
        public class DataClass {
            String name; // 成员变量、实例变量
            int age; // 成员变量、实例变量
            static final String website = "C语言中文网"; // 成员变量、静态变量(类变量)
            static String URL = "http://c.biancheng.net"; // 成员变量、静态变量(类变量)
        }
        ```
- 局部变量是指在方法或者方法代码块中定义的变量，其作用域是其所在的代码块。可分为以下三种：
    - 方法参数变量（形参）：在整个方法内有效。
    - 方法局部变量（方法内定义）： 从定义这个变量开始到方法结束这一段时间内有效。
    
    - 代码块局部变量（代码块内定义）：从定义这个变量开始到代码块结束这一段时间内有效。
    - 局部变量在使用前必须被程序员主动初始化值。
        ```java 
            public class Test2 {
            public static void main(String[] args) {
                int a = 7;
                if (5 > 3) {
                    int s = 3; // 声明一个 int 类型的局部变量
                    System.out.println("s=" + s);
                    System.out.println("a=" + a);
                }
                System.out.println("a=" + a);
                }
            }
        ```
    - 上述实例中定义了 a 和 s 两个局部变星，其中 int 类型的 a 的作用域是整个 main() 方法，而 int 类型的变量 s 的作用域是 if 语句的代码块内.

    - 作为方法参数声明的变量的作用域是整个方法。
    
