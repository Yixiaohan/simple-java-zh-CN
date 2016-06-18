## How to Check if an Array Contains a Value in Java Efficiently?

如何检查一个未排序的数组中是否包含某个特定值，这是一个在 Java 中非常实用并且频繁使用的操作。也是 Stack Overflow 上面非常受关注的问题。在得票数最多的答案中，检查数组中是否包含特定值可以用多种不同的方式实现，但是每种方式的时间复杂度是有差别的。下文将展示每种实现方式的时间复杂度。

###1. Four Different Ways to Check If an Array Contains a Value 检查数组中是否包含某特定值的四种不同方法


1) Using List:

```
public static boolean useList(String[] arr, String targetValue) 
{
	return Arrays.asList(arr).contains(targetValue);
}
```

2) Using Set:

```
public static boolean useSet(String[] arr, String targetValue) 
{
	Set<String> set = new HashSet<String>(Arrays.asList(arr));
	return set.contains(targetValue);
}
```

3) Using a simple loop:

```
public static boolean useLoop(String[] arr, String targetValue) 
{
	for(String s: arr)
	{
		if(s.equals(targetValue))
			return true;
	}
	return false;
}
```

4) Using Arrays.binarySearch():


下面的代码是错误的，在这里列出来此代码，是为了便于理解。
binarySearch()（二分搜索方法）**仅仅**试用于，己排序的数组。
以下代码的运行结果很诡异的。

```
public static boolean useArraysBinarySearch(String[] arr, String targetValue) 
{	
	int a =  Arrays.binarySearch(arr, targetValue);
	if(a > 0)
		return true;
	else
		return false;
}
```

###2. Time Complexity

The approximate time cost can be measured by using the following code. The basic idea is to search an array of size 5, 1k, 10k. The approach may not be precise, but the idea is clear and simple.

以下代码可以衡量每种方法的近似时间消耗。基本思想就是分别查找 5，1000，10000个元素的数组。可能不精确，但基本思想简单清晰可行。


```
public static void main(String[] args) 
{
	String[] arr = new String[] {  "CD",  "BC", "EF", "DE", "AB"};
 
	//use list
	long startTime = System.nanoTime();
	for (int i = 0; i < 100000; i++) 
	{
		useList(arr, "A");
	}
	long endTime = System.nanoTime();
	long duration = endTime - startTime;
	System.out.println("useList:  " + duration / 1000000);
 
 
	//use set
	startTime = System.nanoTime();
	for (int i = 0; i < 100000; i++) 
	{
		useSet(arr, "A");
	}
	endTime = System.nanoTime();
	duration = endTime - startTime;
	System.out.println("useSet:  " + duration / 1000000);
 
 
	//use loop
	startTime = System.nanoTime();
	for (int i = 0; i < 100000; i++) 
	{
		useLoop(arr, "A");
	}
	endTime = System.nanoTime();
	duration = endTime - startTime;
	System.out.println("useLoop:  " + duration / 1000000);
 
 
	//use Arrays.binarySearch()
	startTime = System.nanoTime();
	for (int i = 0; i < 100000; i++) 
	{
		useArraysBinarySearch(arr, "A");
	}
	endTime = System.nanoTime();
	duration = endTime - startTime;
	System.out.println("useArrayBinary:  " + duration / 1000000);
}

```

输出结果:


```
useList:  13
useSet:  72
useLoop:  5
useArraysBinarySearch:  9
```

--------------------------

**Use a larger array (1k) 使用1000个元素的数组:**

```
String[] arr = new String[1000];
 
Random s = new Random();
for(int i=0; i< 1000; i++)
{
	arr[i] = String.valueOf(s.nextInt());
}

```
输出结果：

```
useList:  112
useSet:  2055
useLoop:  99
useArrayBinary:  12
```


--------------------------

**Use a larger array (10k):使用10000个元素的数组**

```

String[] arr = new String[10000];
 
Random s = new Random();
for(int i=0; i< 10000; i++)
{
	arr[i] = String.valueOf(s.nextInt());
}

```
输出结果：

```
useList:  1590
useSet:  23819
useLoop:  1526
useArrayBinary:  12
```
--------------------------


很明显，使用最简单的 for 循环，要比使用其他的 collection 效率更高。很多开发者使用第一种方法 `Arrays.asList(arr).contains(targetValue);`，但此方法效率低下。


`Arrays.binarySearch()`的使用前提是，数组是有序的。
此例子中，数组是无序的，因此，二分搜索不能用在此处。

Actually, if you really need to check if a value is contained in some array/collection efficiently, a sorted list or tree can do it in O(log(n)) or hashset can do it in O(1).

事实上，如果你真的需要高效地检查一个数组或者集合中是否包含某个特定的值，一个有序的数组或者树可以达到 O(log(n))的时间复杂度，HashSet 甚至能达到O(1)的时间复杂度。

