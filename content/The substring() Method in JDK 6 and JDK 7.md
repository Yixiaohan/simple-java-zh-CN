## The substring() Method in JDK 6 and JDK 7
 
`substring(int beginIndex, int endIndex)` 方法在 JDK 6 和 JDK 7 的底层实现是不同的，了解这些不同，可以帮助我们更好的使用这个方法。为了简单起见，下文中用 `substring()` 指代 `substring(int beginIndex, int endIndex)`。

###1.substring() 方法的作用是什么?
`substring(int beginIndex, int endIndex)` 方法返回字符串，该字符串以 beginIndex 为起始，以 endIndex-1 为结束

```
String x = "abcdef";
x = x.substring(1,3);
System.out.println(x);
```
输出结果为：

```
bc
```

###2.当调用 substring() 方法时，发生了什么？

变量 x 是不可变的，当 x.substring(1,3) 的返回值赋值给 x 时，x 就指向了一个全新的字符串

![](http://www.programcreek.com/wp-content/uploads/2013/09/string-immutability1-650x303.jpeg)

然而，上面的图不完全正确。
因为，当 `substring()` 被调用时，在 JDK 6 和 JDK 7 底层实现是不同的。

###3.JDK 6 中的 substring()

Java 中的字符串是通过字符数组（char array）来支持实现的，在JDK 6 中，**String** 类包含了 3 个域，`char[] value`、`int offset`、`int count`。它们分别用于存储真实的字符数组、数组的开始下标以及字符串中的字符数量。

当 substring() 方法被调用时，它会创建一个新的字符串对象，但是这个字符串的值在 Java 堆中仍然指向的是同一个数组。这两个字符串的不同在于他们的 count 和 offset 的值。

![](http://www.programcreek.com/wp-content/uploads/2013/09/string-substring-jdk6.jpeg)

以下是 JDK 6 中的简化后只包括核心逻辑的代码，足以说明问题：

```
//JDK 6
String(int offset, int count, char value[]) {
	this.value = value;
	this.offset = offset;
	this.count = count;
}
 
public String substring(int beginIndex, int endIndex) {
	//check boundary
	return  new String(offset + beginIndex, endIndex - beginIndex, value);
}
```

###4.JDK 6 中 substring() 引起的问题

如果你有一个**非常长**的字符串，但是你仅仅只需要这个字符串的一小部分，这就会导致性能问题，因为你需要的只是很小的部分，而这个子字符串却要包含整个字符数组，在JDK 6 中的解决办法就是使用下面的方法，它会指向一个真正的子字符串。

```
x = x.substring(x, y) + ""
```


### 5.JDK 7 中的 substring()

上面提到的问题，在 JDK7 中已经改正。在 JDK7 中，substring() 方法确实会在堆中创建一个新的数组。如下图所示：

![](http://www.programcreek.com/wp-content/uploads/2013/09/string-substring-jdk71.jpeg)



```
//JDK 7
public String(char value[], int offset, int count) {
	//check boundary
	this.value = Arrays.copyOfRange(value, offset, offset + count);
}
 
public String substring(int beginIndex, int endIndex) {
	//check boundary
	int subLen = endIndex - beginIndex;
	return new String(value, beginIndex, subLen);
}
```

[Top 10 questions of Java Strings](http://www.programcreek.com/2013/09/top-10-faqs-of-java-strings/)

参考：
[Java 6 vs Java 7: When implementation matters](http://nextmovesoftware.com/blog/2013/07/05/java-6-vs-java-7-when-implementation-matters/)

[本文英文原文](http://www.programcreek.com/2013/09/the-substring-method-in-jdk-6-and-jdk-7/)


