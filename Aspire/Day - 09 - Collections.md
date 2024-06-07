
*Date : 04.29.2024*

   - If we want to sort the elements of List interface we have to use Collections.sort(List l)
   - If we want to sort the elements of Set interface we have to use TreeSet class
   - If it is numbers then it will be sorted in ascending order and String means it will be sorted in alphabetical order

List<Employee> l=new ArrayList<>();
empid,ename, salary, age - properties  
 
Comparable and Comparator interface
     - If ur List or Set contains collection of user defined object like Employee, Student, Person etc, now we want to sort based on their properties rather than sorting its reference 

Comparable interface                       Comparator interface
1. provides single sorting           1. provides multiple sorting sequence(ie)
sequence (ie) we can do sorting      we can do sorting based on empid and 
only based on one property either    ename and salary and age
by empid or ename or salary
or age

2. present in java.lang.*            2. present in java.util.* package
package

3. int compareTo(Object o)           3. int compare(Object o1, Object o2)

4. If we do sorting using            4. If we do sorting using Comparator
Comparable interface for List        intf for List we have to use
we have to use                       Collections.sort(List l, Comparator c)
Collections.sort(List l)             and for Set intf we have to use
and for Set intf we have to          TreeSet(Comparator c) 
use TreeSet class


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
        Collections.sort(l1,Comparator.reverseOrder());
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

Arrays class
     - used to perform operation on datatype array 
     - present in java.util.*

int a[]=new int[5];

Constructor
1. Arrays()

Methods
1. static List asList(int[] a) - convert int array to List 
2. static void fill(int[] a, int val) - fill all elts of array with val
3. static void fill(int[] a,int start, int end, int val) - fill elts with val from start to end-1
4. static void sort(int[] a) - sort all elts of array
5. static void sort(int[] a, int start, int end) sort elts of array from start to end
6. static boolean equals(int[] a1, int[] a2)
7. static int binarySearch(int[] a, int val)

These methods are applicable for all datatype arrays

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

Map interface
     - used to store collection of object but in the form of unique key value pair
     - Map is unordered

Methods
1. void put(Object k, Object v) - store single key value pair
2. void putAll(Map m) - store multiple key value pair
3. Object putIfAbsent(Object k, Object v) - if specified key is not associated with the value, then it associates the key with given value and returns null
4. boolean containsKey(Object k)
5. boolean containsValue(Object v)
6. Object get(Object k) - if we provide the key, it will return value associated with the key
7. Object getOrDefault(Object k, Object defaultvalue)-if key is not associated with any value then by default it returns null, instead we can return some default value
8. Object remove(Object k) - If we provide the key, it will remove value associated with that key and return the value
9. boolean remove(Object k, Object v)
10. Object replace(Object k, Object newvalue) - replace value for the key and returns old value
11. boolean replace(Object k, Object oldval, Object newval)
12. boolean isEmpty()
13. int size()

We cant apply Iterator interface directly on Map interface, we have convert Map to Set interface 
14. Set entrySet() - convert both key and value to Set interface
15. Set keySet() - convert only key to Set interface

Map.Entry interface
    - used to describe the key and value separately
Methods
1. Object getKey()
2. Object getValue()
3. Object setValue(Object v)

SortedMap interface
    - used to sort the etls of Map interface
Methods
1. Object firstKey()
2. Object lastKey()
3. SortedMap subMap(int start, int end)
4. SortedMap headMap(Object k)
5. SortedMap tailMap(Object k)

3 classes
1. HashMap class
       - uses Hashing technique to print the value in random order and contains key value pair
       - default capacity 16
       - allow one null key and any  number null values

Syntax: public class HashMap extends AbstractMap implements Map, Cloneable, Serializable

Constructor
1. HashMap()
2. HashMap(int capacity)
3. HashMap(int capacity, float fillratio)
4. HashMap(Map m)

Map<Employee,String> hm=new HashMap<>();

So whenever we create object of HashMap, internally it create a bucket from 0 to 15 because default capacity is 16. Each bucket internally considered as LinkedList, and each LinkedList contains one node, the internal structure of node will have key,value,hashcode and next 

Employee e1=new Employee(1,"Ram");
Employee e2=new Employee(2,"Sam");
Employee e3=new Employee(3,"Raj");
Employee e4=new Employee(4,"Tam");

hm.put(e1,"HR");

So when we call put(), first it will calculate the hashcode for the key using hashCode (ie) e1.hashCode() = 2000
Next it will calculate the index using index=hashCode(key) & (n-1)
                                            = 2000 & (16-1) = 2000 & 15 = 6

now it stores e1 into index 6

hm.put(e2,"IT");

So when we call put(), first it will calculate the hashcode for the key using hashCode (ie) e2.hashCode() = 1000
Next it will calculate the index using index=hashCode(key) & (n-1)
                                            = 1000 & (16-1) = 1000 & 15 = 9

