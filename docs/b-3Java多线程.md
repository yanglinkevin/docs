# 1. 悲观锁，乐观锁，synchronized，volatile，CAS
- 悲观锁（Pessimistic Lock）： 
    - 每次获取数据的时候，都会担心数据被修改，所以每次获取数据的时候都会进行加锁，确保在自己使用的过程中数据不会被别人修改，使用完成后进行数据解锁。由于数据进行加锁，期间对该数据进行读写的其他线程都会进行等待。
   
    - 悲观锁比较适合写入操作比较频繁的场景，如果出现大量的读取操作，每次读取的时候都会进行加锁，这样会增加大量的锁的开销，降低了系统的吞吐量。

- 乐观锁（Optimistic Lock）： 
    - 每次获取数据的时候，都不会担心数据被修改，所以每次获取数据的时候都不会进行加锁，但是在更新数据的时候需要判断该数据是否被别人修改过。如果数据被其他线程修改，则不进行数据更新，如果数据没有被其他线程修改，则进行数据更新。由于数据没有进行加锁，期间该数据可以被其他线程进行读写操作。
    
    - 比较适合读取操作比较频繁的场景，如果出现大量的写入操作，数据发生冲突的可能性就会增大，为了保证数据的一致性，应用层需要不断的重新获取数据，这样会增加大量的查询操作，降低了系统的吞吐量。

- CAS
    - 所谓的CAS，一种乐观锁，即compareAndSwap，执行CAS操作的时候，将内存位置的值与预期原值比较，如果相匹配，那么处理器会自动将该位置值更新为新值，否则，处理器不做任何操作。  
            举个例子，内存值V、期望值A、更新值B，当V == A的时候将V更新为B。
    - CAS是原子操作
    - CAS是CPU的一个指令（需要JNI调用Native方法，才能调用CPU的指令）
    - CAS是非阻塞的、轻量级的乐观锁

- Synchronized
    - https://www.jianshu.com/p/d53bf830fa09  
    - ![](figure/synchronized.png)
    
    - synchronized关键字最主要的三种使⽤⽅式
        - 修饰实例⽅法: 作⽤于当前对象实例加锁，进⼊同步代码前要获得当前对象实例的锁
            ```java
            public class SynchronizedDemo2 {
                public synchronized void method() {
                    System.out.println("synchronized ⽅法");
                }
            }
            ```
        - 修饰静态⽅法: 也就是给当前类加锁，会作⽤于类的所有对象实例，因为静态成员不属于任何⼀
        个实例对象，是类成员（static 表明这是该类的⼀个静态资源，不管new了多少个对象，只有
        ⼀份）。所以如果⼀个线程A调⽤⼀个实例对象的⾮静态 synchronized ⽅法，⽽线程B需要调⽤
        这个实例对象所属类的静态 synchronized ⽅法，是允许的，不会发⽣互斥现象， 因为访问静态
        synchronized ⽅法占⽤的锁是当前类的锁，⽽访问⾮静态 synchronized ⽅法占⽤的锁是当前
        实例对象锁。
        
        - 修饰代码块: 指定加锁对象，对给定对象加锁，进⼊同步代码库前要获得给定对象的锁。
            ```java 
            public class SynchronizedDemo {
                public void method() {
                    synchronized (this) {
                        System.out.println("synchronized 代码块");
                    }
                }
            }
            ```