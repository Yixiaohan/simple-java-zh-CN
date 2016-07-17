# Frequently Used Methods of Java HashMap
HashMap 常用方法


作为计数器：

```
HashMap<String, Integer> countMap = new HashMap<String, Integer>();
 
//.... a lot of a's like the following
if(countMap.keySet().contains(a))
{
	countMap.put(a, countMap.get(a)+1);
}
else
{
	countMap.put(a, 1);
}
```

## 1. Loop Through HashMap 循环

```
Iterator it = mp.entrySet().iterator();
while (it.hasNext()) 
{
    Map.Entry pairs = (Map.Entry)it.next();
    System.out.println(pairs.getKey() + " = " + pairs.getValue());
}
```


```
Map<Integer, Integer> map = new HashMap<Integer, Integer>();
for (Map.Entry<Integer, Integer> entry : map.entrySet()) 
{
    System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
}
```


## 2. Print HashMap 打印

```
public static void printMap(Map mp) 
{
    Iterator it = mp.entrySet().iterator();
    while (it.hasNext()) 
    {
        Map.Entry pairs = (Map.Entry)it.next();
        System.out.println(pairs.getKey() + " = " + pairs.getValue());
        it.remove(); // avoids a ConcurrentModificationException 新手经常会犯的错
    }
}
```

##3. Sort HashMap by Value 按值排序

The following code example take advantage of a constructor of TreeMap here.

以下例子，充分利用了 TreeMap 的构造方法：

```
class ValueComparator implements Comparator<String> 
{
 
    Map<String, Integer> base;
 
    public ValueComparator(Map<String, Integer> base) 
    {
        this.base = base;
    }
 
    public int compare(String a, String b)
     {
        if (base.get(a) >= base.get(b))
        {
            return -1;
        } 
        else 
        {
            return 1;
        } // returning 0 would merge keys
    }
}
```


```
HashMap<String, Integer> countMap = new HashMap<String, Integer>();
//add a lot of entries
countMap.put("a", 10);
countMap.put("b", 20);
 
ValueComparator vc =  new ValueComparator(countMap);
TreeMap<String,Integer> sortedMap = new TreeMap<String,Integer>(vc);
 
sortedMap.putAll(countMap);  
 
printMap(sortedMap);
```

-------------------------

[译者著 StackOverflow 上的一个问答： sort-a-mapkey-value-by-values-java](http://stackoverflow.com/questions/109383/sort-a-mapkey-value-by-values-java)

Here's a generic-friendly version you're free to use:

```
import java.util.*;

public class MapUtil
{
    public static <K, V extends Comparable<? super V>> Map<K, V> 
        sortByValue( Map<K, V> map )
    {
        List<Map.Entry<K, V>> list =
            new LinkedList<Map.Entry<K, V>>( map.entrySet() );
        Collections.sort( list, new Comparator<Map.Entry<K, V>>()
        {
            public int compare( Map.Entry<K, V> o1, Map.Entry<K, V> o2 )
            {
                return (o1.getValue()).compareTo( o2.getValue() );
            }
        } );

        Map<K, V> result = new LinkedHashMap<K, V>();
        for (Map.Entry<K, V> entry : list)
        {
            result.put( entry.getKey(), entry.getValue() );
        }
        return result;
    }
}
```


