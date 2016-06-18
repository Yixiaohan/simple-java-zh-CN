## Create Java String Using ” ” or Constructor? 创建字符串时，使用“ ”还是使用构造函数？

在 Java 中创建字符串有两种方法：

```
String x = "abc";
String y = new String("abc");
```
使用双引号和使用构造方法创建字符串，二者有哪些区别呢？

###1. Double Quotes vs. Constructor 双引号 vs 构造函数

用两段简短的事例代码说明：

**例 1:**

```
String a = "abcd";
String b = "abcd";
System.out.println(a == b);  // True
System.out.println(a.equals(b)); // True
```

a == b等于 true，是因为 x 和 y 指向内存方法区中同一个字符串常量，他们的引用是相同的（==比较的是引用）。

当相同的字符串常量被多次创建时，只会保存字符串常量的一份副本，这称为 string interning （字符串驻留）。在 Java中，所有编译时字符串常量都是驻留的。

**例 2:**

```
String c = new String("abcd");
String d = new String("abcd");
System.out.println(c == d);  // False
System.out.println(c.equals(d)); // True
```
c==d is false because c and d refer to two different objects in the heap. Different objects always have different memory references.

c == d等于 false， 是因为 c 和 d 指向内存 heap（堆）中不同的对象。不同的对象总是拥有不同的内存引用。

下面的两张图说明了以上两种情形：

![constructor-vs-double-quotes-Java-String](http://www.programcreek.com/wp-content/uploads/2014/03/constructor-vs-double-quotes-Java-String-New-Page-650x324.png)



### 2. Run-Time String Interning 运行时字符串驻留

运行时也会发生 String interning（字符串驻留），即使两个字符串是由构造函数方法创建的。

```
String c = new String("abcd").intern();
String d = new String("abcd").intern();
System.out.println(c == d);  // Now true
System.out.println(c.equals(d)); // True
```

###3. When to Use Which

字符串 "abcd" 已经是字符串类型了，使用构造函数只会创建一个多余的、毫无用途的对象。因此，当需要创建字符串时，就应该使用双引号。

如果你需要在内存的 heap （堆）中创建一个新的字符串对象，那么，就应该使用构造函数了。这是用构造函数创建字符串的一个应用场景。


