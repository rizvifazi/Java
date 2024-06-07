

*Date : 04.26.2024*

# Java Collections Framework

## java.util.* 
- Utility framework or collection framework
- Used to store collection of objects - any object (i.e., String, Employee, Player, etc.)

1. **Collection Interface** - Core interface used to store a collection of objects
2. **Collections Class** - Provided with static methods or static algorithms that support the util package

### Collection Interface
- Core interface used to store a collection of objects

#### Methods
1. `boolean add(Object o)` - Store a single object
2. `boolean addAll(Collection c)` - Store multiple objects
3. `boolean remove(Object o)` - Remove a single object
4. `boolean removeAll(Collection c)` - Remove multiple objects
5. `boolean contains(Object o)` - Check if a single object is present in the collection
6. `boolean containsAll(Collection c)` - Check if multiple objects are present in the collection
7. `boolean retainAll(Collection c)` - Remove from the target collection, all the elements that are not contained in the specified collection
8. `int size()` - Return the number of elements present in the collection
9. `boolean isEmpty()` - Check whether the collection is empty
10. `Object[] toArray()` - Convert the collection to an Object array
11. `String toString()`
12. `boolean equals(Object o)`
13. `Iterator iterator()`
14. `ListIterator listIterator()`

### List Interface
- Ordered and duplicates elements allowed

#### Methods**
1. `void add(int index, Object o)` - Add a single object at a particular index position
2. `boolean addAll(int index, Collection c)` - Add multiple objects at a particular index position
3. `Object get(int index) `- Return a single object present at a particular index
4. `int indexOf(Object o) `- Return the position of the first occurrence of the object in the given collection
5. `int lastIndexOf(Object o)`- Return the position of the last occurrence of the object in the given collection
6. `Object remove(int index)` - Remove a single object present at a particular index
7. `Object set(int index, Object value)` - Replace an object at a particular index
8. `List subList(int start, int end)` - Return part of the list from start to end-1
### Set Interface
- Unordered and no duplicates allowed

### SortedSet Interface
- Used to sort the elements of the Set interface

#### Methods
1. `Object first()` - Return the first element
2. `Object last()` - Return the last element
3. `SortedSet subSet(int start, int end`) - Return part of the set from start to end-1
4. `SortedSet headSet(Object o)` - Return all elements before the specified element
	`"1 2 3 4 5".headSet(3);  // 1 2`
5. `SortedSet tailSet(Object o)` - Return all elements after the specified element.
	`"1 2 3 4 5".tailSet(3);  // 4 5`

   

### List Interface
- Ordered and duplicates elements allowed

```java
int a[] = new int[5]; // Static array
```

### 1. ArrayList Class (Best Implementation)
- It is similar to an array but is called a dynamic array (i.e., we can increase or decrease its size at runtime)
- Used for faster retrieval of data and slower in insertion and deletion
- Default capacity is 10

#### Syntax
```java
public class ArrayList extends AbstractList implements List, Cloneable, Serializable, RandomAccess
```

#### Constructors
1. **ArrayList()**
2. **ArrayList(int capacity)**
3. **ArrayList(Collection c)**

#### Example
```java
public class Main {
    public static void main(String[] args) {
        ArrayList l1 = new ArrayList();
        System.out.println(l1.size()); // 0
        l1.add("A");
        l1.add("B");
        l1.add(5);  // Autoboxing
        System.out.println(l1.size()); // 3
        System.out.println(l1); // Whenever we print an object of any collection, it will print inside []
        // [A, B, 5]

        ArrayList l2 = new ArrayList();
        System.out.println(l2.size()); // 0
        l2.addAll(l1);
        System.out.println(l2); // [A, B, 5]

        System.out.println(l1.contains(5));  // true
        System.out.println(l1.containsAll(l2)); // true
        System.out.println(l1.indexOf(5)); // 2

        List l3 = new ArrayList();  // DMD
        l3.add("A");
        l3.add("B");
        l3.add(5);
        l3.add(6);
        l3.add(7);
        System.out.println(l3); // [A, B, 5, 6, 7]

        List l4 = new ArrayList();
        l4.add("A");
        l4.add("B");
        l4.add(5);
        System.out.println(l4); // [A, B, 5]

        l3.retainAll(l4);
        System.out.println(l3); // [A, B, 5]
    }
}
```

### Generics
- Available from JDK1.5 onwards
- Used to specify what type of object is stored in the collection, avoiding type casting
- Denoted by `<>`

