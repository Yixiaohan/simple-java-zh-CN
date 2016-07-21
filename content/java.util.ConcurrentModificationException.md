# java.util.ConcurrentModificationException

本文将解决 ArrayList 常见的 java.util.ConcurrentModificationException

错误信息类似：

```
Exception in thread "main" java.util.ConcurrentModificationException
	at java.util.ArrayList$Itr.checkForComodification(Unknown Source)
	at java.util.ArrayList$Itr.next(Unknown Source)
	...
	...
```

## The Problem

一边循环（基本的 for 循环、增强型 for 循环） ArrayList，一边删除其中的元素，就会引起 java.util.ConcurrentModificationException

```
import java.util.ArrayList;
import java.util.List;
 
public class AddRemoveListElement 
{
 
	public static void main(String args[])
	 {
		List<String> list = new ArrayList<String>();
		list.add("A");
		list.add("B");
 
		for (String s : list) 
		{
			if (s.equals("B")) 
			{
				list.remove(s);
			}
		}
	}
}
```
![java.util.ConcurrentModificationException](http://www.programcreek.com/wp-content/uploads/2014/01/java-util-concurrentModificationException.jpg)


##Solution 1 解决方案一

使用 Iteator

```
Iterator<String> iter = list.iterator();
while(iter.hasNext())
{
	String str = iter.next();
      if( str.equals("B") )
      {
        iter.remove();
      }
}
```

## Solution 2 解决方案二

不使用 `ArrayList`，而是使用 `CopyOnWriteArrayList`。
`CopyOnWriteArrayList` 是线程安全的。

```
public static void main(String args[]) 
{
	List<String> list = new CopyOnWriteArrayList<String>();
	list.add("A");
	list.add("B");
 
	for (String s : list) 
	{
		if (s.equals("B")) 
		{
			list.remove(s);
		}
	}
}
```

## How about other Collection types?


```
public static void main(String args[]) {
	Set<String> set = new HashSet<String>();
	set.add("A");
	set.add("B");
 
	for (String s : set) {
		if (s.equals("B")) {
			set.remove(s);
		}
	}
}
```


```
public static void main(String args[]) {
	LinkedList<String> llist = new LinkedList<String>();
	llist.add("A");
	llist.add("B");
 
	for (String s : llist) {
		if (s.equals("B")) {
			llist.remove(s);
		}
	}
}
```
上面的代码没问题，因为它们的底层实现不是用的 array。

[本文英文原文地址 http://www.programcreek.com/2014/01/java-util-concurrentmodificationexception/](http://www.programcreek.com/2014/01/java-util-concurrentmodificationexception/)


