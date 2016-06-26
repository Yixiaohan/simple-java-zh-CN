# What exactly is null in Java? null 究竟是什么？
 
让我们以下面的语句开始：

`String x = null;`

##1. What exactly does this statement do? 该语句做了什么？

回忆一下什么是变量，什么是变量的值。常见的比喻是，变量就像一个盒子。就像你可以用盒子来存放物品一样，你可以用变量存放值。当你声明一个变量的时候，应该同时设置此变量的类型。

Java 中两种主要的类型。原生数据类型和引用类型（primitive and reference）。当变量声明为原生数据类型时，它存放的是值。当变量声明为引用类型时，它存放的是引用。`String x = null;`中的变量 x，存放的是 字符串引用，此时为 null。


下图更加的直观：

![string null reference](http://www.programcreek.com/wp-content/uploads/2013/12/what-is-null-150x150.png)



如果 `x = "abc"; ` 那么：

![variable-reference](http://www.programcreek.com/wp-content/uploads/2013/12/variable-reference.png)

##2. What exactly is null in memory?在内存中 null 是怎样的？


在内存中，null 是什么呢？或者说，在 Java 中，null 的值是什么？

首先，null 不是一个合法的对象实例，所以并没有为它分配内存。它只是一个简单的值，该值表示对象的引用现在并没有指向一个对象实例。

Java [虚拟机规范中](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-2.html#jvms-2.4) ：

> The Java Virtual Machine specification does not mandate a concrete value encoding null.


##3. What exactly is x in memory?

Now we know what null is. And we know a variable is a storage location and an associated symbolic name (an identifier) which contains some value. Where exactly x is in memory?

From the diagram of JVM run-time data areas, we know that since each method has a private stack frame within the thread's steak, the local variable are located on that frame.

参考文献:
1. [Variables, Operators, and Expressions](http://www.cs.cmu.edu/~pattis/15-1XX/15-200/lectures/voe/lecture.html)
2. [Variable](https://en.wikipedia.org/wiki/Variable_(computer_science))
3. [JVM Specifications](http://docs.oracle.com/javase/specs/jvms/se7/html/jvms-2.html#jvms-2.4)

[本文英文原文地址为:     http://www.programcreek.com/2013/12/what-exactly-is-null-in-java/](http://www.programcreek.com/2013/12/what-exactly-is-null-in-java/)

