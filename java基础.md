# java基础面试题

## 面向对象的特征有哪些方面
**封装**:安全性，把数据和操作数据的方法绑定起来，对数据的访问只能通过已经定义的接口
**继承**:子类继承父类的特征和行为，使得子类对象具有父类的属性和方法
**多态**:接口的多种不同的实现方式即为多态，多态性是向不同的对象发送同一条消息，不同的对象在接受时会产生不同的行为。
**抽象** 将一类对象的共同特征总结出来

## 基本的数据类型

8种，byte、short、int、long、float、double、char、boolean，其余都是引用数据类型

例如：class 声明、interface 声明、数组、枚举

## switch可以使用的数据类型

int,string,byte,enum枚举
浮点型都不可以

## String、StringBuilder和StringBuffer的区别？
String是只读字符串，内容不能被更改。StringBuffer和StringBuilder可以修改内容。StringBuffer是线程安全的，内部的方法有synchronized

## 重载（Overload）和重写（Override）的区别。重载的方法能否根据返回类型进行区分？
重载和重写都是实现多态的方式，区别在于前者实现的是编译时的多样性，而后者是实现运行时的多样性。重载发生在一个类中，同名的方法有不同的参数列表；重写发生在子类与父类之间，子类不能比父类被重写的方法声明更多的异常（里氏代换原则）


## 描述一下 JVM 加载 class 文件的原理机制？
类加载的过程：装载（通过类加载器）、链接和初始化
1. **装载**：查找并且加载类的二进制数据
2. **链接**:
    1. 验证：确保被加载类的正确性
    2. 准备：为类的静态变量分配内存，并将其初始化为默认值
    3. 解析：把类中的符号转化为直接引用
3. **初始化**：为类的静态变量赋予正确的初始值

### 类加载器
1. java虚拟机自带的加载器
    1. 根类加载器（Bootstrap）：使用C++编写，程序员无法再java代码中获得该类
    2. 扩展类加载器（Extension）：使用java代码实现、系统类加载器（System）：使用java代码实现。
2.  用户自定义的类加载器
    java.lang.ClassLoader的子类，用户可以定制类的加载方式

### 类的初始化
类什么时候被初始化
1. 创建类的实例，就是new一个对象
2. 访问某个类或接口的静态变量，或者对该静态变量赋值
3. 调用类的静态方法
4. 反射(Class.forName('权限定类名'))
5. 初始化一个类的子类（会先初始化子类的父类）
6. jvm启动时表明的启动类，即文件名和类目相同的那个类

## 抽象类（abstract class）和接口（interface）有什么异同？
1. 声明方式：class、interface
2. 属性：抽象类可以有普通属性，接口都是常量(public static final String NAME="xxx")
3. 抽象类可以有抽象方法和普通方法，接口默认都是抽象方法（jdk1.8有默认方法实现default修饰，静态方法static修饰）
4. 构造方法：抽象类有构造方法，接口没有
5. 抽象类和接口都不能够实列化，但可以定义抽象类和接口类型的引用。
6. 数量关系: 一个类可以继承extends一个父类，实现implements多个接口

## GC 是什么？为什么要有 GC？
垃圾回收站，内存处理是编程人员容易出现问题的地方，忘记或者错误的内存回收会导致程序或系统的不稳定甚至崩溃，Java 提供的 GC 功能可以自动监测对象是否超过作用域从而达到自动回收内存的目的，Java 语言没有提供释放已分配内存的显示操作方法。

## 接口是否可继承（extends）接口？抽象类是否可实现（implements）接口？抽象类是否可继承具体类（concreteclass）？
接口可以继承接口，而且支持多重继承。抽象类可以实现接口抽象类可以继承具体类，也可以及继承抽象类

## Java 中的 final 关键字有哪些用法？
1. 修饰类，表示该类不能被继承
2. 修饰方法，表示该方法不能被重写
3. 修饰变量，表示只能一次赋值后不能被更改（常量）

