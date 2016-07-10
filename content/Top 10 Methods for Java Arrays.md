# Top 10 Methods for Java Arrays

Java 数组常用方法

## 0. Declare an array 声明数组


```
String[] aArray = new String[5];
String[] bArray = {"a","b","c", "d", "e"};
String[] cArray = new String[]{"a","b","c","d","e"};
```

## 1. Print an array in Java 打印数组

```
int[] intArray = { 1, 2, 3, 4, 5 };
String intArrayString = Arrays.toString(intArray);
 
// print directly will print reference value
System.out.println(intArray);
// [I@7150bd4d
 
System.out.println(intArrayString);
// [1, 2, 3, 4, 5]
```

## 2. Create an ArrayList from an array.  array --> arrayList

```
String[] stringArray = { "a", "b", "c", "d", "e" };
ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(stringArray));
System.out.println(arrayList);
// [a, b, c, d, e]
```

## 3. Check if an array contains a certain value 数组中是否包含某个值


```
String[] stringArray = { "a", "b", "c", "d", "e" };
boolean b = Arrays.asList(stringArray).contains("a");
System.out.println(b);
// true
```

## 4. Concatenate two arrays 合并两个数组


```
int[] intArray = { 1, 2, 3, 4, 5 };
int[] intArray2 = { 6, 7, 8, 9, 10 };
// Apache Commons Lang library
int[] combinedIntArray = ArrayUtils.addAll(intArray, intArray2);
```

## 5. Declare an array inline


```
method(new String[]{"a", "b", "c", "d", "e"});
```

##6. Joins the elements of the provided array into a single String


```
// containing the provided list of elements
// Apache common lang
String j = StringUtils.join(new String[] { "a", "b", "c" }, ", ");
System.out.println(j);
// a, b, c
```

##7. Covnert an ArrayList to an array. ArrayList --> array


```
String[] stringArray = { "a", "b", "c", "d", "e" };
ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(stringArray));
String[] stringArr = new String[arrayList.size()];
arrayList.toArray(stringArr);
for (String s : stringArr)
	System.out.println(s);
```
	
	
##8. Convert an array to a set. array --> set

```
Set<String> set = new HashSet<String>(Arrays.asList(stringArray));
System.out.println(set);
//[d, e, b, c, a]
```

## 9. Reverse an array 反转

```
int[] intArray = { 1, 2, 3, 4, 5 };
ArrayUtils.reverse(intArray);
System.out.println(Arrays.toString(intArray));
//[5, 4, 3, 2, 1]
```

## 10. Remove element of an array 删除元素

```
int[] intArray = { 1, 2, 3, 4, 5 };
int[] removed = ArrayUtils.removeElement(intArray, 3);//create a new array
System.out.println(Arrays.toString(removed));
```

##One more - convert int to byte array


```
byte[] bytes = ByteBuffer.allocate(4).putInt(8).array();
 
for (byte t : bytes) {
   System.out.format("0x%x ", t);
}
```

