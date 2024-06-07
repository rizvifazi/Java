
*Date : 04.29.2024*

---
## Sorting Techniques

| Sorting Type | Implementation                                       |
|--------------|------------------------------------------------------|
| List         | `Collections.sort(List l)`                          |
| Set          | Use `TreeSet` class                                 |
| Numbers      | Sorted in ascending order                           |
| Strings      | Sorted in alphabetical order                        |

Example:
```java
List<Employee> l=new ArrayList<>();
empid,ename, salary, age - properties  
```
### Comparable and Comparator Interface

- Used to sort user-defined objects based on their properties rather than sorting its reference.
- `Comparable` provides single sorting sequence, while `Comparator` allows multiple sorting sequences.

| Interface        | `Comparable`                                  | `Comparator`                                                        |
| ---------------- | --------------------------------------------- | ------------------------------------------------------------------- |
| Purpose          | Single sorting sequence based on a property   | Multiple sorting sequences based on different properties            |
| Package          | `java.lang.*`                                 | `java.util.*`                                                       |
| Method Signature | `int compareTo(Object o)`                     | `int compare(Object o1, Object o2)`                                 |
| Usage            | `Collections.sort(List l)`<br>`TreeSet Class` | `Collections.sort(List l, Comparator c)`<br>`TreeSet(Comparator c)` |

### Example Implementations

Student.java
```java
public class Student implements Comparable<Student> {
   Integer id;
   String name;
   Integer age;
public Integer getId() {
              return id;
}
public void setId(Integer id) {
              this.id = id;
}
public String getName() {
              return name;
}
public void setName(String name) {
              this.name = name;
}
public Integer getAge() {
              return age;
}
public void setAge(Integer age) {
              this.age = age;
}
public Student(Integer id, String name, Integer age) {
              super();
              this.id = id;
              this.name = name;
              this.age = age;
}
public Student() {
              super();
              // TODO Auto-generated constructor stub
}
/*@Override
public int compareTo(Student o) {
              if(age==o.age)
                 return 0;
              else if(age>o.age)
                 return 1;
              else
                             return -1;
}*/


@Override
public String toString() {
              return "Student [id=" + id + ", name=" + name + ", age=" + age + "]";
}
@Override
public int compareTo(Student o) {
              return name.compareTo(o.name);
}
   
}
```


Employee.java
```java
public class Employee {
   Integer eid;
   String name;
   Integer age;
public Integer getEid() {
              return eid;
}
public void setEid(Integer eid) {
              this.eid = eid;
}
public String getName() {
              return name;
}
public void setName(String name) {
              this.name = name;
}
public Integer getAge() {
              return age;
}
public void setAge(Integer age) {
              this.age = age;
}
public Employee(Integer eid, String name, Integer age) {
              super();
              this.eid = eid;
              this.name = name;
              this.age = age;
}
public Employee() {
              super();
              // TODO Auto-generated constructor stub
}
@Override
public String toString() {
              return "Employee [eid=" + eid + ", name=" + name + ", age=" + age + "]";
}
   
}


public class NameComparator implements Comparator<Employee>{

              @Override
              public int compare(Employee o1, Employee o2) {
                             return o1.name.compareTo(o2.name);
              }

}

public class IdComparator implements Comparator<Employee> {

              @Override
              public int compare(Employee o1, Employee o2) {
                             if(o1.getEid()==o2.getEid())
                                           return 0;
                             else if(o1.getEid()>o2.getEid())
                                           return 1;
                             else 
                                           return -1;
              }

}


```