## Error 和 Exception 有什么区别？
Error表示系统级的错误和程序不必处理的异常，回复很困难的严重问题；比如内存溢出；Exception表示需要捕捉或者需要程序进行处理的异常，是一种设计或实现问题。如果程序正确运行，不会出现Exception。

## Java 语言如何进行异常处理，关键字：throws、throw、try、catch、finally 分别如何使用？
在java中，每一个异常都是一个对象，它是Throwable类或其他子类的实列。当一个方法出现异常后便抛出一个异常对象，该对象包含异常信息，调用这个对象的方法可以捕捉这个异常并处理。

一般情况下用try来执行一段程序，如果出现异常，系统会抛出（throws）一个异常，这时候可以用catch捕捉它，或最后（finally）由缺省处理器来处理。

try用来指定一块预防所有‘异常’的程序，catch 子句紧跟在try 块后面，用来指定你想要捕捉的“异常”的类型；throw 语句用来明确地抛出一个“异常”；throws 用来标明一个成员函数可能抛出的各种“异常”；Finally 为确保一段代码不管发生什么“异常”都被执行一段代码；

throws是用来声明一个方法可能抛出的所有异常信息，throws是将异常声明但是不处理，而是将异常往上传，谁调用我就交给谁处理。而throw则是指抛出的一个具体的异常类型。

throw：就是自己进行异常处理，处理的时候有两种方式，要么自己捕获异常（也就是try catch进行捕捉），要么声明抛出一个异常（就是throws 异常~~）。

注意：
throw一旦进入被执行，程序立即会转入异常处理阶段，后面的语句就不再执行，而且所在的方法不再返回有意义的值！

## 列出一些你常见的运行时异常？？
ArithmeticException（算术异常）
ClassCastException （类转换异常）
IllegalArgumentException （非法参数异常）
IndexOutOfBoundsException （下标越界异常）
NullPointerException （空指针异常）NPE 行话，黑话
SecurityException （安全异常）
StackOverflowError （堆栈溢出异常）

## 阐述 final、finally、finalize 的区别
final：修饰符（关键字）有三种用法：如果一个类被声明为 final，意味着它不能再派生出新的子类，即不能被继承，因此它和 abstract 是反义词。将变量声明为 final，可以保证它们在使用中不被改变，被声明为 final 的变量必须在声明时给定初值，而在以后的引用中只能读取不可修改。被声明为 final 的方法也同样只能使用，不能在子类中被重写。

finally：通常放在 try…catch…的后面构造总是执行代码块，这就意味着程序无论正常执行还是发生异常，这里的代码只要 JVM 不关闭都能执行，可以将释放外部资源的代码写在 finally 块中。极端的情况： System.exit(0);

finalize：Object 类中定义的方法，Java 中允许使用 finalize()方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由**垃圾收集器在销毁对象时调用的**，通过重写 finalize()方法可以整理系统资源或者执行其他清理工作。

## List、Set、Map 是否继承自 Collection 接口？
ist、Set 是，Map 不是。Map 是键值对映射容器，与 List 和 Set 有明显的区别， 而 Set 存储的零散的元素且不允许有重复元素（数学中的集合也是如此），List是线性结构的容器，适用于按数值索引访问元素的情形。List和Set是单列集合，Map双列集合。

## 阐述 ArrayList、Vector、LinkedList 的存储性能和特性。
ArrayList 和 Vector 都是使用**数组**方式存储数据，它们都允许直接按序号索引元素，但是插入元素要涉及数组元素移动等内存操作，所以**索引数据快而插入数据慢**，Vector 中的方法由于添加了 synchronized 修饰，因此 **Vector 是线程安全的容器**，但性能上较ArrayList 差，因此已经是 Java 中的遗留容器。

