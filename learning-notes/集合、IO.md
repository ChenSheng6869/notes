# 1 集合

```java
package com.chen.collectiontest;

import org.junit.Test;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collection;

public class CollectionTest {

    @Test
    public void test1(){
        Collection coll = new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(false);
        coll.add(new Person("Jerry",20));
//        Person p = ;
//        coll.add(p);

        boolean contains = coll.contains(123);
        System.out.println(contains);

//        System.out.println(coll.contains(p));
        System.out.println(coll.contains(new Person("Jerry",20)));
    }

    @Test
    public void test2(){
        //3.remove(Object obj)
        Collection coll = new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new Person("Tom",20));
        coll.add(false);
        coll.add(new Person("Jerry",20));
        System.out.println(coll);
        System.out.println(coll.remove(1234));
        coll.remove(new Person("Jerry",20));
        System.out.println(coll);

        //4.removeAll(Collection coll1) 从当前集合中移除coll中所有的元素
        Collection coll1 = Arrays.asList(123,456);
        coll1.removeAll(coll1);
        System.out.println(coll1);
    }
}

```

## 1.2 ArrayList、LinkedList及Vector异同点

```
/**
 *  Collection接口：单列集合，用来存储一个一个的对象
 *  list接口：存储有序的、可重复的数据
 *
 *  |----->ArrayList：作为；list接口的主要实现类（执行效率高，线程不安全），底层使用Object[]存储 elementData存储
 *  |----->LinkedList：对于频繁的插入删除操作，使用此类效率比ArrayList效率高，底层使用的双向链表存储
 *  |----->Vector：作为list接口的古老实现类（线程安全，效率低），底层使用Object[]存储 elementData存储
 *
 *  面试题：三者的异同
 *  相同点：三个类都是先了list接口，存储数据的特点相同
 *  不同：见上
 *  LinkedList list = new LinkedList();
 *  内部声明了Node类型的first和last属性，默认值为null
 *  list.add(123); //将123封装到Node中，创建Node对象 
 */
```

## 1.3 ArrayList源码分析

## 1.3 Set

```java
package com.chen.settest;

public class User {
    private String name;
    private int age;

    public User(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        System.out.println("User equals()...");
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        User user = (User) o;

        if (age != user.age) return false;
        return name != null ? name.equals(user.name) : user.name == null;
    }

    @Override
    public int hashCode() {//return name.hashCode() + age;
        int result = name != null ? name.hashCode() : 0;
        result = 31 * result + age;
        return result;
    }
}
```

```java
package com.chen.settest;


import org.junit.Test;

import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

/**
 *  Set接口的框架
 *  Set接口：存储无需的、不可重复的数据   -->    集合
 *  HashSet：作为Set接口的主要实现类；线程不安全的，可以存储null值
 *  LinkedHashSet：作为HashSet的子类；遍历其内部数据时，可以暗战添加的顺序遍历
 *  TreeSet：可以按照添加对象的指定属性，进行排序。
 *
 *  1.Set接口中没有额外定义新的方法啊，使用的都是Collection
 *  2.要求：向Set中添加的数据，其所在的类一定要重写hashCode（）和equals（）
 *          重写的hashCode（）和equals（）尽可能保持一致性。（相等的对象必须具有相等的散列码）
 */
public class SetTest {

    /*
        一、Set：存储无序的、不可重复的数据
        以HashSet为例说明：
            1.无序性：不等于随机性。存储的数据在底层数组中并非按照数组索引的顺序添加，
                                而是根据数据Hash值存储的。

            2.不可重复性：保证添加的元素按照equals()判断是，不能返回true，即相同的元素只能添加一个

        二、添加元素的过程：以HashSet为例：
            我们想HashSet中添加元素a,首先调用元素a所在类的hashCode()方法，计算元素a的哈希值，
            此哈希值接着用过某种算法计算出在Hash底层数组中的存放位置，判断数组此位置上是否已经有元素：
                如果此位置上没有其他元素，则元素a添加成功。  ---> 情况1
                如果此位置上有其他元素b（或者以链表形式存在的多个元素），则比较元素a与元素b的hash值：
                如果hash值不相同，则元素a添加成功           ---> 情况2
                如果hash值相同，进而需要调用元素a所在类的equals()方法：
                    equals（）返回True，元素a添加失败
                    equals（）返回false，则元素a添加成功。  ---> 情况3

                对于添加成功的情况2和情况3而言：元素a与已经存在指定索引位置上数据以链表方式存储。
                jdk7：元素a放到数组中，指向原来的元素。
                jdk8：原来的元素在数组中，指向元素a

          HashSet底层：数组+链表的结构。
     */
    @Test
    public void test1(){
        Set set = new HashSet();
        set.add(456);
        set.add(123);
        set.add("AA");
        set.add("BB");
        set.add(new User("Tom",12));
        set.add(new User("Tom",12));
        set.add(129);
        set.add(129);
        Iterator iterator = set.iterator();
        while (iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }
}
```

