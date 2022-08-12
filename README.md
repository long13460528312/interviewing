# interviewing
#redis面试题集锦
Redis是单线程还是多线程：
    在Redis4.0版本之前Redis是单线程模型的，这里的单线程并不是指Redis中只有一个线程在工作，而是说在进行set与get操作时是有一个线程完成的，而Redis的持久化、集群同步等还是有其他线程完成。
   
那么为什么单线程还是那么快：
    1、因为Redis本身是存储在内存中的，而内存本身的执行效率就比较快。 2、因为使用的是单线程所以不用担心死锁问题，也节省了线程切换的时间
Redis是如何保证数据不丢失的：
    Redis是存储在内存中的，要保证其中数据不丢失那么就要将其数据存储到磁盘中，存储的方式有AOF和RDB两种。AOF是写后日志的方式，Redis现将数据写入内存中，然后再记录操作命令存储到磁盘中，如果需要恢复时，就需要讲磁盘中的日志文件所有的命令在执行一遍。写后日志可能会导致部分命令丢失，导致恢复后部分数据数据丢失。RDB是采用快照的方式，每隔一定的时间间隔，将Redis中的数据记录下来存储到磁盘中，故障恢复只需要将RDB文件读入内存中即可。

Redis如何实现高可用：
    三种方式：主从复制、哨兵模式、集群。主从复制是指将主Redis服务器同步数据到多个从服务器上，这样读Redis中的数据就可以从从服务器上读取，减轻主服务器压力，但是写数据到Redis还是只能通过主服务器进行。  哨兵模式：监控主从服务器，提供自动容灾恢复的功能，比如主服务器宕机后，会选举从服务器作为主服务器。  集群：部署多个主从服务器，将数据分布在不同的服务器上。主要是为了提升Redis的写入能力。






#Java基础面试集锦：
简单介绍一下Java：java是一门开源的、可移植性高、面向对象开发的一门编程语言。他有三大特点：封装：将对象的属性以及方法封装在一起，只对外暴露部分属性及方法，能够实现高内聚，低耦合。   继承 ：使用已存在类的定义作为基础创建新的类，子类继承父类的属性以及方法，提高代码的复用性。 多态：引用的类型在编译期不确定，在运行期才确定，子类引用指向父类对象，可以通过同一个父类对象调用不同的子类中被重写的方法，实现不同的功能。

基本数据类：bite 1位 8字节、int 4位 32字节、short 2位、long 8位、char 2位、布尔 1字节、float4位、double8位

接口与抽象类的区别：1、接口中不能有具体的方法实现，抽象类中可以。2、接口可以被多实现，抽象类只能被单继承。3、接口中的修饰符只能是public和默认，抽象类中可以有前三种。4、接口中基本数据类型用public static final 修饰，并且需要给初始值，抽象类不是。

重载与重写：重载发生在同一个类中，方法名相同，参数不同，返回类型可以相同，抛出异常的范围可以大于重载的方法。重写发生在子父类中，方法名相同，参数列表相同，返回值类型相同，抛出异常的范围需要小于被重写的方法所抛出异常的范围。

ArrayList与linkList的区别：数据结构：ArrayList本质上是数组，LinkList本质上是双链表。ArrayList查找速度快，插入速率慢，linkList插入快，查询慢。占用空间：linkList比ArrayList占用的空间小，因为ArrayList是提前预留空间进行存储。

hashmap1.7与1.8的区别：最大的区别就是数据结构发生了改变，1.7是采用数组加链表的方式存储，1.8是采用数组加链表加红黑树，当链表的长度超过8就会采用红黑树进行存储数据。插入数据的方式：1.7使用的是头插法，1.8使用的是尾插法。扩容方式：1.7插入前扩容，1.8插入后扩容。

hashset的存储原理：底层存储原理是HashMap，通过HashMap中的key进行存储数据，所以不会重复。当数据要存储进来时，先计算改值的hash值，如果有hash值相同的数时，通过equals方法进行判断，返回为true则两个值相同，为false，则不同，都存储到链表中，当链表长度超过8后存储到红黑树中。

什么是泛型：泛型是指在编译期的时候类型不确定，当创建对象是才确定类型。

进程与线程的区别：进程是系统资源分配与调度的基本单位，线程是进程中运行的基本单位
简述一下单例模式：单例模式分为懒汉式和饿汉式，懒汉式就是在类加载时不创建对象，只有在第一次创建对象时创建唯一的对象，饿汉式是指在类加载时就直接创建出对象来。

保证线程安全：加锁，sy   和lock锁，sy可以加在代码块，方法上
多线程创建的方式：继承thread类，实现runnable接口，从线程池中取。
线程池中有哪些重要的参数：线程最大数最小数，策略模式、
四种引用类型：强，软、弱、虚引用：强引用，只有在引用类型为空时，才会被回收，软引用：当内存足够时，不会被回收，当内存不足是，系统会回收此对象，弱引用：无论内存是否充足，只要JVM开始进行垃圾回收，此对象就会被回收，虚引用：就像没有任何引用一样，随时可能被回收。
深拷贝和浅拷贝的区别：对于引用类型，浅拷贝是复制了一个引用对象的地址，拷贝对象和被拷贝对象指向同一块地址，修改会同时改变，深拷贝是重新创建一块地址并复制对象内容放入其中，不会同步修改。



