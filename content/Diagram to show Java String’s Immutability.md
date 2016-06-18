##Diagram to show Java String’s Immutability
## 图解 Java 字符串的不可变性

通过一系列的图片来说明 Java 中字符串的不可变性（Java String's immutability）。

###1.声明字符串

```
String s = "abcd";
```
变量 s 存储着字符串对象的索引。下图中的箭头的意思就是「store reference of」。

![String-Immutability-1](http://www.programcreek.com/wp-content/uploads/2009/02/String-Immutability-1.jpeg)

###2.将一个字符串变量赋值给另外一个字符串变量

s2 stores the same reference value since it is the same string object.

![](http://www.programcreek.com/wp-content/uploads/2009/02/String-Immutability-2.jpeg)

###3.合并字符串 Concat string

```
s = s.concat("ef");
```

现在，s 变量存储的是**新创建**的字符串对象的引用

![](http://www.programcreek.com/wp-content/uploads/2009/02/string-immutability-650x279.jpeg)

###4.总结

一旦一个字符串在[内存（栈）](http://www.programcreek.com/2013/04/jvm-run-time-data-areas/)上创建，这个字符串将不可改变。我们应该注意到 String 类中的所有方法都不会改变**字符串本身**，而是返回一个**新的字符串**。

如果我们需要一个可以改变的字符串，那么我们可以使用 **StringBuffer** 或 **StringBuilder**。否则，因为每次都是创建一个新的字符串。所以，这将浪费好多时间在垃圾回收上。

[本文英文原文 http://www.programcreek.com/2009/02/diagram-to-show-java-strings-immutability/](http://www.programcreek.com/2009/02/diagram-to-show-java-strings-immutability/)