LinkedList 使用双向链表实现存储,按序号索引数据需要进行前向或后向遍历，但是插入数据时只需要记录本项的前后项即可，所以插入速度较快。

ArrayList 和 LinkedListed 都是非线程安全的，如果遇到多个线程操作同一个容器的场景，则可以通过工具类Collections 中的 synchronizedList 方法将其转换成线程安全的容器后再使用（这是对装潢模式的应用，将已有对象传入另一个类的构造器中创建新的对象来增强实现）。

### 线程安全的集合类

老的集合类：Vector、Hashtable
新的集合类：CopyOnWriteArrayList、CopyOnWriteArraySet、ConcurrentHashMap
Copyonwrite：写时复制,使用的Lock接口的实现类，加锁和释放锁的方法
ConcurrentHashMap：是通过synchronized同步代码块实现的线程安全
Hashtable：是通过synchronized同步方法实现线程安全的

## Collection 和 Collections 的区别？
Collection 是一个接口，它是 Set、List 等容器的父接口；
Collections 是个一个工具类，提供了一系列的静态方法来辅助容器操作，这些方法包括对容器的搜索、排序、线程安全化等等。 

## 创建线程有几种方式？
1. 继承Thread类
2. 实现Runnable接口
3. 实现Callable接口
4. 线程池

## 线程的 sleep()方法和 yield()方法有什么区别？
1. sleep()方法给其他线程运行机会时不考虑线程的优先级，因此会给低优先级的线程以运行的机会；yield()方法只会给相同优先级或更高优先级的线程以运行的机会；
2. 线程执行 sleep()方法后转入阻塞（blocked）状态，而执行 yield()方法后转入就绪（ready）状态；
3. sleep()方法声明抛出 InterruptedException，而 yield()方法没有声明任何异常；
4. sleep()方法比 yield()方法（跟操作系统 CPU 调度相关）具有更好的可移植性。

## 当一个线程进入一个对象的 synchronized 方法 A 之后，其它线程是否可进入此对象的 synchronized 方法 B？
不能。其它线程只能访问该对象的非同步方法，同步方法则不能进入。因为非静态方法上的 synchronized 修饰符要求执行方法时要获得对象的锁，如果已经进入 A 方法说明对象锁已经被取走，那么试图进入 B 方法的线程就只能在等锁池（注意不是等待池哦）中等待对象的锁。

## 多线程应用的场景
1. 常见的浏览器、web服务、web处理请求，各种专用服务器
2. servlet多线程
3. FTP下载、多线程操作文件
4. 数据库连接池用到的多线程
5. 分布式计算
6. tomcat内部采用多线程
7. 后台任务：如定时向大量(100W以上)的用户发送邮件；定期更新配置文件、任务调度(如quartz)，一些监控用于定期信息采集
8. 自动作业处理：比如定期备份日志、定期备份数据库
9. 异步处理：如发微博、记录日志
10. 页面异步处理：比如大批量数据的核对工作(有10万个手机号码，核对哪些是已有用户)
11. 数据库的数据分析(待分析的数据太多)，数据迁移
12. 多步骤的任务处理，可根据步骤特征选用不同个数和特征的线程来协作处理，多任务的分割，由一个主线程分割给多个线程完成
13. desktop应用开发，一个费时的计算开个线程，前台加个进度条显示
14. swing编程


## 线程的基本状态以及状态之间的关系？
线程有五个状态:
1. new创建状态
2. Runnable就绪状态
3. Running运行状态
4. Dead消亡状态
5. Blocked阻塞状态。

创建线程通过start方法进入就绪状态，获取cpu的执行权进入运行状态，失去cpu执行权会回到就绪状态，运行状态完成进入消亡状态，运行状态通过sleep方法和wait方法进入阻塞状态，休眠结束或者通过notify方法或者notifyAll方法释放锁进入就绪状态