now it stores e2 into index 9

hm.put(e3,"Sales");

So when we call put(), first it will calculate the hashcode for the key using hashCode (ie) e3.hashCode() = 2000
Next it will calculate the index using index=hashCode(key) & (n-1)
                                            = 2000 & (16-1) = 2000 & 15 = 6

now it stores e3 into index 6

If same bucket contains multiple node then that is called hashing collision, so map will not directly add the entry into the bucket since both key have same index, map will internally call equals() and check whether both content are same or different, if it is different then it will store the entry into same bucket and if it is same it will replace the entry 

hm.put(null,"Admin")
   - If we pass key as null, then entry will be directly stored in 0th index

Before we get elts from HashMap, we see how searching is done in LinkedList

Start -> item1:P -> item2:P -> item3:P -> item4:P

So in case LinkedList if we search any value it will always traverse one by one which reduces the performance
   But when we call hm.get(key), first JVM will find the hashcode of key and from hashcode it will find the bucket index, so JVM will directly goes to the index and find the value 
   In general, HashMap dosent have multiple nodes in single bucket, it should have only one node in one bucket, but there can be hashing collision where each bucket can have multiple nodes, so it reduce performance as JVM will traverse one by one
   From Java8, HashMap has been enhanced to reduce time when we use get()

Map<Integer,String> hm=new HashMap<>();
hm.put(4,"a");
hm.put(6,"a");
hm.put(2,"a");
hm.put(7,"a");
hm.put(1,"a");
hm.put(5,"a");
hm.put(3,"c");
Consider all keys are having same values so it will same hashcode so it will have same index in bucket which degrade the performance
  From Java8, LinkedList into tree structure(self balancing/redblack tree) when no of nodes reaches certain threshold, that threshold is called Treefy threshold

Map<Integer,Integer> hm1=new HashMap<>();
hm.put(4,6);
hm.put(6,6);
hm.put(2,2);
hm.put(7,7);
hm.put(1,1);
hm.put(5,5);
hm.put(3,3);
           
          7

     6
          
          5

4
          3
          
     2

           1

In numbers we know greater or smaller, but if we store string or any other objectsm then JVM will determine the particular object is greater or smaller using compareTo()


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
       System.out.println(hm); //print in curly braces in random order
       
       System.out.println(hm.putIfAbsent(20, "melon"));  //null
       System.out.println(hm.putIfAbsent(11, "Berry")); //null
       System.out.println(hm.putIfAbsent(10, "Lime")); //mango
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


- If we want to sort the elements of List interface we have to use Collections.sort(List l)
   - If we want to sort the elements of Set interface we have to use TreeSet class
   - If it is numbers then it will be sorted in ascending order and String means it will be sorted in alphabetical order

List<Employee> l=new ArrayList<>();
empid,ename, salary, age - properties  
 
Comparable and Comparator interface
     - If ur List or Set contains collection of user defined object like Employee, Student, Person etc, now we want to sort based on their properties rather than sorting its reference 

Comparable interface                       Comparator interface
1. provides single sorting           1. provides multiple sorting sequence(ie)
sequence (ie) we can do sorting      we can do sorting based on empid and 
only based on one property either    ename and salary and age
by empid or ename or salary
or age

2. present in java.lang.*            2. present in java.util.* package
package

3. int compareTo(Object o)           3. int compare(Object o1, Object o2)

4. If we do sorting using            4. If we do sorting using Comparator
Comparable interface for List        intf for List we have to use
we have to use                       Collections.sort(List l, Comparator c)
Collections.sort(List l)             and for Set intf we have to use
and for Set intf we have to          TreeSet(Comparator c) 
use TreeSet class


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
        Collections.sort(l1,Comparator.reverseOrder());
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

Arrays class
     - used to perform operation on datatype array 
     - present in java.util.*

int a[]=new int[5];

Constructor
1. Arrays()

Methods
1. static List asList(int[] a) - convert int array to List 
2. static void fill(int[] a, int val) - fill all elts of array with val
3. static void fill(int[] a,int start, int end, int val) - fill elts with val from start to end-1
4. static void sort(int[] a) - sort all elts of array
5. static void sort(int[] a, int start, int end) sort elts of array from start to end
6. static boolean equals(int[] a1, int[] a2)
7. static int binarySearch(int[] a, int val)

These methods are applicable for all datatype arrays

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

Map interface
     - used to store collection of object but in the form of unique key value pair
     - Map is unordered

Methods
1. void put(Object k, Object v) - store single key value pair
2. void putAll(Map m) - store multiple key value pair
3. Object putIfAbsent(Object k, Object v) - if specified key is not associated with the value, then it associates the key with given value and returns null
4. boolean containsKey(Object k)
5. boolean containsValue(Object v)
6. Object get(Object k) - if we provide the key, it will return value associated with the key
7. Object getOrDefault(Object k, Object defaultvalue)-if key is not associated with any value then by default it returns null, instead we can return some default value
8. Object remove(Object k) - If we provide the key, it will remove value associated with that key and return the value
9. boolean remove(Object k, Object v)
10. Object replace(Object k, Object newvalue) - replace value for the key and returns old value
11. boolean replace(Object k, Object oldval, Object newval)
12. boolean isEmpty()
13. int size()

