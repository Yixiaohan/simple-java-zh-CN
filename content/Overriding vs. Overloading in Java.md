# Overriding vs. Overloading in Java

![overloading-vs-overriding](http://www.programcreek.com/wp-content/uploads/2009/02/overloading-vs-overriding.png)

覆写和重载（Overriding and Overloading）在 Java 中是两个非常重要的概念。Java 新手程序员经常会他们的概念感到迷惑不解。本文用两个例子讲解二者的差异。

##1. Definitions 定义

重载（Overloading）：一个类里的两个或多个方法的方法名相同，但是参数不同

覆写（Overriding）：意味着两个方法有相同的方法名和参数名（例如，方法签名）。一个方法在父类中，另一个方法在子类中

##2. Overriding vs. Overloading 覆写 vs 重载

一些关键点：

1). The real object type in the run-time, not the reference variable's type, determines which overridden method is used at runtime. In contrast, reference type determines which overloaded method will be used at compile time.

2). 多态适用于覆写, 而对重载却不适用。

3). 覆写是运行（run-time）时的概念，而重载是编译（compile-time）时的概念。

## 3. An Example of Overriding

以下是覆写（Overriding）例子，猜一下输出结果是什么


```
class Dog
{
    public void bark()
    {
        System.out.println("woof ");
    }
}

class Hound extends Dog
{
    public void sniff()
    {
        System.out.println("sniff ");
    }
 
    public void bark()
    {
        System.out.println("bowl");
    }
}
 
public class OverridingTest
{
    public static void main(String [] args)
    {
        Dog dog = new Hound();
        dog.bark();
    }
}
```
输出结果为：`bowl`

In the example above, the dog variable is declared to be a Dog. During compile time, the compiler checks if the Dog class has the bark() method. As long as the Dog class has the bark() method, the code compilers. At run-time, a Hound is created and assigned to dog. The JVM knows that dog is referring to the object of Hound, so it calls the bark() method of Hound. This is called Dynamic Polymorphism.


##4. An Example of Overloading 重载例子

```
class Dog
{
    public void bark()
    {
        System.out.println("woof ");
    }
 
    //overloading method
    public void bark(int num)
    {
    	for(int i=0; i<num; i++)
    		System.out.println("woof ");
    }
}
```
在重载例子中，两个 bark 方法可以使用不同的参数调用。编译器知道这两个方法是不同的，因为这两个方法的方法签名（方法名和参数列表）不同。

References:
1) Defining Method. This tutorial is from Oracle, it explains the components of a method and which of them are used by compiler to differentiate methods.

[本文英文原文地址 http://www.programcreek.com/2009/02/overriding-and-overloading-in-java-with-examples/](http://www.programcreek.com/2009/02/overriding-and-overloading-in-java-with-examples/)