```java
List<String> l1 = new ArrayList<String>(); // JDK1.5
List<Integer> l2 = new ArrayList<>(); // JDK1.7

public class Main {
    public static void main(String[] args) {
        List<String> l1 = new ArrayList<>();
        System.out.println(l1.size()); // 0
        l1.add("C");
        l1.add("F");
        l1.add(1, "O");
        l1.add("T");
        l1.add("R");
        System.out.println(l1); // [C, O, F, T, R]
        System.out.println(l1.get(1)); // 0
        System.out.println(l1.contains("Z")); // false

        List<String> l2 = new ArrayList<>();
        l2.add("C");
        l2.add("F");
        System.out.println(l1.containsAll(l2)); // true
        System.out.println(l1.indexOf("U")); // -1
        l1.remove("T"); // [C, O, F, R]
        l1.remove(1);
        System.out.println(l1); // [C, F, R]
    }
}
```

### 2. LinkedList Class
- It is also called a Dynamic array
- Used for faster insertion and deletion, slower in selection

#### Syntax
```java
public class LinkedList extends AbstractSequentialList implements List, Cloneable, Serializable, Deque
```

**Deque** - Double Ended Queue - we can do insertion and deletion at both ends 

#### Constructors
1. **LinkedList()**
2. **LinkedList(Collection c)**

#### Methods
1. `void addFirst()`
2. `void addLast()`
3. `Object getFirst()`
4. `Object getLast()`
5. `Object removeFirst()`
6. `Object removeLast()`
7. `void push(Object o)`
8. `Object pop()`
9. `boolean offerFirst(Object o)` - Insert specified element at the front of the list
10. `boolean offerLast(Object o)` - Insert specified element at the end of the list
11. `Object peekFirst()`- Retrieve the first element of the list but does not remove 
12. `Object peekLast()` - Retrieve the last element of the list but does not remove 
13. `Object pollFirst()` - Retrieve the first element of the list and remove it
14. `Object pollLast()` - Retrieve the last element of the list and remove it

#### Example
```java
public class Main {
    public static void main(String[] args) {
        LinkedList<Integer> l1 = new LinkedList<>();
        l1.add(3);
        l1.add(5);
        l1.add(2);
        l1.add(1, 7);
        l1.addFirst(8);
        l1.addLast(9);
        System.out.println(l1.size()); // 6
        System.out.println(l1); // [8, 3, 7, 5, 2, 9]
        System.out.println(l1.get(5)); // 9
        System.out.println(l1.getFirst());  // 8
        System.out.println(l1.getLast()); // 9
        l1.remove(1); // [8, 7, 5, 2, 9]
        l1.removeFirst();
        l1.removeLast();
        System.out.println(l1); // [7, 5, 2]
        System.out.println(l1.peekFirst()); // 7
        System.out.println(l1.pollLast()); // 2
        System.out.println(l1); // [7, 5]
    }
}
```

### 3. Vector Class
- It is a legacy (older) class
- It is also similar to ArrayList (i.e.) dynamic array, but  it is synchronized or thread safe so gives lower performance
- Default capacity is 10

#### Syntax
```java
public class Vector extends AbstractList implements List, RandomAccess, Cloneable, Serializable
```

#### Constructors
1. **Vector()**
2. **Vector(int capacity)**
3. **Vector(int capacity, int incrementalValue)**
4. **Vector(Collection c)**

#### Example
```java
public class Main {
    public static void main(String[] args) {
        Vector<Integer> v=new Vector<>(3,2);
        System.out.println(v.size()); //0
        System.out.println(v.capacity()); //3
        v.add(1);
        v.add(2);
        v.add(3);
        v.add(4); //3+2
        System.out.println(v.size()); //4
        System.out.println(v.capacity()); //5
              v.add(5);
              v.add(6); 
              System.out.println(v.size()); //6
              System.out.println(v.capacity()); //7
              System.out.println(v); //[1,2,3,4,5,6]
    }
}
```

### Set interface
- unordered and no duplicates allowed

#### 1. HashSet class (best impl)
- does not maintain the insertion order, it will be inserted based on **hashcode** value
- default capacity is 16

**Syntax:**
```java
public class HashSet extends AbstractSet implements Set, Cloneable, Serializable
```

**Constructor**
1. **HashSet()**
2. **HashSet(int capacity)**
3. **HashSet(int capacity, float fillratio)**
    - fillratio used to increase the capacity, default value is 0.75, ranges from 0.0 to 1.0
4. **HashSet(Collection c)**

```java
Set<Integer> hs = new HashSet<>();      
Map<Integer, Object> hm = new HashMap<>();
System.out.println(hs.size()); //0
hs.add(2);                            
hm.put(2, PRESENT);
hs.add(3);                            
hm.put(3, PRESENT);
hs.add(2);                            
hm.put(2, PRESENT);
System.out.println(hs.size()); //2
```

