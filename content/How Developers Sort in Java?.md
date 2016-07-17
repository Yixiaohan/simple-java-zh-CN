# How Developers Sort in Java?

在阅读 Java 开源项目源代码过程中，我发现 Java 程序员经常使用两排序方式：
* 一种是使用 Collections 或 Arrays 类的 sort 方法，
* 另一种是使用可排序的数据结构，例如，TreeMap、TreeSet


## 1. Using sort() Method 使用sort()方法

如果是 collection ，则可以使用 `Collections.sort() `

```
// Collections.sort
List<ObjectName> list = new ArrayList<ObjectName>();
Collections.sort(list, new Comparator<ObjectName>() 
{
	public int compare(ObjectName o1, ObjectName o2) 
	{
		return o1.toString().compareTo(o2.toString());
	}
});
```


如果是数组，则可以使用 `Arrays.sort()`

```
// Arrays.sort
ObjectName[] arr = new ObjectName[10];
Arrays.sort(arr, new Comparator<ObjectName>() 
{
	public int compare(ObjectName o1, ObjectName o2) 
	{
		return o1.toString().compareTo(o2.toString());
	}
});
```


## 2. Using Sorted Data Structures 使用可排序的数据结构

如果是 list 或 set，则可以使用 TreeSet 排序

```
// TreeSet
Set<ObjectName> sortedSet = new TreeSet<ObjectName>(new Comparator<ObjectName>() {
	public int compare(ObjectName o1, ObjectName o2) {
		return o1.toString().compareTo(o2.toString());
	}
});
sortedSet.addAll(unsortedSet);
```

如果是 map ，则可以使用 TreeMap 进行排序，TreeMap 是根据 key 来排序的。

```
// TreeMap - using String.CASE_INSENSITIVE_ORDER which is a Comparator that orders Strings by compareToIgnoreCase
Map<String, Integer> sortedMap = new TreeMap<String, Integer>(String.CASE_INSENSITIVE_ORDER);
sortedMap.putAll(unsortedMap);
//TreeMap - In general, defined comparator
Map<ObjectName, String> sortedMap = new TreeMap<ObjectName, String>(new Comparator<ObjectName>() {
	public int compare(ObjectName o1, ObjectName o2) {
		return o1.toString().compareTo(o2.toString());
	}
});
sortedMap.putAll(unsortedMap);
```
This approach is very useful, if you would do a lot of search operations for the collection. The sorted data structure will give time complexity of O(logn), which is lower than O(n).

## 3. Bad Practices 不好的编程实践

也有很多不好的编程实践，比如说，使用自定义的排序算法。
以下代码，不仅效率低，而且可读性也很差

```
double t;
for (int i = 0; i < 2; i++)
	for (int j = i + 1; j < 3; j++)
		if (r[j] < r[i]) {
			t = r[i];
			r[i] = r[j];
			r[j] = t;
		}
```
[英文原文链接 http://www.programcreek.com/2014/03/how-developers-sort-in-java/](http://www.programcreek.com/2014/03/how-developers-sort-in-java/)


