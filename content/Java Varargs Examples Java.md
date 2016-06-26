## Java Varargs Examples Java 可变参数
 
##1. What is Varargs in Java? 可变参数是什么？

可变参数 (variable arguments) 是在 Java 1.5 中引进的新特性。可变参数允许方法有任意个数量的参数。

```
public static void main(String[] args) 
{
	print("a");
	print("a", "b");
	print("a", "b", "c");
}
 
public static void print(String ... s)
{
	for(String a: s)
		System.out.println(a);
}
```

##2. How Varargs Work? 可变参数工作原理

当使用可变参数时，实际上底层首先创建了一个数组，然后把参数值放进该数组当中，最后将该数组传递给了调用方法。

##3. When to Use Varargs? 什么时候使用可变参数

正如定义所说，当你不确定一个方法的参数时，就可以用可变参数了。
Java SDK 使用可变参数的好的例子是
`String.format(String format, Object... args).` 该方法可以格式化任意数量的参数。

```
String.format("An integer: %d", i);
String.format("An integer: %d and a string: %s", i, s);
```
[英文原文地址为： http://www.programcreek.com/2014/01/java-varargs-examples/](http://www.programcreek.com/2014/01/java-varargs-examples/)