## 阐述 JDBC 操作数据库的步骤
1. 加载驱动
2. 获取连接 DriverManager.getConnection()
3. 编写SQL语句  String sql = “s”
4. 创建Statement对象 Statement stmt = conn.createStatement
5. 执行语句  stmt.executeUpdate
6. 结果处理  while(rs.next())
7. 释放资源：关闭连接  conn.close()

## java的集合框架
Collection：单列集合，存储的数据时单个数据
Map：Map时双列集合，存储数据的时候时key---value
List的实现类：ArrayList，LinkedList 不是线程安全的，遍历方式，下标遍历和迭代器
Set的实现类：HashSet、TreeSet 不是线程安全的，通过迭代器遍历

## ArrayList、LinkedList区别
1. 数据结构实现：ArrayList是动态数据，LinkedList是基于双向列表随机访问，随机访问ArrayList效率更高，因为是数组。
2. 增加和删除效率：LinkedList比ArrayList效率更高，LinkedList效率更高
3. 线程安全问题：都不是线程安全的

## 为什么需要线程池？
创建对象和销毁对象是非常耗时的，所以就想到可以重复使用一个对象，而不是用一次创建一次；数据库的连接池也是同理，创建一个连接非常耗时的，TCP三次握手四次挥手等。为了重复利用一个Connection，引入连接池的概念。可以重复利用Connection对象。线程也是同样的道理: 重复利用一个线程，引入线程池的概念。


## 线程同步有几种方法？

### 同步方法
synchronized关键字修饰方法。由于java的每个对象都有一个内置锁，当用此关键字修饰方法时，内置锁会保护整个方法。在调用该方法前，需要获得内置锁，否则就处于阻塞状态。

代码如下：
public synchronized void save(){}
注：synchronized关键字也可以修饰静态方法，此时调用该静态方法，将会锁住整个类

### 同步代码块
synchronized关键字修饰的语句块。被该关键字修饰的语句块会自动加上内置锁，从而实现同步
代码如下：
synchronized(object){}

注：同步是一种高开销的操作，因此应该尽量减少同步内容。通常没有必要同步整个方法，使用synchronized代码块同步关键代码即可

### 使用特殊域变量（volatile）实现线程同步
1. volatile关键字为域变量的访问提供一种免锁机制
2. 使用volatile修饰域相当于告诉虚拟机该域可能被其他现象更新
3. 因此每次使用该域就要重新计算，而不是使用寄存器中的值
4. volatile不会提供任何原子操作，它也不能用来修饰final类型的变量

### 使用重入锁实现线程同步
在javaSE5.0新增了一个java.concurrent包来支持同步。ReentrantLock类可以重入、互斥、实现了Lock接口的锁，它与使用synchronized方法和快具体相同的基本行为和语义，并且扩展了其能力

ReentrantLock类的常用方法有：
ReentrantLock():创建一个ReentrantLock实例      
lock():获得锁  
unlock():释放锁

### 使用局部变量实现线程同步
如果使用ThreadLocal管理变量，则每一个使用变量的线程都获得该变量的副本，副本之间相互独立，这样每一个线程都可以随意修改自己的变量副本，而不会对其他线程产生影响。

ThreadLocal类的常用方法：
ThreadLocal():创建一个线程本地变量
get():返回此线程局部变量的当前线程副本中的值
initialValue():返回此线程局部变量的当前线程的“初始值”
set(T value):将此线程局部变量的当前线程副本中的值设置为value
#### ThreadLocal和线程同步机制对比

共同点：

   ThreadLocal和线程同步机制都是为了解决多线程中相同变量的访问冲突问题。

