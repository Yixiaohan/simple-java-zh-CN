## Start from length & length() in Java

首先，你可以快速回答以下问题吗？

> 在不使用任何 IDE 自动补全的情况下，如何获取一个数组的长度？如何获取一个字符串的长度？

这个问题，我问过初级和中级，两个不同层次的开发人员。他们都不能准确而自信地回答这个问题。当 IDE 提供方便的代码自动补全功能时，它也会带来 “肤浅表面的理解” 的问题。在这篇文章中，将介绍一些 Java 数组的关键概念。

上述问题的正确答案是：


```
int[] arr = new int[3];
System.out.println(arr.length);//length for array
 
String str = "abc";
System.out.println(str.length());//length() for string
```
问题是，为什么数组有 length 属性，而字符串没有？或者，为什么字符串有 length() 方法，而数组没有？


### Q1. Why arrays have length property?为什么数组有 length 属性？

首先，一个数组是一个对象容器，包含了一定数量的对象，这些对象都是同一个类型。当一个数组被创建后，数组的长度不会再改变。数组的长度可以当成一个 final 实例变量。因此，length 可以当做数组的一个定义好的属性。

数组有两种创建方式：
1) 数组创建表达式（an array creation expression），
2) 数组初始化（an array initializer.）。当它被创建时，它的长度已经确定下来。

上面的例子就是用的数组表达式。它指明了元素类型、数组嵌套的层次数以及每一层（至少一层）的数组长度。

下面的这个声明方式也是合法的，即使只声明了嵌套中一层的长度。

```
int[][] arr = new int[3][];
```
数组初始化也可以创建数组，比提供所有的初始化值。它写起来像是逗号分割的表达式列表，只是被花括号包裹。例如：

```
int[] arr = {1, 2, 3};
```

### Q2. Why there is not a class "Array" defined similarly like "String"? 为什么没有定义一个类似 String 的 Array 类？

因为数组也是对象，所以下面的代码也是合法的：

```
Object obj = new int[10];
```


数组包含所有从 Object 类继承下来的方法，除clone()之外。为什么没有为数组定义一个类呢？我们也没发现Array.java文件。一个简单的解释是，它们被隐藏起来了。你可以这样想这个问题，如果存在这样一个类 Array，那么它将会是什么样子呢？那么，还是需要一个数组来包含数组数据，对吧？因此，定义一个这样的类并不是好主意。

实际上，我们可以通过下面的这段代码来获取一个数组的类型：

```
int[] arr = new int[3];
System.out.println(arr.getClass());
```

输出结果为：

```
class [I
```
**class [I** 表示 int 数组的运行时类型。

Q3. Why String has length() method?为什么字符串有length()方法？

String 背后的数据结构是 char array。所以，没有必要再定义一个属性。这点和 C语言 不同，字符数组在 Java 中不是一个字符串。

英语原文链接地址[start-from-length-length-in-java](http://www.programcreek.com/2013/11/start-from-length-length-in-java/)

