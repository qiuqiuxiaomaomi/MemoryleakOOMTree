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