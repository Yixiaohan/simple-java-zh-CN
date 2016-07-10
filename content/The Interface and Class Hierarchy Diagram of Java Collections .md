# The Interface and Class Hierarchy Diagram of Java Collections 

层次关系图

## 1. Collection vs Collections


首先，"Collection" 和 "Collections" 是两个不同的概念。
正如下图所示，"Collection" 是顶层接口，而 "Collections" 是一个类，该类提供了一些静态方法用来操作 Collection中的数据。

![CollectionVsCollections](http://www.programcreek.com/wp-content/uploads/2009/02/CollectionVsCollections.jpeg)


## 2. Class hierarchy of Collection 集合类层次关系图


![java-collection-hierarchy](http://www.programcreek.com/wp-content/uploads/2009/02/java-collection-hierarchy.jpeg)

## 3. Class hierarchy of Map 


![MapClassHierarchy](http://www.programcreek.com/wp-content/uploads/2009/02/MapClassHierarchy-600x354.jpg)

## 4. Summary of classes 集合类总结

![collection-summary](http://www.programcreek.com/wp-content/uploads/2009/02/collection-summary.png)

## 5. Code Example 代码示例

```
List<String> a1 = new ArrayList<String>();
a1.add("Program");
a1.add("Creek");
a1.add("Java");
a1.add("Java");
System.out.println("ArrayList Elements");
System.out.print("\t" + a1 + "\n");
 
List<String> l1 = new LinkedList<String>();
l1.add("Program");
l1.add("Creek");
l1.add("Java");
l1.add("Java");
System.out.println("LinkedList Elements");
System.out.print("\t" + l1 + "\n");
 
Set<String> s1 = new HashSet<String>(); // or new TreeSet() will order the elements;
s1.add("Program");
s1.add("Creek");
s1.add("Java");
s1.add("Java");
s1.add("tutorial");
System.out.println("Set Elements");
System.out.print("\t" + s1 + "\n");
 
Map<String, String> m1 = new HashMap<String, String>(); // or new TreeMap() will order based on keys
m1.put("Windows", "2000");
m1.put("Windows", "XP");
m1.put("Language", "Java");
m1.put("Website", "programcreek.com");
System.out.println("Map Elements");
System.out.print("\t" + m1);
```

输出结果为：

```
ArrayList Elements
	[Program, Creek, Java, Java]
LinkedList Elements
	[Program, Creek, Java, Java]
Set Elements
	[tutorial, Creek, Program, Java]
Map Elements
	{Windows=XP, Website=programcreek.com, Language=Java}
```


