# 1. Hashmap Hashtable ConcurrentHashMap
- HashMap和Hashtable的区别:  
    - HashMap线程不安全，Hashtable里的方法经过synchronized修饰，线程安全。
    - HashMap支持null key，Hashtable不支持。
    - HashMap默认初始化大小为16，之后每次扩容变为原来的2倍。而Hashtable初始化为11，之后每次扩容变为原来的2*n+1.
      若给定初始容量，HashMap会自动将其扩容为2的幂次方，而HashTable就用给定的。
    - HashMap链表长度大于8之后，会变为红黑树结构。以减少搜索时间。Hashtable则没有。
- HashMap的扩容怎么做的，扩容的时候又有put操作怎么办？  
https://www.cnblogs.com/yanzige/p/8392142.html 有源码
http://javastack.cn/article/2020/hashmap-21-questions/ 常见hashmap面试题  
    - 扩容必须满足两个条件：  
1、 存放新值的时候当前已有元素的个数必须大于等于阈值  
2、 存放新值的时候当前存放数据发生hash碰撞（当前key计算的hash值换算出来的数组下标位置已经存在值）  
    
    - 如果两个线程同时触发扩容，在移动节点时会导致一个链表中的2个节点相互引用，从而生成环链表.
- 如何让HashMap变成线程安全？  
Hashtable在读写数据的时候会对整个容器上锁，而ConcurrentHashMap并不需要对整个容器上锁，它只需要锁住要修改的部分就行了

- HashMap(HashSet)如何检查重复
    - 先计算hashcode，如果没有相同就直接插入，如果有相同就调用equals方法。
    - 两个对象hashcode相同不一定是相同的
    - equals被覆盖，hashcode也要被覆盖。假如我现在在开发中有一个person类，他有一些属性 如：姓名 年龄 住址。而我逻辑上需要当姓名和年龄都相同时，就认为这是同一个人，也就是同一个对象。那么肯定要重写它的equals方法。这时候不重写hashcode就会出错。
    - hashcode是内存地址计算出的值（比如内存地址取余），equals是用==来判断是否相同，也就是根据内存地址判断是不是相同对象。
    - hashcode只生成一个hash值，速度较快，而equals是全面复杂的比较，效率较慢。
    - 不同对象生成的hashcode可能是一样的，并不是绝对可靠的。所以需要equals来比较两个对象是不是完全的。
    
- 为什么HashMap扩容要变为原来的2倍，并且初始时候是16，如果不是还要变成2的幂次。
    - Hash散列值的范围值-2147483648到2147483647，求出hash值之后，要对数组长度进行取余，余数才对应数组的小标，也就是要存的位置。
    - hash%length == hash&(length-1)的前提是 length 是2的n 次⽅。 所以二次方是为了计算取余更快，变成位的与操作。
    
- ConcurrentHashMap 和 HashMap ，HashTable的区别
    - ConcurrentHashMap底层数据结构和HashMap一样，数组+链表+红黑树。
    - ConcurrentHashMap实现线程安全方式：
        - HashTable在实例方法上加了锁，所以put的时候，其他线程put，get会阻塞住，因为修饰实例方法，相当于是给整个对象上了锁。
        - 在JDK1.7的时候，ConcurrentHashMap用分段锁，一把锁只锁容器一部分数据，多线程访问不同数据段的数据，不会存在锁竞争，提高了并发效率。
        - JDK1.8之后，⽤ Node 数组+链表+红⿊树的数据结构来实现，并发控制使⽤ synchronized 和CAS 来操作。
            - ConcurrentHashMap保证线程安全主要有三个地方。
            - 使用volatile保证当Node中的值变化时对于其他线程是可见的。
            - 使用table数组的头结点作为synchronized的锁来保证写操作的安全
            - 当头结点为null时，使用CAS操作来保证数据能正确的写入。

            - ![](figure/ConcurrentHashMap.jpg)


# 2. ArrayList, LinkedList, Vector

# 3. HashMap, Hashtable, ConcurrentHashMap

# 4. comparable, comparator
- comparator定制排序，重写compare方法，实际还是调用compareTo
```java
Collections.sort(arrayList, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2.compareTo(o1);
            }
        });
```

- 继承comparable接口，重写compareTo方法    代码可见javaCode

- 自定义排序，比如 treeMap.put()的时候，put对象（比如Person()）的话，就是需要继承Comparable接口重写compareTo方法的，不然这个红黑树没法去排序。 而String Integer内部已经继承了comparable接口，所以不需要重写。