区别：

   在同步机制中，通过对象的锁机制保证同一时间只有一个线程访问变量。

      这时该变量是多个线程共享的，使用同步机制要求程序慎密地分析什么时候对变量进行读写，什么时候需要锁定某个对象，什么时候释放对象锁等繁杂的问题，程序设计和编写难度相对较大。
   而ThreadLocal则从另一个角度来解决多线程的并发访问。

      ThreadLocal会为每一个线程提供一个独立的变量副本，从而隔离了多个线程对数据的访问冲突。因为每一个线程都拥有自己的变量副本，从而也就没有必要对该变量进行同步了。

      ThreadLocal提供了线程安全的共享对象，在编写多线程代码时，可以把不安全的变量封装进ThreadLocal。
      由于ThreadLocal中可以持有任何类型的对象，低版本JDK所提供的get()返回的是Object对象，需要强制类型转换。但JDK5.0通过泛型很好的解决了这个问题，在一定程度地简化ThreadLocal的使用。

总结：
   对于多线程资源共享的问题，

    同步机制采用了“以时间换空间”的方式，

    而ThreadLocal采用了“以空间换时间”的方式。

前者仅提供一份变量，让不同的线程排队访问，而后者为每一个线程都提供了一份变量，因此可以同时访问而互不影响。

### 使用阻塞队列实现线程同步
前面5种同步方法都是在底层实现的线程同步，但还是我们在实际开发当中，应当尽量远离底层结构。使用javaSE5.0版本中新增的java.util.concurrent包将有助于简化开发。本小节主要使用LinkedBlockingQueue<E>来实现线程的同步，LinkedBlocking<E>来实现线程同步LinkedBlockingQueue<E>是一个基于已连接节点的，范围任意的blocking queue 队列是先进先出的顺序。

LinkedBlockingQueue 类常用方法 
LinkedBlockingQueue() : 创建一个容量为Integer.MAX_VALUE的LinkedBlockingQueue 
put(E e) : 在队尾添加一个元素，如果队列满则阻塞 
size() : 返回队列中的元素个数 
take() : 移除并返回队头元素，如果队列空则阻塞 

### 使用原子变量实现线程同步
原子操作就是指将读取变量值、修改变量值、保存变量值看成一个整体来操作
即-这几种行为要么同时完成，要么都不完成。

在java的util.concurrent.atomic包中提供了创建了原子类型变量的工具类，
使用该类可以简化线程同步。

其中AtomicInteger 表可以用原子方式更新int的值，可用在应用程序中(如以原子方式增加的计数器)，但不能用于替换Integer；可扩展Number，允许那些处理机遇数字类的工具和实用工具进行统一访问。

AtomicInteger类常用方法：
AtomicInteger(int initialValue) : 创建具有给定初始值的新的AtomicInteger
addAddGet(int dalta) : 以原子方式将给定值与当前值相加
get() : 获取当前值

## Thread的sleep释放锁吗？如何释放锁？
首先，多线程中会使用到两个延迟的函数，wait和sleep。 
wait是Object类中的方法，而sleep是Thread类中的方法。

sleep是Thread类中的静态方法。无论是在a线程中调用b的sleep方法，还是b线程中调用a的sleep方法，谁调用，谁睡觉。 
最主要的是sleep方法调用之后，并没有释放锁。使得线程仍然可以同步控制。sleep不会让出系统资源； 
而wait是进入线程等待池中等待，让出系统资源。

调用wait方法的线程，不会自己唤醒，需要线程调用 notify / notifyAll 方法唤醒等待池中的所有线程，才会进入就绪队列中等待系统分配资源。sleep方法会自动唤醒，如果时间不到，想要唤醒，可以使用interrupt方法强行打断。

Thread.sleep(0) // 触发操作系统立刻重新进行一次CPU竞争。

使用范围：

sleep可以在任何地方使用。而wait，notify，notifyAll只能在同步控制方法或者同步控制块中使用。 
sleep必须捕获异常，而wait，notify，notifyAll的不需要捕获异常。

## jdk1.8相比之前的版本有什么新特性？
Lambda表达式
函数式接口
方法引用和构造器调用
Stream API： map，filter，limit，
接口中的默认方法和静态方法
新时间日期API