We cant apply Iterator interface directly on Map interface, we have convert Map to Set interface 
14. Set entrySet() - convert both key and value to Set interface
15. Set keySet() - convert only key to Set interface

Map.Entry interface
    - used to describe the key and value separately
Methods
1. Object getKey()
2. Object getValue()
3. Object setValue(Object v)

SortedMap interface
    - used to sort the etls of Map interface
Methods
1. Object firstKey()
2. Object lastKey()
3. SortedMap subMap(int start, int end)
4. SortedMap headMap(Object k)
5. SortedMap tailMap(Object k)

3 classes
1. HashMap class
       - uses Hashing technique to print the value in random order and contains key value pair
       - default capacity 16
       - allow one null key and any  number null values

Syntax: public class HashMap extends AbstractMap implements Map, Cloneable, Serializable

Constructor
1. HashMap()
2. HashMap(int capacity)
3. HashMap(int capacity, float fillratio)
4. HashMap(Map m)

Map<Employee,String> hm=new HashMap<>();

So whenever we create object of HashMap, internally it create a bucket from 0 to 15 because default capacity is 16. Each bucket internally considered as LinkedList, and each LinkedList contains one node, the internal structure of node will have key,value,hashcode and next 

Employee e1=new Employee(1,"Ram");
Employee e2=new Employee(2,"Sam");
Employee e3=new Employee(3,"Raj");
Employee e4=new Employee(4,"Tam");

hm.put(e1,"HR");

So when we call put(), first it will calculate the hashcode for the key using hashCode (ie) e1.hashCode() = 2000
Next it will calculate the index using index=hashCode(key) & (n-1)
                                            = 2000 & (16-1) = 2000 & 15 = 6

now it stores e1 into index 6

hm.put(e2,"IT");

So when we call put(), first it will calculate the hashcode for the key using hashCode (ie) e2.hashCode() = 1000
Next it will calculate the index using index=hashCode(key) & (n-1)
                                            = 1000 & (16-1) = 1000 & 15 = 9

now it stores e2 into index 9

hm.put(e3,"Sales");

So when we call put(), first it will calculate the hashcode for the key using hashCode (ie) e3.hashCode() = 2000
Next it will calculate the index using index=hashCode(key) & (n-1)
                                            = 2000 & (16-1) = 2000 & 15 = 6

now it stores e3 into index 6

If same bucket contains multiple node then that is called hashing collision, so map will not directly add the entry into the bucket since both key have same index, map will internally call equals() and check whether both content are same or different, if it is different then it will store the entry into same bucket and if it is same it will replace the entry 

hm.put(null,"Admin")
   - If we pass key as null, then entry will be directly stored in 0th index

Before we get elts from HashMap, we see how searching is done in LinkedList

Start -> item1:P -> item2:P -> item3:P -> item4:P

So in case LinkedList if we search any value it will always traverse one by one which reduces the performance
   But when we call hm.get(key), first JVM will find the hashcode of key and from hashcode it will find the bucket index, so JVM will directly goes to the index and find the value 
   In general, HashMap dosent have multiple nodes in single bucket, it should have only one node in one bucket, but there can be hashing collision where each bucket can have multiple nodes, so it reduce performance as JVM will traverse one by one
   From Java8, HashMap has been enhanced to reduce time when we use get()

Map<Integer,String> hm=new HashMap<>();
hm.put(4,"a");
hm.put(6,"a");
hm.put(2,"a");
hm.put(7,"a");
hm.put(1,"a");
hm.put(5,"a");
hm.put(3,"c");
Consider all keys are having same values so it will same hashcode so it will have same index in bucket which degrade the performance
  From Java8, LinkedList into tree structure(self balancing/redblack tree) when no of nodes reaches certain threshold, that threshold is called Treefy threshold

Map<Integer,Integer> hm1=new HashMap<>();
hm.put(4,6);
hm.put(6,6);
hm.put(2,2);
hm.put(7,7);
hm.put(1,1);
hm.put(5,5);
hm.put(3,3);
           
          7

     6
          
          5

4
          3
          
     2

           1

In numbers we know greater or smaller, but if we store string or any other objectsm then JVM will determine the particular object is greater or smaller using compareTo()


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
       System.out.println(hm); //print in curly braces in random order
       
       System.out.println(hm.putIfAbsent(20, "melon"));  //null
       System.out.println(hm.putIfAbsent(11, "Berry")); //null
       System.out.println(hm.putIfAbsent(10, "Lime")); //mango
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