When we create an object for **HashSet, internally it will create HashMap (unique key-value pairs)**, with the key as the element we are inserting into HashSet and the value as a dummy object called **PRESENT**.

If `hm.put(key, value)` returns null, then the statement `hm.put(2, PRESENT) == null` will return true, and the element will be added to the HashSet.

If `hm.put(key, value)` returns the old value of the key, then the statement `hm.put(2, PRESENT) == null` will return false, and the element will not be added to the HashSet.

```java
Set<Integer> hs = new HashSet<>(3);  
hs.add(1);
hs.add(2);
hs.add(3);
hs.add(4);  // 3 * 0.75 = 2.25 + 3 = 5.25
hs.add(5);
hs.add(6);  // 5.25 * 0.75 = 3.93 + 5.25 = 9
```

#### 2. LinkedHashSet class
- used to maintain the insertion order (i.e., the order in which we insert elements is the same order in which they are printed)

**Syntax:**
```java
public class LinkedHashSet extends HashSet implements Set, Cloneable, Serializable
```

**Constructor**
1. **LinkedHashSet()**
2. **LinkedHashSet(int capacity)**
3. **LinkedHashSet(int capacity, float fillratio)**
    - fillratio used to increase the capacity, default value is 0.75, ranges from 0.0 to 1.0
4. **LinkedHashSet(Collection c)**

#### 3. TreeSet class
- Prints elements of Set interface in sorted order (i.e., numbers in ascending order and strings in alphabetical order)

**Syntax:**
```java
public class TreeSet extends AbstractSet implements NavigableSet, Cloneable, Serializable
```

**Constructor**
1. **TreeSet()**
2. **TreeSet(Comparator c)**
3. **TreeSet(Collection c)**
4. **TreeSet(SortedSet s)**

```java
public class Main {
    public static void main(String[] args) {
        Set<Integer> hs = new HashSet<>();
        System.out.println(hs.size()); // 0
        hs.add(4);
        hs.add(2);
        hs.add(3);
        hs.add(1);
        System.out.println(hs); // [1, 2, 3, 4]
        
        Set<String> hs1 = new HashSet<>();
        hs1.add("Ram");
        hs1.add("Sam");
        hs1.add("Raj");
        System.out.println(hs1);
        
        LinkedHashSet<String> ls = new LinkedHashSet<>();
        ls.add("B");
        ls.add("S");
        ls.add("Q");
        ls.add("E");
        ls.add("A");
        System.out.println(ls); // [B, S, Q, E, A]
        
        TreeSet<String> ts = new TreeSet<>();
        ts.add("B");
        ts.add("S");
        ts.add("Q");
        ts.add("E");
        ts.add("A");
        System.out.println(ts); // [A, B, E, Q, S]
        
        TreeSet ts1 = (TreeSet) ts.descendingSet();
        System.out.println(ts1); // [S, Q, E, B, A]
    }
}
```

### To print individual elements of collections - 5 ways
1. **Normal for loop**
2. **For each statement**
3. **Iterator interface**
    - used to access individual elements of the collection only in the forward direction
    - Using `Iterator iterator()`, we create an object for the Iterator interface
    - **Methods**
        1. `boolean hasNext()` - checks whether it contains the next element
        2. `Object next()` - retrieves each element
        3. `void remove()` - at the time of accessing, we can remove the element
4. **ListIterator interface**
    - used to access individual elements of the collection in both forward and backward directions
    - Using `ListIterator listIterator()`, we create an object for the ListIterator interface
    - **Methods**
        1. `boolean hasNext()` - checks whether it contains the next element
        2. `Object next()` - retrieves each element
        3. `void remove()` - at the time of accessing, we can remove the element
        4. `boolean hasPrevious()`
        5. `Object previous()`
        6. `void set(Object o)` - replaces the value
        7. `void add(Object o)`
5. Enumeration interface
    - It is a legacy interface
    - used to access individual elements of the collection only in the forward direction
    - Using `Enumeration elements()`, we create an object for the Enumeration interface
    - **Methods**
        1. `boolean hasMoreElements()`
        2. `Object nextElement()`