## 列举常见的设计模式？
单例模式、工厂模式、模板方法模式、策略模式、装饰模式、代理模式、适配器模式

## javaweb

### Servlet生命周期
1. 加载: Tomcat类加载器加载Servlet字节码文件
2. 实例化: 创建对象，调用的构造方法
3. 初始化: init方法，可以对Servlet的一些数据进行赋值
4. 服务:service方法，父类的方法，我们重写doPost和doGet，然后父类再根据请求的方法调用子类的方法
5. 销毁: destroy方法，谁调用的方法？这是Web容器，Tomcat调用的

### JSP 9大内置对象及其功能
1. Request  获取请求提交的参数
2. Response 响应对象
3. Session   会话对象，存储用户信息，Token票据
4. application
5. page
6. pageContext
7. config
8. exception
9. out   向浏览器输出数据

### 四大作用域对象
1. pageContext 页面作用域
2. request作用域
3. session
4. application

### session和cookie的区别
存储的数据位置: session 服务器端、cookie客户端

存储的数据类型: session任何类、cookie只能String类型

存储的数据大小: session没有限制、cookie限制4KB

存储的数据时间: session默认30分钟，cookie可以自定义；setMaxAge

关联: session的id是通过一个cookie存储的，name=jsessionid
### 转发和重定向的区别
作用位置: 转发是在服务器端、重定向是在浏览器端

请求次数: 转发是同一个请求、重定向是新发送一个请求

数据获取: 转发客户获取request作用域的数据、重定向之后不可以获取

地址栏地址: 转发不变、重定向改变成新的请求地址
转发是系统内部的资源，重定向可以定位到外部的资源。
Servlet是线程安全的吗？ 不是线程安全的。Servlet不建议存储一些属性，单实例。
## JAVA反射机制

### 什么是反射机制？
JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。

### 静态编译和动态编译
静态编译：在编译时确定类型，绑定对象
动态编译：运行时确定类型，绑定对象

### 反射机制优缺点
优点：运行期类型的判断，动态加载类，提高代码灵活度。
缺点：性能瓶颈：反射相当于一系列解释操作，通知 JVM 要做的事情，性能比直接的java代码要慢很多。

### 反射机制的应用场景有哪些？
举例：①我们在使用JDBC连接数据库时使用Class.forName()通过反射加载数据库的驱动程序；②Spring框架也用到很多反射机制，最经典的就是xml的配置模式。
Spring 通过 XML 配置模式装载 Bean 的过程：
1. 将程序内所有 XML 或 Properties 配置文件加载入内存中;
2. Java类里面解析xml或properties里面的内容，得到对应实体类的字节码字符串以及相关的属性信息;
3. 使用反射机制，根据这个字符串获得某个类的Class实例; 
4. 动态配置实例的属性

Java获取反射Class对象的三种方法
1. 通过new对象实现反射机制 
2. 通过路径实现反射机制 
3. 通过类名实现反射机制

回答思路：
1. 反射是对于任意一个类，都可以动态的获取它的信息，包括属性、方法等；
2. 反射的核心类是Class；
3. Class对象的三种获取方式是class.forName()、类名.class、对象名.getClass()；
4. 反射的应用场景：spring、springMvc、mybatis底层都是通过反射来实现的，比如<Bean>中的id、class都是应用了反射，通过获取Bean的构造方法来创建对象。

## 网络编程
简单实现服务器端和客户端通信，客户端发送数据、服务器原样返回？

### 服务器端
1. 创建服务器端ServerSocket对象，并指定端口号
2. 调用serverSocket.accept()方法，线程阻塞:等待客户端连接
3. 当有客户端连接到服务器的时候，accept方法返回的是Socket对象
4. 通过socket对象获取输入流和输出流进行数据传输
5. 关闭输入流和输出流包括serverSocket也要关闭；

