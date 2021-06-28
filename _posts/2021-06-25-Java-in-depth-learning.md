---
layout:     post
title:      Java 
subtitle:   String, stack, heap, threading...
date:       2021-06-25
author:     Shuo Wang
header-img:  img/post-bg-java-log.jpeg
catalog: true
tags:
    - Java
    - 
    - 
    - 
---

# The difference between '==' and 'equals'
1. if it compares the primitive data type, it will compare the value directly.  
2. if it compares the reference type, it will compare to the memory address. For the data type of String, when the variable of String has been created, it will be saved as a constant (String pool) that is not modifiable. redirect the name to another variable, it will point to another memory address.  
For example,  
```java
String str1 = "abc";
String str2 = new String("abc")
System.out.print(str1 == str2) result = False
```
Because when people want to compare String in two variables, it is hard to decide the name of a variable is to point to 'constant' or 'new memory space'. '==' can compare the address, but we want to compare is it the same value for two String variables. Thus, use .equals() to compare to String.  

# The difference between authentication and authorization
authentication(认证): to verify you is you, such as account and password.  
authorization(授权): to confirm your permissions, such as the admin and normal users.

# Heap(堆), Stack(栈) and Method Area
Heap:  
1.FIFO(First Input First Output: Queue).  
2.one Heap zone is shared by all the threading.  
3.Heap is located in the L2 cache in CPU, lower than Stack.  
4.for all the 'new object or array'.  
5.Can allocate the memory size dynamically, life cycle is not confirmative. However, lower speed.  
Stack:  
1.FILO(First Input Last Output).  
2.A place to temporarily store data, each threading will contain one Stack zone.  
3.Stack is saved in L1 cache in CPU, faster read and write speed.  
4.for the address of primitive data type and reference variable.  
5.faster speed, but the life cycle and the size of data must be determined. not flexible.  
![picture1](/img/Java/heapstack.png)
Method Area:  
This place is for method and static variable.

# Swtich method(data type?)
It can only be String, char, or int.
  
# Access modifier for Class(Default and public)
1. Public: The class is accessible by any other class.  
2. Default: The class is only accessible by classes in the same package. This is used when you don't specify a modifier.
3. In the inner class, it can use 'private' or 'protected' modifier.

# ArrayList and LinkedList?
Use an ArrayList when:  
1. You want to access random items frequently;
2. You only need to add or remove elements at the end of the list.  
Use a LinkedList when:  
1. You only use the list by looping through it instead of accessing random items;
2. You frequently need to add and remove items from the beginning, middle or end of the list.  
[Manual Implementation codes](https://github.com/JadeSure/Data-Structure-and-Algorithm/tree/main/Project1%20Binary%20Space%20Partitioning%20(BSP))

# Iterator
Iterator is an object that can be used to loop through collections. It is called an "iterator" because "iterating" is the technical term for looping, which is designed to easily change the collections that they loop through.
```java
import java.util.ArrayList;
import java.util.Iterator;

public class Main {
  public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();
    numbers.add(12);
    numbers.add(8);
    numbers.add(2);
    numbers.add(23);
    Iterator<Integer> it = numbers.iterator();
    while(it.hasNext()) {
      Integer i = it.next();
      if(i < 10) {
        it.remove();
      }
    }
    System.out.println(numbers);
  }
}
```
Because the collection is changing size at the same time that the code is trying to loop, it cannot use a for loop or a for-each loop to remove items.(remove())

# throw and throws
throw: used to throw an exception for a method, but it cannot throw multiple exceptions.(used inside the method). 
throws: used to indicate what exception type my be thrown by a method, it can declare mutliple exceptions.(used with the method signature).

# Process and Thread
1. One process has multiple threads. A thread is a smallest part of the process that can execute concurrently with other threads of the process.  
2. A program in execution is often referred as process. A thread is a subset of the process.  
3. Threading is the basic unit of cpu scheduling, which can complete a separate program control flow.  
4. Process is isolated from each other, which is located in the isolated RAM space.(Hack) However, threads that from the same process can share the same RAM space.  
5. There is an priority for both threading and processing.  
6. Two Ways of Implementing Treading(interface Runnable and inheritance Thread).  
7. The priority is only determing the processing probability of threading. No guarantee.  
8. In order to avoid competing, the higher priority threading can call sleep() or yield() method to give a chance for system to run lower or the same level of priority.
9. `thread.setDaemon(true)` 守护者

### Threading method
1. Join(): force current threading to stop and wait other threadings finished. Then, implement current threading
```java
public class JoinDemo {

   public static void main(String [] args) throws InterruptedException {
       Thread printTask = new Thread(new PrintNumTask(), "printThreading");
       printTask.start();

       for (int i = 0; i<50; i++){
           if (i == 33){
               printTask.join();
           }
           System.out.println("main threading to print numbers "+i);
       }
   }
}

class PrintNumTask implements Runnable{

   @Override
   public void run() {
       for(int i = 0; i<10; i++){
           System.out.println(Thread.currentThread().getName()+"printed number "+ i);
       }
   }
}

```
2. Thread.yield()
allow other threadings that have the same priority to process first. Current threading will turn to ready status.(may not be success)
```java
public class YieldDemo {
   public static void main(String[] args){
       Thread temp1 = new Thread(new PrintNum(), "testYield1");
       Thread temp2 = new Thread(new PrintNum(), "testYield2");

       temp1.start();
       temp2.start();
   }
}

class PrintNum implements Runnable{

   @Override
   public void run() {
       for(int i = 0; i<100; i++){
           if (i==20){
               System.out.println(Thread.currentThread().getName()+" allow others");
               Thread.yield();
           }
           System.out.println(Thread.currentThread().getName()+"printed number "+ i);
       }
   }
}
```
3. thread.setDaemon(true) make sure the main threading will not be stopped because when there is no any non-daemon threading, the main threading will finished(JVM quit);  
The garbage collection machanism is handled by daemon threading;  
Daemon threading cannot handle the resources that need to be closed, such as file resources.

```java
public class YieldDemo {
   public static void main(String[] args){
       Thread temp1 = new Thread(new PrintNum(), "testYield1");
       Thread temp2 = new Thread(new PrintNum(), "testYield2");
       
       temp1.setDaemon(true);
       temp2.setDaemon(true);
       
       temp1.start();
       temp2.start();
       
       Thread.sleep(1000);
   }
}

class PrintNum implements Runnable{

   @Override
   public void run() {
       for(int i = 0; i<100; i++){
           if (i==20){
               System.out.println(Thread.currentThread().getName()+" allow others");
               Thread.yield();
           }
           System.out.println(Thread.currentThread().getName()+"printed number "+ i);
       }
   }
}
```
4. thread.interrupt() mark a stop point for the application

### Threading KeyWords: synchronized
In order to lock resources that one thread can access this method at this moment.(Lock a thread)
```java
public synchronized void beAttacted(long attack){
    if(hp > 0) hp -= attack;
}
or

public void beAttacked(long attack){
    synchronized(this){
        if(hp>0) hp -= attack;
    }
 }
```
1. One synchronized method need a lock before implementing util it has finished. Other threadings is in blocking. For instance method, it needs to lock the instance(block codes).   
2. static method needs to add a lock for the static class. 
|List|Table|String|Threading|
|:----:|:----:|:----:|
|ArrayList|HashMap|StringBuilder|Not Safe|
|Vector|HashTable|StringBuffer|Safe|
For ArrayList and Vector, when the memory is not enough, ArrayList * 150% / Vector * 200%.  
HashMap allows null for both key and values. However, reversed results for HashTable.  