Main.java
```java
public class Main {
    public static void main(String[] args) {
        List<Integer> l1=new ArrayList<>();
        l1.add(3);
        l1.add(5);
        l1.add(2);
        l1.add(1);
        System.out.println(l1);  //[3,5,2,1]
        Collections.sort(l1);
        System.out.println(l1); //[1,2,3,5]
        Collections.sort(l1,Comparator.reverseOrder()); //remember
        System.out.println(l1); //[5,3,2,1]
        
        TreeSet<String> ts=new TreeSet<>();
        ts.add("J");
        ts.add("F");
        ts.add("A");
        ts.add("I");
        System.out.println(ts); //[A,F,I,J]
        TreeSet ts1=(TreeSet) ts.descendingSet();
        System.out.println(ts1); //[J,I,F,A]
        
        List<Student> l2=new ArrayList<>();
        l2.add(new Student(103,"Ram",25));
        l2.add(new Student(100,"Raj",21));
        l2.add(new Student(101,"Sam",23));
        l2.add(new Student(104,"Bam",20));
        l2.add(new Student(102,"Tam",24));
        
        Collections.sort(l2);  //internally call compareTo
        for(Student st:l2)
              System.out.println(st);
        
        System.out.println();
        TreeSet<Student> ts2=new TreeSet<>();
        ts2.add(new Student(103,"Ram",25));
        ts2.add(new Student(100,"Raj",21));
        ts2.add(new Student(101,"Sam",23));
        ts2.add(new Student(104,"Bam",20));
        ts2.add(new Student(102,"Tam",24));
        for(Student st:ts2)
              System.out.println(st);
        
        System.out.println();
        
        List<Employee> l3=new ArrayList<>();
        l3.add(new Employee(103,"Ram",25));
        l3.add(new Employee(100,"Raj",21));
        l3.add(new Employee(101,"Sam",23));
        l3.add(new Employee(104,"Bam",20));
        l3.add(new Employee(102,"Tam",24));
        
        Collections.sort(l3,new NameComparator());
        for(Employee e:l3)
              System.out.println(e);
        System.out.println();
        Collections.sort(l3,new IdComparator());
        for(Employee e:l3)
              System.out.println(e);
        
        System.out.println();
        TreeSet<Employee> ts4=new TreeSet<>(new NameComparator());
        ts4.add(new Employee(103,"Ram",25));
        ts4.add(new Employee(100,"Raj",21));
        ts4.add(new Employee(101,"Sam",23));
        ts4.add(new Employee(104,"Bam",20));
        ts4.add(new Employee(102,"Tam",24));
        for(Employee st:ts4)
              System.out.println(st);
    }
}
```

---
## Arrays Class

- Used to perform operations on arrays.
- present in `java.util.*`
- Methods are applicable to all datatype arrays.

#### Syntax:
```java
int a[]=new int[5];
```


#### Constructor
1. Arrays()

| Method                                                   | Description                                  |
| -------------------------------------------------------- | -------------------------------------------- |
| `static List asList(int[] a)`                            | Convert int array to List                    |
| `static void fill(int[] a, int val)`                     | Fill all elements of array with value        |
| `static void fill(int[] a, int start, int end, int val)` | Fill elements with value from start to end-1 |
| `static void sort(int[] a)`                              | Sort all elements of array                   |
| `static void sort(int[] a, int start, int end)`          | Sort elements of array from start to end     |
| `static boolean equals(int[] a1, int[] a2)`              | Check if two arrays are equal                |
| `static int binarySearch(int[] a, int val)`              | Perform binary search on array               |

- Methods are applicable to all datatype arrays.
### Example

```java
public class Main {
    public static void main(String[] args) {
       Integer[] array=new Integer[10];
       for(int i=0;i<10;i++) {
                 array[i]=i*-3;
       }
       for(int arr:array)
                 System.out.println(arr); //0,-3,-6,-9,-12,-15,-18,-21,-24,-27
       
       List l1=Arrays.asList(array);
       System.out.println(l1); //[0,-3,-6,-9,-12,-15,-18,-21,-24,-27]
       
       Arrays.sort(array); //-27,-24,-21,-18,-15,-12,-9,-6,-3,0
       System.out.println(Arrays.binarySearch(array, -15)); //4
       
       //If the value is not present then it returns negative value using -(index)-1
       //-27,-24,-21,-18,-15,-12,-10,-9,-6,-3,0  = -(6)-1
       System.out.println(Arrays.binarySearch(array, -10)); //-7
      //-27,-24,-23, -21,-18,-15,-12,-9,-6,-3,0 = -(2)-1
       System.out.println(Arrays.binarySearch(array, -23)); //-3
       
       Arrays.sort(array); //-27,-24,-21,-18,-15,-12,-9,-6,-3,0
       Arrays.fill(array, -1);//-1,-1,-1,-1,-1,-1,-1,-1,-1,-1
       Arrays.fill(array,2,5,-3);//-1,-1,-3,-3,-3,-1,-1,-1,-1,-1
       Arrays.sort(array); //-3,-3,-3,-1,-1,-1,-1,-1,-1,-1
    }
}
```


