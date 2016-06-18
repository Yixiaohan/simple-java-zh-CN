## Why string is immutable 
##为什么字符串是不可变的

**String** 是 Java 中一个不可变的类。不可变的类一旦被实例化则无法被修改。不可变类的实例一旦创建，其成员变量的值就不能被修改。不可变类有很多优势。本文总结了为什么字符串被设计成不可变的。一个好的回答需要建立在对内存、同步、数据结构等知识的深入理解之上.

###字符串池

字符串池是方法区中的一部分特殊存储。当一个字符串被被创建的时候，首先会去这个字符串池中查找，如果找到，直接返回对该字符串的引用。

下面的代码只会在堆中创建一个字符串


`String string1 = "abcd";
String string2 = "abcd";`

下面是图示：

![java-string-pool](http://www.programcreek.com/wp-content/uploads/2013/07/java-string-pool.jpeg)

如果字符串是可变的，那么改变其中一个引用指向的字符串将会导致另外一个引用所指向错误的值。

##2. Caching Hashcode 缓存字符串的哈希值

在 Java 中 字符串的 hashcode （哈希值）经常会用到。例如，在 HashMap 中，不可变保证字符串的哈希值总是一样的，所以，可以缓存起来而不用担心发现变化。换句话说，并不是每次调用都需要计算哈希值。这样会更有效。

在 String 类的源代码中，有如下代码：


```
private int hash;//this is used to cache hash code.
```
 
## 3. Facilitating the Use of Other Objects

举例说明，考虑以下代码：

```
HashSet<String> set = new HashSet<String>();
set.add(new String("a"));
set.add(new String("b"));
set.add(new String("c"));

for(String a: set)
	a.value = "a";
	
```

在此例子中，如果字符串是可变的，那么字符串的值改变后将会违背 set 的设计原则（ set 是不允许出现重复的值的），此例是简要说明问题，真实情况中，String 类是没有 value 字段的。

##4. Security 安全性

字符串作为类的参数，被广泛应用于 Java 的很多类中。例如，网络连接、打开的文件等等。如果字符串是可变的，一个连接或者文件将可能会被改变，从而导致严重的安全问题。方法以为它已经连接到一个机器上，但事实上却没有。在反射中，可变的字符串也可能导致安全问题，例如字符串参数

示例代码：

```
boolean connect(string s){
    if (!isSecure(s)) { 
throw new SecurityException(); 
}
    //here will cause problem, if s is changed before this by using other references.    
    causeProblem(s);
}
```


## 5. Immutable objects are naturally thread-safe 不可变对象天生是线程安全的

因为不可变对象是不可变的，所以不可变对象可以在多线程环境中自由的共享。This eliminates the requirements of doing synchronization.

总结一下，String 类设计成不可变是为了效率和安全性的考虑。这也是不可变类更受欢迎的原因。

本文英文链接为[http://www.programcreek.com/2013/04/why-string-is-immutable-in-java/](http://www.programcreek.com/2013/04/why-string-is-immutable-in-java/)