```java
public class Main {
    public static void main(String[] args) {
        List<Integer> l1 = new ArrayList<>();
        l1.add(2);
        l1.add(1);
        l1.add(4);
        l1.add(5);
        System.out.println(l1); // [2, 1, 4, 5]
        
        System.out.println("1. Normal For loop");
        for (int i = 0; i < l1.size(); i++) {
            System.out.println(l1.get(i));
        }
        
        System.out.println("2. For each statement");
        for (Integer i1 : l1) {
            System.out.println(i1);
        }
        
        System.out.println("3. Using Iterator");
        Iterator<Integer> it = l1.iterator();
        while (it.hasNext()) {
            Integer i = it.next();
            System.out.println(i);
        }
        
        List<Student> l2 = new ArrayList<>();
        l2.add(new Student(1, "Ram", 24));
        l2.add(new Student(2, "Sam", 21));
        l2.add(new Student(3, "Raj", 22));
        l2.add(new Student(4, "Tam", 22));
        
        ListIterator<Student> li = l2.listIterator();
        while (li.hasNext()) {
            Student st = li.next();
            System.out.println(st.getName());
        }
        System.out.println();
        while (li.hasPrevious()) {
            Student st = li.previous();
            System.out.println(st.getName());
        }
        
        List<String> l3 = new ArrayList<>();
        l3.add("Ram");
        l3.add("Sam");
        l3.add("Tam");
        ListIterator<String> li1 = l3.listIterator();
        while (li1.hasNext()) {
            String str = li1.next();
            li1.set(str + "mmmm");
        }
        while (li1.hasPrevious()) {
            String st = li1.previous();
            System.out.println(st);
        }
        
        Vector<Integer> v = new Vector<>();
        v.add(1);
        v.add(2);
        v.add(3);
        v.add(4);
        System.out.println(v); // [1, 2, 3, 4]
        
        Enumeration<Integer> e = v.elements();
        while (e.hasMoreElements()) {
            System.out.println(e.nextElement());
        }
    }
}
```

### Collections class
- contains static methods/static algorithms that support util package

**Methods**
1. `static int binarySearch(List l, int val)` - search element in list 
2. `static void copy(List dest, List src)`
3. `static List nCopies(int n, Object val)` - create an immutable list with a list of values
4. `static boolean disjoint(List l1, List l2)` - return true if there is no common element
5. `static List emptyList()` - create an immutable empty list
6. `static Set emptySet()` - create an immutable empty set
7. `static Map emptyMap()` - create an immutable empty map
8. `static void fill(List l, Object o)` - fill the list with a particular value
9. `static int frequency(List l, Object o)` - return how many times an element occurs in the list
10. `static boolean replaceAll(List l, Object oldValue, Object newValue)`
11. `static Object max(List l)`
12. `static Object min(List l)`
13. `static void reverse(List l)`
14. `static void shuffle(List l)` -  randomly shuffle the elements

**Unmodifiable list** - readonly views of the original collection, we can perform modifying operation on original collection and those modification will be reflected in the collection

**Immutable list** - you cant modify once they are created 
JDK10 - List.of(T...t), Set.of(T...t)

15. `static List unmodifiableList(List l)`
16. `static Set unmodifiableSet(Set s)`
17. `static Map unmodifiableMap(Map m)`
18. `static void sort(List l)`
19. `static void sort(List l, Comparator c)`
20. `static void swap(List l, int oldindex, int newindex)`
21. `static List singletonList(Object o)` - create immutable list with single element
22. `static Set singleton(Object o)`
23. `static Map singletonMap(Object k, Object v)`
24. `static List synchronziedList(List l)`
25. `static Set synchronziedSet(Set s)`
26. `static Map synchronziedMap(Map m)`