## 1.4 HashMap底层实现原理

```java
package com.chen.maptest;

import org.junit.Test;

import java.util.HashMap;
import java.util.Map;

/**
 *  一、Map:双列数据，存储key-->value对的数据      ---类似于高中的函数y=f(x)
 *      HashMap:作为Map的主要实现类；线程不安全，效率高；存储null的key和value
 *          LinkedHashMap:保证在遍历map元素时，可以按照添加的顺序实现遍历。
 *                        原因：在原有的HashMap底层结构基础上，添加了一堆指针，指向前一个和后一个元素。
 *                        对于频繁的遍历操作，此类执行效率高于HashMap
 *      TreeMap:保证按照添加的key-value对进行排序，实现排序遍历。此时考虑key的自然排序或定制排序
 *      Hashtable:作为古老的实现类，线程安全，效率低；不能存储null的key和value
 *          Properties：常用来处理配置文件。key和value都是String类型
 *
 *      HashMap底层：数组+链表（jdk7之前）
 *                   数组+链表+红黑树（jdk 8，为了提升效率）
 *
 *   面试题：
 *   1.HashMap的底层实现原理？
 *   2.HashMap和Hashtable的异同？
 *   3.CurrentHashMap与Hashtable的异同？
 *
 *  二、Map结构的理解
 *      Map中的key：无序、不可重复，使用Set存储所有的key--->key所在的类要重写equals和hashCode
 *      Map中的value：无序、可重复，使用Collection存储所有的value--->valyue所在的类要重写equals
 *      一个键值对：key-value构成了一个Entry对象。
 *      Map中的entry：无序、不可重复，使用Set存储所有entry
 *
 *  三、HashMap的底层实现原理？以jdk7为例说明：
 *      HashMap map = new HashMap();
 *      在实例化后，底层创建了长度是16的一维数组Entry[] table
 *      ...可能已经执行过多次put...
 *      map.put(key1,value1):
 *       首先调用key1所在类的hashCode方法计算key1哈希值，此哈希值经过计算后，得到在Entry数组中的存放位置
 *       如果此位置上数据为空，此时的key1-value1添加成功 ---> 情况1
 *       如果此位置上的数据不为空，意味着此位置上存在一个或多个数据（以链表形式存在），比较key1和已经存在的
 *       一个或多个数据的哈希值:
 *                      如果key1的哈希值与已经存在的数据的哈希值都不相同，此时key1-value1添加成功 ---> 情况2
 *                      如果key1的哈希值与已经存在的某一个数据哈希值相同，继续比较：调用key1所在类的equals方法
 *                      比较：
 *                          如果equals返回false：key1-value1添加成功 ---> 情况3
 *                                    返回true：将value1替换相同key的value值
 *              补充：关于情况2和情况3：此时key1-value1和原来的数据以链表的方式存储
 *              在不断的添加过程中，会涉及到扩容问题，默认的扩容方式：扩容为原来容量的2被，并将原有的数据复制过来。
 *
 *       jdk8相较于jdk7在底层实现方面的不同：
 *       1. new HashMap()：底层没有创建一个长度为16的数组
 *       2.jdk 8底层数组是：Node[], 而非Entry[]
 *       3.首次调用put方法时，底层创建长度为16的数组
 *       4.jdk7底层：数组+链表     jdk8：数组+链表+红黑树
 *          当数组的某一个索引位置上的元素以链表形式存在的数据个数 > 8 且当前数组的长度 > 64，此时索引位置
 *          上的所有数据改为红黑树存储。
 *
 */
public class MapTest {
    @Test
    public void test1(){
        Map map = new HashMap();
//        map = new Hashtable();
        map.put(null,123);
    }
}
```

# 2 Java泛型

## 2.1 关于泛型的几个Question

> 1.什么是泛型？
>
> 泛型的本质是参数化类型，对所操作的数据类型指定为一个参数。
>
> 2.什么时候用泛型？
>
> 假设有一个需求是写一个排序方法，能够对整形数组、字符串数组甚至其他任何类型的数组进行排序，可以考虑使用泛型实现。
>
> 使用Java泛型的概念，可以写一个泛型方法来对一个对象数组排序。然后调用该泛型方法对整型数组、浮点数数组、字符穿数组等进行排序。

## 2.2 泛型方法

泛型方法在调用时可以接收不同类型的参数。根基传递给泛型方法的参数类型，编译器适当的处理每一个方法方法调用。

### 2.2.1 有界的类型参数

extends用法：











