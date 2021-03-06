# MemoryleakOOMTree
Java内存溢出，内存泄漏技术研究

![](https://i.imgur.com/TS9OxVj.png)

<pre>
内存泄漏：
        内存泄漏的定义：对象已经没有被应用程序使用，但是垃圾回收器没办法移除它们，因为还
      在被引用着
</pre>

<pre>
Java内存模型
      按照JVM规范，JAVA虚拟机在运行时会管理一下的内存区域：
          1）程序计数器：
             当前线程执行的字节码的行号指示器，线程私有
          2）JAVA虚拟机栈
             JAVA方法执行的内存模型，每个Java方法的执行对应着一个栈帧的进栈和出栈的操作。
          3）本地方法栈
             类似JAVA虚拟机栈，但是为Native方法运行提供内存环境。
          5）JAVA堆
             对象内存分配的地方，内存垃圾回收的主要区域，所有线程共享，可以分为新生代，老年代。
          6）方法区
             用于存储已经被JVM加载的类信心，常量，静态变量，JIT编译器编译后的代码等数据，
             HotSpot中的永久代。
          7）运行时常量池
             方法区的一部分，存储常量信息，如各种字面量，符号引用等。
          8）直接内存
              并不是JVM运行时数据区的一部分，可直接访问的内存，比如NIO用到的部分。
</pre>

<pre>
常见的OOM情况有3种：

      1）堆溢出
         java.lang.OutOfMemoryError:Java heap space

      2）方法区溢出
         Java.lang.OutOfMemoryError:PermGen space
 
      3) 栈溢出
         Java.lang.StackOverflowError:
</pre>

<pre>
内存泄漏场景

      1）Hashmap, vector等容易和应用生命周期一样，所引用的所有对象Object也不能释放。
      2）当集合类里面的对象的属性被修改后，再调用remove()不起作用，hashcode值发生了变更。
      3) 对象添加监听器，但是往往释放对象时忘记删除监听器。
      5）各种连接记得关闭
      6）内部类的引用
      7）调用其他模块，对象作为参数
      8）单例模式，持有外部对象的引用，所以无法回收
</pre>

<pre>
栈溢出

      1)是否递归的调用，大量循环，全局变量是否过多，
      2）栈过大会导致内存占用过多，频繁页交换阻碍效率。
      3）过多使用了static:static最好只用int或者string等基本类型。
         大量的递归或者死循环；
         大数据项的查询，如返回表的所有记录，应该采用分页查询
         检查是否有数组，list,map中存放的是对象的引用而不是对象。这些引用会让个对象不能被释放掉。
</pre>

<pre>
常用调优工具分为两类

        jdk自带监控工具：jconsole和jvisualvm，第三方有：MAT(Memory Analyzer Tool)、
        GChisto。

        1.jconsole，Java Monitoring and Management Console是从java5开始，在JDK中
          自带的java监控和管理控制台，用于对JVM中内存，线程和类等的监控
        2.jvisualvm，jdk自带全能工具，可以分析内存快照、线程快照；监控内存变化、GC变化等。
        3.MAT，Memory Analyzer Tool，一个基于Eclipse的内存分析工具，是一个快速、功能
          丰富的Java heap分析工具，它可以帮助我们查找内存泄漏和减少内存消耗
        4.GChisto，一款专业分析gc日志的工具
</pre>