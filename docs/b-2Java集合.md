# 1. Hashmap
1. hashmap的扩容怎么做的，扩容的时候又有put操作怎么办？  
https://www.cnblogs.com/yanzige/p/8392142.html 有源码
http://javastack.cn/article/2020/hashmap-21-questions/ 常见hashmap面试题
- 扩容必须满足两个条件：  
1、 存放新值的时候当前已有元素的个数必须大于等于阈值  
2、 存放新值的时候当前存放数据发生hash碰撞（当前key计算的hash值换算出来的数组下标位置已经存在值）  
>>如果两个线程同时触发扩容，在移动节点时会导致一个链表中的2个节点相互引用，从而生成环链表.
- 如果让hashmap变成线程安全？  
Hashtable在读写数据的时候会对整个容器上锁，而ConcurrentHashMap并不需要对整个容器上锁，它只需要锁住要修改的部分就行了