```java
public class Main {
    public static void main(String[] args) {
        List<Integer> l1=new ArrayList<>();
        l1.add(3);
        l1.add(5);
        l1.add(2);
        l1.add(1);
        System.out.println(Collections.binarySearch(l1, 1)); //3 returns index of 1
        
        List<String> l2=new ArrayList<>();
        l2.add("one");
        l2.add("two");
        l2.add("three");
        List<String> l3=new ArrayList<>();
        l3.add("four");
        l3.add("five");
        l3.add("six");
        l3.add("seven");
              
        System.out.println(Collections.disjoint(l2, l3)); //true
        Collections.copy(l3, l2);
        System.out.println(l2); //[one,two,three]
        System.out.println(l3); //[one,two,three,seven]
        System.out.println(Collections.disjoint(l2, l3)); //false
        
        List l4=Collections.nCopies(3, "Hello"); // This creates a immutable list
        System.out.println(l4); //[Hello,Hello,Hello]
       // l4.add("Hi");
       // System.out.println(l4); //UnsupportedOperationException
        
        //Unmodifiable
        List<String> l5=new ArrayList<>();
        l5.add("a");
        System.out.println(l5); //[a]
        List l6=Collections.unmodifiableList(l5);
        System.out.println(l6); //[a]
        l5.add("b");
        System.out.println(l5); //[a,b]
        //l6.add("c"); //exception
        System.out.println(l6); //[a,b]
        
        //Immutable
        List<String> l7=Collections.unmodifiableList(new ArrayList<String>(l5));
        l5.add("c");
       // l7.add("c");  //exception
        System.out.println(l5); //[a,b,c]
        System.out.println(l6); //[a,b,c]
        System.out.println(l7); //[a,b]
        
        List l8=Collections.emptyList(); //Creates a immutable empty list
        System.out.println(l8); //[]
        //l8.add("hi");
       // System.out.println(l8);  //exception
        
        System.out.println(Collections.frequency(l4, "Hello"));  //3
        Collections.fill(l2, "Hi");
        System.out.println(l2); //[Hi,Hi,Hi]
        Collections.replaceAll(l2, "Hi", "He");
        System.out.println(l2); //[He,He,He]
        
        List<String> l9=new ArrayList<>();
        l9.add("Hii");
        l9.add("Hi");
        l9.add("Hiiiii");
        l9.add("Hi Good morning");
        Collections.replaceAll(l9, "Hi", "He");
        System.out.println(l9);  //[Hii,He,Hiiiii,Hi Good morning]
        
        List<Integer> l10=new ArrayList<>();
        l10.add(8);
        l10.add(-20);
        l10.add(20);
        l10.add(-8);
        System.out.println(l10); //[8,-20,20,-8]
        
        Collections.reverse(l10);
        System.out.println(l10); //[-8,20,-20,8]
        System.out.println(Collections.max(l10)); //20
        System.out.println(Collections.min(l10)); //-20
        
        Collections.shuffle(l10);
        System.out.println(l10); //random order
        
        Collections.sort(l10);
        System.out.println(l10); //[-20,-8,8,20]  asc order
        Collections.sort(l10,Comparator.reverseOrder());  //remember
        System.out.println(l10); //[20,8,-8,-20]  desc order
        
        Collections.swap(l10,0,3); // swap the indexed values
        System.out.println(l10); //[-20,8,-8,20]
        
        l10=Collections.singletonList(10);
        System.out.println(l10);  //[10]
        //l10.add(12);
        //System.out.println(l10);  //exception
        
        List l11=Collections.synchronizedList(l9);
        System.out.println(l11);   //threadsafe
    }
}
```


Here are two main approaches to achieve immutable collections of objects in Java:

1. **Using Unmodifiable Collections:**
    
    The `java.util.Collections` class provides methods to create unmodifiable versions of existing collections. These unmodifiable collections appear like regular collections but throw exceptions when you try to modify them (add, remove, etc.).
    
    Here's an example:
    
    Java
    
    ```
    List<String> names = new ArrayList<>();
    names.add("Alice");
    names.add("Bob");
     
    // Create an unmodifiable list
    List<String> unmodifiableNames = Collections.unmodifiableList(names);
    
    // Trying to add an element to the unmodifiable list throws an exception
    unmodifiableNames.add("Charlie"); // java.lang.UnsupportedOperationException
    ```
    
    Commonly used methods for creating unmodifiable collections include:
    
    - `Collections.unmodifiableList(List)`
    - `Collections.unmodifiableSet(Set)`
    - `Collections.unmodifiableMap(Map)`
2. **Using Immutable Collection Classes:**
    
    Java provides specific immutable collection implementations that guarantee immutability by design. These classes typically don't allow modifications after creation.
    
    Here are some examples:
    
    - **`java.util.concurrent.ImmutableList`:** An immutable list implementation.
    - **`java.util.ImmutableSet`:** An immutable set implementation.
    - **`java.util.ImmutableMap`:** An immutable map implementation.
    
    These classes offer methods to create new immutable collections with modifications (e.g., `add` in `ImmutableList`) but return a completely new collection object instead of modifying the existing one.
    
    Here's an example with `ImmutableList`:
    
    Java
    
    ```
    List<String> names = ImmutableList.of("Alice", "Bob");
    
    // Trying to add an element throws an exception (because a new list is returned)
    names.add("Charlie"); // UnsupportedOperationException (at runtime)
    
    // You can create a new immutable list with the modification
    List<String> updatedNames = ImmutableList.builder().addAll(names).add("Charlie").build();
    ```
    

**Choosing the Right Approach:**

- Use unmodifiable collections if you have an existing modifiable collection that you want to make read-only for a specific use case.
- Use immutable collection classes if you want to ensure immutability from the beginning and leverage the benefits like thread-safety (some implementations) and better reasoning about your code.