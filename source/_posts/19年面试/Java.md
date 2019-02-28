---
title: Java面试
date: 2019-2-26
author: alanJiang
tags:
    - Java
categories:
    - 面试
thumbnail:  /img/thumbnail/hello.jpg
blogexcerpt: Java面试
---


# 一、基本功
## 面向对象特征
封装，继承，多态和抽象

## final, finally, finalize 的区别
### final
1. 修饰类（常亮类）表示类不能派出新的子类，不能被继承。
2. 修饰变量和方法，只能使用，不能修改，常量在初始化的时候必须要初始值，常亮方法不能被重载。
### finally
1. 和异常捕获一起使用，不管try还是catch，最终都会走finally方法体
### finalize
1. 方法是在垃圾收集器删除对象之前对这个对象调用的。


## 重载和重写的区别
### override（重写）
特点
1. 方法名、参数、返回值相同
2. 子类方法不能缩小父类方法的访问权限
3. 子类方法不能抛出比父类方法更多的异常(但子类方法可以不抛出异常)。
4. 方法被定义为final不能被重写。
5. 存在于父类和子类之间。

### overload（重载）
1. 方法名相同，参数类型、个数、顺序至少有一个不相同
2. 存在于父类和子类、同类中

## 抽象类和接口有什么区别
1. 接口是公开的，里面不能有私有的方法或变量，是用于让别人使用的，而抽象类是可以有私有方法或私有变量的
2. 接口所有方法必须被重写，抽象类只有抽象方法必须要被重写。
---
## java反射
主要功能
1. 运行时构建一个类
2. 判断一个类的变量、方法、注解等信息
3. 动态代理，多用于框架
4. 找出某个接口定义的常量和方法注释
5. 反射效率比较低

### 常用于
#### 获取类所有变量信息：
- 获取指定名称变量：mClass.getField("name"),getDeclaredField("test1");
- 获取所有public变量：mClass.getFields();
- 获取所有变量：mClass.getDeclaredFields();
- 获取指定名称方法：mClass.getMethod("name"),getDeclaredMethod("test1");
- 获取所有public方法：mClass.getMethods();
- 获取所有方法：mClass.getDeclaredMethods();
- 获取注释：method.getAnnotation(AnnotationTest01.class);

----

## 自定义注解
### 使用场景
例如登陆、权限拦截、日志处理，以及各种Java框架，如Spring，Hibernate，JUnit 提到注解就不能不说反射。
，Java自定义注解是通过运行时靠反射获取注解。实际开发中，例如我们要获取某个方法的调用日志，可以通过AOP（动态代理机制）给方法添加切面，
通过反射来获取方法包含的注解，如果包含日志注解，就进行日志记录。

### 元注解
#### 1.@Target,
@Target说明了Annotation所修饰的对象范围，可以用在类上，还是用在方法上之类
取值ElementType
> 1.CONSTRUCTOR:用于描述构造器
> 2.FIELD:用于描述域
> 3.LOCAL_VARIABLE:用于描述局部变量
> 4.METHOD:用于描述方法
> 5.PACKAGE:用于描述包
> 6.PARAMETER:用于描述参数
> 7.TYPE:用于描述类、接口(包括注解类型) 或enum声明


#### 2.@Retention,
@Retention定义了该Annotation被保留的时间长短：
取值RetentionPoicy
> 1.SOURCE:在源文件中有效（即源文件保留）
> 2.CLASS:在class文件中有效（即class保留）
> 3.RUNTIME:在运行时有效（即运行时保留）
#### 3.@Documented,
@Documented用于描述其它类型的annotation应该被作为被标注的程序成员的公共API,标记型注解，没有成员

#### 4.@Inherited
@Inherited 元注解是一个标记注解，@Inherited阐述了某个被标注的类型是被继承的。
例如父类有该注解，那么子类也会继承该注解

### 自定义注解
@interface自定义注解时，自动继承了java.lang.annotation.Annotation接口

default来声明参数的默认值

    定义注解格式：
    　　public @interface 注解名 {定义体}
    
    　　注解参数的可支持数据类型：
    
    　　　　1.所有基本数据类型（int,float,boolean,byte,double,char,long,short)
    　　　　2.String类型
    　　　　3.Class类型
    　　　　4.enum类型
    　　　　5.Annotation类型
    　　　　6.以上所有类型的数组















---
{% raw %}
<style>
qq {
     padding: 2px 4px;
     font-size: 90%;
     color: #c7254e;
     background-color: #f9f2f4;
     border-radius: 4px;
 }
</style>
{% endraw %}

---

## session 与 cookie 区别
cookie 是 Web 服务器发送给浏览器的一块信息。浏览器会在本地文件中给每一个 Web 服务器存储 cookie,
session是会话，客户端可以关闭cookie功能，但是无法关闭session功能。

---

## MVC 设计思想
M:Model 模型
V:View 视图
C:Controller 控制器

---