### 客户端
1. 创建Socket对象，两个参数：服务器的ip地址和端口号
2. 连接到服务器
3. 通过socket对象获取输入流和输出流，进行数据读取和发送
4. 关闭输入流和输出流，包括Socket对象

## 简述HTTP和TCP，UDP的区别和应用
### TCP协议
TCP一般用于文件传输（FTP HTTP 对数据准确性要求高，速度相对慢），收发邮件（POP IMAP SMTP 对数据准确性要求高，非紧急应用），远程登录（TELNET SSH 对数据准确性有一定要求，有连接的概念）；UDP一般用于即时通信（QQ聊天 对数据准确性和丢包要求比较低，但速度必须快），在线视频（RTSP 速度一定要快，保证视频连续），网络语音电话（语音数据包一般比较小，需要高速发送）

### UDP协议
UDP 用户数据报协议，是一个面向无连接的协议。采用该协议不需要两个应用程序先建立连接。UDP协议不提供差错恢复，不能提供数据重传，因此该协议传输数据安全性差。最大长度是1480字节。

### TCP与UDP的区别和应用
1. TCP基于连接的UPD是无连接  
2. TCP要求系统资源较多，UDP较少；   
3. TCP程序结构复杂，UDP程序结构较简单   
4. TCP基于流模式，UDP基于数据报模式;   
5. TCP保证数据正确性，UDP可能丢包   
6. TCP保证数据顺序，UDP不保证 
7. TCP只能点对点全双工通信;UDP支持一对一、一对多、多对一和多对多的交互通信

### HTTP
HTTP（超文本传输协议）是一个基于请求与响应模式的、无状态的、应用层的协议，在上网浏览网页的时候，浏览器和web服务器之间通过HTTP在Internet上进行数据的发送和接收。 常基于TCP的连接方式http表示要通过HTTP协议来定位网络资源；host表示合法的Internet主机域名或者IP地址；port指定一个端口号，为空则使用交请求后，通过HTTP协议传送给Web服务器。Web服务器接到后，进行事务处理，处理结果又通过H缺省端口80；abs_path指定请求资源的URI；如果URL中没有给出abs_path，那么当它作为请求URI时，必须以“/”的形式给出，通常这个工作浏览器自动帮我们完成。

(1) 连接：Web浏览器与Web服务器建立连接，打开一个称为socket（套接字）的虚拟文件，此文件的建立标志着连接建立成功。　　

(2) 请求：Web浏览器通过socket向Web服务器提交请求。HTTP的请求一般是GET或POST命令（POST用于FORM参数的传递）。GET命令的格式为：GET 路径/文件名 HTTP/1.0文件名指出所访问的文件，HTTP/1.0指出Web浏览器使用的HTTP版本。　　

应答：Web浏览器提TTP传回给Web浏览器，从而在Web浏览器上显示出所请求的页面。

## 软连接和硬链接区别？
### 定义不同

软链接又叫符号链接，这个文件包含了另一个文件的路径名。可以是任意文件或目录，可以链接不同文件系统的文件。

硬链接就是一个文件的一个或多个文件名。把文件名和计算机文件系统使用的节点号链接起来。因此我们可以用多个文件名与同一个文件进行链接，这些文件名可以在同一目录或不同目录。

### 限制不同
硬链接只能对已存在的文件进行创建，不能交叉文件系统进行硬链接的创建；
软链接可对不存在的文件或目录创建软链接；可交叉文件系统；

### 创建方式不同
硬链接不能对目录进行创建，只可对文件创建；
软链接可对文件或目录创建；

### 影响不同

删除一个硬链接文件并不影响其他有相同 inode 号的文件。

删除软链接并不影响被指向的文件，但若被指向的原文件被删除，则相关软连接被称为死链接（即 dangling link，若被指向路径文件被重新创建，死链接可恢复为正常的软链接）。

## 项目中出现内存泄露的原因，要怎么处理？
close、赋值为NULL等等