---
title: Java异常
date: 2020-08-27 23:41:12
categories: 
           - java基础
tags:
           - 异常
---

## 1.什么是异常

> 异常是指程序运行中出现的不期而至的各种状况，如：文件找不到、网络连接失败、非法参数等。
>
> 异常发生在程序运行期间，它影响了正常的程序执行。

**分类**

- 检查形异常

- 运行时异常

- 错误ERROR

## 2.异常体系结构

> Java把异常当作对象来处理，并定义一个基类java.lang.Throwable作为所有异常的超类。
>
> 在Java API中已经定义了许多异常类，这些异常类分为两大类，错误Error和异常Exception

![异常体系结构](https://tva1.sinaimg.cn/large/007S8ZIlly1gg98nyiy88j31780r00ze.jpg)

### 2.1 Error

> 由Java虚拟机生成并抛出，大多数错误与代码编写者所执行的操作无关。这些错误是不可查的，因为它们在应用程序的控制和处理能力之外，而且绝大多数时程序运行时不允许出现的状况。

- 例如Java虚拟机运行错误，当JVM不再有继续执行操作所需的内存资源时，出现OutOfMemoryError

### 2.2 Exception

> 这些异常一般是由程序逻辑错误引起的。这些异常是不检查异常，程序可以选择捕获处理，也可以不处理。

- 在Exception分支中有一个重要的子类RuntimeException（运行时异常），例如NullPointerException（空指针异常）、ClassNotFoundException（找不到类）等异常。

### 2.3 Error和Exception的区别

Error通常是灾难性的致命错误，程序无法处理和控制，JVM一般选择终止线程

Exception通常情况下是可以被程序处理的，并且在程序中应该尽可能去处理。

## 3.处理异常

**关键字：try 、catch、finally**

```java
public static void main(String[] args) {
  int a = 1;
  int b = 0;
  try {
    System.out.println(a/b);
  } catch(Exception exception){
    System.out.println("出现异常 : " + exception);
  } finally {
    // 做一些善后工作，一定会执行
    System.out.println("finally执行了");
  }
}
```

**关键字throw**、**throws**

主动抛出异常，一般在方法中使用

```java
public class Demo03 {
    public static void main(String[] args) {
        int a = 1;
        int b = 0;
        try {
            new Demo03().test(a, b);
        } catch (Exception e) {
            System.out.println("异常：" + e);
        }
    }
    // 假设这个方法处理不了，就向上抛出
    public void test(int a,int b) throws Exception{
        if(b==0){
            // 主动抛出异常
            throw new Exception();
        }
        System.out.println(a/b);
    }
}
```

## 4.自定义异常

> 用户自定义异常类，继承Exception类即可
>

```java
public class MyException extends Exception{
    // 传递数字 > 10
    private int detail;

    // 构造函数
    public MyException(int detail) {
        this.detail = detail;
    }

    // 异常打印信息
    @Override
    public String toString() {
        return "MyException{" +
                "detail=" + detail +
                '}';
    }
}
```

```java
public class Demo04 {
    public static void main(String[] args) {
        try {
            test(11);
        } catch (MyException e) {
            System.out.println("异常:" + e);
        }
    }
    
    // 可能存在异常的方法
    static void test(int a) throws MyException {
        if( a>10 ) {
            throw new MyException(a);
        }
    }
}
/*
结果
异常:MyException{detail=11}
*/
```