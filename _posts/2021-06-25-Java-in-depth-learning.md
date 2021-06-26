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
  

# Threading