- The `array` must be sorted in ascending order for `Arrays.binarySearch` to function correctly.
- The negative return value for absent elements helps determine the appropriate insertion point for maintaining the sorted order.
---

## Map Interface

- Used to store collection of objects in a unique key-value pair.
- Map is **unordered**.

| Return-Type | Method                                            | Description                                                |
| ----------- | ------------------------------------------------- | ---------------------------------------------------------- |
| `void`      | `put(Object k, Object v)`                         | Store single key-value pair                                |
| `void`      | `putAll(Map m)`                                   | Store multiple key-value pairs                             |
| `Object`    | `putIfAbsent(Object k, Object v)`                 | Store if key is not associated with a value                |
| `boolean`   | `containsKey(Object k)`                           | Check if key is present                                    |
| `boolean`   | `containsValue(Object v)`                         | Check if value is present                                  |
| `Object`    | `get(Object k)`                                   | Retrieve value for a key                                   |
| `Object`    | `getOrDefault(Object k, Object default)`          | Retrieve value or default if key not present               |
| `Object`    | `remove(Object k)`                                | Remove entry for a key and return the value                |
| `boolean`   | `remove(Object k, Object v)`                      | Remove entry only if key is associated with a given value  |
| `Object`    | `replace(Object k, Object newvalue)`              | Replace value for a key and return the old value           |
| `boolean`   | `replace(Object k, Object oldval, Object newval)` | Replace value only if key is associated with a given value |
| `boolean`   | `isEmpty()`                                       | Check if map is empty                                      |
| `int`       | `size()`                                          | Get size of the map                                        |

## Map.Entry Interface
- Used to describe the key and value separately.

### Methods
1. `Object getKey()`
2. `Object getValue()`
3. `Object setValue(Object v)`

## SortedMap Interface
- Used to sort the elements of the Map interface.

### Methods
1. `Object firstKey()`
2. `Object lastKey()`
3. `SortedMap subMap(int start, int end)`
4. `SortedMap headMap(Object k)`
5. `SortedMap tailMap(Object k)`

### 3 Classes

### 1. HashMap Class
- Uses Hashing technique to print the value in random order and contains key-value pairs.
- Default capacity: 16
- Allows one null key and any number of null values.

**Syntax:** 
```java
public class HashMap extends AbstractMap implements Map, Cloneable, Serializable
```
#### Constructor
1. `HashMap()`
2. `HashMap(int capacity)`
3. `HashMap(int capacity, float fillratio)`
4. `HashMap(Map m)`

```java
Map<Employee,String> hm=new HashMap<>();
```

Whenever we create an object of HashMap, internally it creates a **bucket from 0 to 15 because the default capacity is 16**. Each bucket internally considered as LinkedList, and each LinkedList contains one node, the internal structure of a **node will have key, value, HashCode, and next.**

```java
Employee e1=new Employee(1,"Ram");
Employee e2=new Employee(2,"Sam");
Employee e3=new Employee(3,"Raj");
Employee e4=new Employee(4,"Tam");

hm.put(e1,"HR");
```

So when we call `put()`, first it will calculate the hashCode for the key using `hashCode()` (i.e., `e1.hashCode() = 2000`). Next, it will calculate the index using `index = hashCode(key) & (n-1)`, resulting in `index = 2000 & (16-1) = 2000 & 15 = 6`. Now it stores `e1` into index 6.

```java
hm.put(e2,"IT");
```

So when we call `put()`, first it will calculate the hashCode for the key using `hashCode()` (i.e., `e2.hashCode() = 1000`). Next, it will calculate the index using `index = hashCode(key) & (n-1)`, resulting in `index = 1000 & (16-1) = 1000 & 15 = 9`. Now it stores `e2` into index 9.

```java
hm.put(e3,"Sales");
```

So when we call `put()`, first it will calculate the hashCode for the key using `hashCode()` (i.e., `e3.hashCode() = 2000`). Next, it will calculate the index using `index = hashCode(key) & (n-1)`, resulting in `index = 2000 & (16-1) = 2000 & 15 = 6`. Now it stores `e3` into index 6.