## 集合
### List和Set
#### 区别
    List,Set都是继承自Collection接口
    List特点：元素有放入顺序，元素可重复
    Set特点：元素无放入顺序，元素不可重复，重复元素会覆盖掉(元素虽然无放入顺序，但是元素在set中的位置是有该元素的HashCode决定的，其位置其实是固定的，加入Set 的Object必须定义equals()方法 ，)
#### 对比
    Set：检索元素效率低下，删除和插入效率高，插入和删除不会引起元素位置改变。
    List：和数组类似，List可以动态增长，查找元素效率高，插入删除元素效率低，因为会引起其他元素位置改变。
### Arraylist 与 LinkedList  和 Vector
- Arraylist：
    - 优点：ArrayList是实现了基于动态数组的数据结构,因为地址连续，一旦数据存储好了，查询操作效率会比较高（在内存里是连着放的）
    - 缺点：因为地址连续， ArrayList要移动数据,所以插入和删除操作效率比较低。
- LinkedList：
    - 优点：基于链表的数据结构,地址是任意的，在开辟内存空间的时候不需要等一个连续的地址，对于新增和删除操作add和remove，LinedList比较占优势，LinkedList 适用于要头尾操作或插入指定位置的场景
    - 缺点：因为LinkedList要移动指针,所以查询操作性能比较低。
- Vector：
    - 优点：和ArrayList原理相同，但是是线程安全的
    - 缺点：效率比较略低
### 总结
- collocation：单列集合
    - list:有存储顺序, 可重复
        - ArrayList:
        - LinkedList:
        - Vector:
    - set:无存储顺序, 不可重复
        - HashSet: 利用HashMap的key来实现hashSet
        - TreeSet: 和hashset一样，利用treemap来实现
        - LinkedHashSet: LinkedHashSet 维护着一个运行于所有条目的双重链接列表。此链接列表定义了迭代顺序，该迭代顺序可为插入顺序或是访问顺序。继承与 HashSet、又基于 LinkedHashMap 来实现的（16,0.75）
- Map:键值对
    - HashMap：key允许有null值，key不能重复，value可以，无序，当容量大于设定负载因子的量时，会调整容量为当前2倍，默认0.75
    - TreeMap：TreeMap是一个能比较元素大小的Map集合，会根据传入key的大小进行排序，可以插入null键，null值，可以对元素进行排序,想要自定义顺序，就需要实现Comparable接口的compareTo方法
    - HashTable：同步的，而HashMap是非同步的,线程是安全的，效率上比HashMap要低。不允许key为null
    - LinkedHashMap：是hashMap的之类，它保留插入的顺序，如果需要输出的顺序和输入时的相同。
    - ConcurrentHashMap：线程安全的HashMap的实现。对整个桶数组进行了分割分段(Segment)，每一个分段上都用lock锁进行保护，锁更细腻，性能比hashtable高，ConCurrentHashMap key不允许为null。
    
## 线程
### 创建线程的方式
Java中创建线程主要有三种方式
#### 1.继承Thread类创建线程类，重写run方法
```java
public class FirstThreadTest extends Thread{
    int i = 0;
    //重写run方法，run方法的方法体就是现场执行体
    public void run()
    {
        for(;i<100;i++){
          System.out.println(getName()+"  "+i);
        }
    }
    public static void main(String[] args)
    {
        for(int i = 0;i< 100;i++)
        {
            System.out.println(Thread.currentThread().getName()+"  : "+i);
            if(i==20)
            {
                new FirstThreadTest().start();
                new FirstThreadTest().start();
            }
        }
    }
}
```
#### 2.通过Runnable接口创建线程类,重写run()方法
```java
public class RunnableThreadTest implements Runnable
{
    private int i;
    public void run()
    {
        for(i = 0;i <100;i++)
        {
            System.out.println(Thread.currentThread().getName()+" "+i);
        }
    }
    public static void main(String[] args)
    {
        for(int i = 0;i < 100;i++)
        {
            System.out.println(Thread.currentThread().getName()+" "+i);
            if(i==20)
            {
                RunnableThreadTest rtt = new RunnableThreadTest();
                new Thread(rtt,"新线程1").start();
                new Thread(rtt,"新线程2").start();
            }
        }
    }
}
```

#### 3.通过Callable和Future创建线程,并实现call()方法
```java
public class CallableThreadTest implements Callable<Integer>
{
 @Override
    public Integer call() throws Exception
    {
        int i = 0;
        for(;i<100;i++)
        {
            System.out.println(Thread.currentThread().getName()+" "+i);
        }
        return i;
    }
}
```

### sleep() 、join（）、yield（）有什么区别
#### sleep
指定线程休眠多少毫秒，让其他线程有机会执行，不会释放对象锁，
#### yield
使当前线程重新回到可执行状态,回到可执行状态后，又会马上被执行，但是只能是同级以上的线程获得执行机会。
#### join
Thread的非静态方法join()让一个线程B“加入”到另外一个线程A的尾部。在A执行完毕之前，B不能工作。


## 浅拷贝、深拷贝

# JVM
# Java 内存模型
# 锁
