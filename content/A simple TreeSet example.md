# A simple TreeSet example

下面非常简单的小例子是有关 TreeSet。从例子中可以看出：

*  TreeSet 是有序的
*  如何 iterate（迭代）TreeSet
*  如何检测 TreeSet 是否为空
*  如何获取 TreeSet 的第一个元素、最后一个元素

如果想看更多有关 Java Collection（类集框架）的知识，请点击查看
[the Java Collection hierarchy diagram](http://www.programcreek.com/2009/02/the-interface-and-class-hierarchy-for-collections/)



```
import java.util.Iterator;
import java.util.TreeSet;

public class TreeSetExample
{
	public static void main(String[] args)
	{
		System.out.println("Tree Set Example!\n");
		
		TreeSet<Integer> tree = new TreeSet<Integer>();
		tree.add(12);
		tree.add(63);
		tree.add(34);
		tree.add(45);

		// here it test it's sorted, 63 is the last element. see output below
		Iterator<Integer> iterator = tree.iterator();
		System.out.print("Tree set data: ");

		// Displaying the Tree set data
		while (iterator.hasNext())
		{
			System.out.print(iterator.next() + " ");
		}
		System.out.println();

		// Check empty or not
		if (tree.isEmpty())
		{
			System.out.print("Tree Set is empty.");
		} 
		else
		{
			System.out.println("Tree Set size: " + tree.size());
		}

		// Retrieve first data from tree set
		System.out.println("First data: " + tree.first());

		// Retrieve last data from tree set
		System.out.println("Last data: " + tree.last());

		if (tree.remove(45))
		{ // remove element by value
			System.out.println("Data is removed from tree set");
		}
		else
		{
			System.out.println("Data doesn't exist!");
		}
		System.out.print("Now the tree set contain: ");
		iterator = tree.iterator();

		// Displaying the Tree set data
		while (iterator.hasNext())
		{
			System.out.print(iterator.next() + " ");
		}
		System.out.println();
		System.out.println("Now the size of tree set: " + tree.size());

		// Remove all
		tree.clear();
		if (tree.isEmpty())
		{
			System.out.print("After clear, Tree Set is empty.");
		} 
		else
		{
			System.out.println("Tree Set size: " + tree.size());
		}
	}
}
```


输出结果为：

```
Tree Set Example!

Tree set data: 12 34 45 63
Tree Set size: 4

First data: 12
Last data: 63

Data is removed from tree set

Now the tree set contain: 12 34 63
Now the size of tree set: 3

Tree Set is empty.
```


[本文英文原文地址 http://www.programcreek.com/2009/02/a-simple-treeset-example/](http://www.programcreek.com/2009/02/a-simple-treeset-example/)