If the same bucket contains multiple nodes, **then that is called hashing collision**. So, the map will not directly add the entry into the bucket since both keys have the same index. The map will internally call `equals()` and check whether both contents are the same or different. If they are different, it will store the entry into the same bucket, and if they are the same, it will replace the entry.

```java
hm.put(null,"Admin")
```

If we pass the key as null, then the entry will be directly stored in the 0th index.

Before we get elements from HashMap, let's see how searching is done in LinkedList.

```
Start -> item1:P -> item2:P -> item3:P -> item4:P
```

So, in case LinkedList, if we search any value, it will always traverse one by one, which reduces performance. But when we call `hm.get(key)`, first JVM will find the hashcode of the key, and from the hashcode, it will find the bucket index. So, JVM will directly go to the index and find the value. In general, HashMap doesn't have multiple nodes in a single bucket. It should have only one node in one bucket, but there **can be hashing collision where each bucket can have multiple nodes**, so it reduces performance as JVM will traverse one by one. From Java8, HashMap has been enhanced to reduce time when we use `get()`.

```java
Map<Integer,String> hm=new HashMap<>();
hm.put(4,"a");
hm.put(6,"a");
hm.put(2,"a");
hm.put(7,"a");
hm.put(1,"a");
hm.put(5,"a");
hm.put(3,"c");
```

Consider all keys are having the same values, so it will have the same hashcode, so it will have the same index in the bucket which degrades the performance. **From Java8, LinkedList is transformed into a tree structure (self-balancing/red-black tree)** when the number of nodes reaches a certain threshold, that threshold is called the **Treefy threshold.**

```java
Map<Integer,Integer> hm1=new HashMap<>();
hm.put(4,6);
hm.put(6,6);
hm.put(2,2);
hm.put(7,7);
hm.put(1,1);
hm.put(5,5);
hm.put(3,3);
```

```
          7
     6
          5
4
          3
     2
           1
```

In numbers, we know greater or smaller, but if we store strings or any other objects, then JVM will determine whether the particular object is greater or smaller using `compareTo()`.

```java
public class Main {
    public static void main(String[] args) {
       Map<Integer,String> hm=new HashMap<>();
       System.out.println(hm.size()); //0
       hm.put(10, "apple");
       hm.put(13, "grapes");
       hm.put(15, "banana");
       hm.put(16, "Guava");
       hm.put(10, "manago"); //no error, the value will be overridden 
       System.out.println(hm.size()); //4
       System.out.println(hm); //print in curly braces in random order {16=Guava, 10=manago, 13=grapes, 15=banana}
       
       System.out.println(hm.putIfAbsent(20, "melon"));  //null
       System.out.println(hm.putIfAbsent(11, "Berry")); //null
       System.out.println(hm.putIfAbsent(10, "Lime")); //mango
       // {16=Guava, 20=melon, 10=manago, 11=Berry, 13=grapes, 15=banana} Above only puts if key does not contain a value.
       System.out.println(hm.size()); //6
       System.out.println(hm.get(10));  //mango
       System.out.println(hm.get(22)); //null
       System.out.println(hm.getOrDefault(22, "Greenapple")); //Greenapple
       System.out.println(hm.size()); //6
       
       System.out.println(hm.remove(10)); //mango
       System.out.println(hm.get(10)); //null
       System.out.println(hm.remove(11,"Berry")); //true
       System.out.println(hm.get(11)); //null
       System.out.println(hm.remove(13,"Berry")); //false
       System.out.println(hm.get(13)); //grapes
       
       System.out.println(hm.replace(16, "Guava", "Orange")); //true
       System.out.println(hm.get(16)); //Orange
       System.out.println(hm.replace(15, "Pineapple")); //banana
       System.out.println(hm.get(15)); //Pineapple
       System.out.println(hm);
       
       Set set=hm.entrySet();  //convert both key value to Set intf
       Iterator it=set.iterator(); 
       while(it.hasNext()) {
                   Map.Entry me=(Map.Entry)it.next();
                   System.out.println(me.getKey()+" "+me.getValue());
       }
       System.out.println();
       set=hm.keySet();  //convert only keys
       Iterator<Integer> it1=set.iterator();
       while(it1.hasNext()) {
                    Integer key=it1.next();
                    System.out.println(key+" "+hm.get(key));
       }
       
    }
}
```
