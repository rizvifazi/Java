

*Date : 04.26.2024*



java.util.* 
    - Utility framework or collection framework
    - used to store collection of objects - any object (ie) String, Employee, Player etc

1. Collection interface - core interface used to store collection of objects
2. Collections class - provided with static methods or static algorithms that support util package

Collection interface
      - core interface used to store collection of objects

Methods
1. boolean add(Object o) - store single object
2. boolean addAll(Collection c) - store multiple object
3. boolean remove(Object o) - remove single object
4. boolean removeAll(Collection c) - remove multiple object
5. boolean contains(Object o) - check single object present in collection or not
6. boolean containsAll(Collection c) - check multiple object present in collection or not
7. boolean retainAll(Collection c) - remove from the target collection, all the elemt that are not contained in the specified collection
8. int size() - return number of elts present in the collection
9. boolean isEmpty() - check whether collection is empty or not
10. Object[] toArray() - convert collection to an Object[]
11. String toString()
12. boolean equals(Object o)
13. Iterator iterator()
14. ListIterator listIterator()

List interface
     - ordered and duplicates elements allowed

Methods
1. void add(int index,Object o) - add single object at particular index position
2. boolean addAll(int index, Collection c) -  add multiple object at particular index position
3. Object get(int index) - return single object present in particular index
4. int indexOf(Object o) - return position of first occurence of object in given collection
5. int lastIndexOf(Object o) - return position of last occurence of object in given collection
6. Object remove(int index) - remove single object present in particular index
7. Object set(int index, Object value) - replace an object at particular index 
8. List subList(int start,int end) - return part of List from start to end-1

Set interface
     - unordered and no duplicated allowed

SortedSet interface
     - used to sort the elements of Set interface

Methods
1. Object first() - return first elemt
2. Object last - return last elt
3. SortedSet subSet(int start,int end) - return part of set from start to end-1
4. SortedSet headSet(Object o) - return all elt before the specified elt
    "1 2 3 4 5".headSet(3);  //1 2
5. SortedSet tailSet(Object o) - return all elt after the specified elt
    "1 2 3 4 5".tailSet(3);  //4 5

List interface
     - ordered and duplicates elements allowed

int a[]=new int[5]; //static array

1. ArrayList class (best impl)
      - It is similar to array but it is called as dynamic array (ie) we can increase or decrease its size at runtime
      - used for faster retrieval of data and slower in insertion and deletion
      - default capacity is 10

Syntax: public class ArrayList extends AbstractList implements List, Cloneable, Serializable, RandomAccess

Constructors
1. ArrayList()
2. ArrayList(int capacity)
3. ArrayList(Collection c)

public class Main {
    public static void main(String[] args) {
              ArrayList l1=new ArrayList();
              System.out.println(l1.size()); //0
              l1.add("A");
              l1.add("B");
              l1.add(5);  //Autoboxing
              System.out.println(l1.size()); //3
              System.out.println(l1); //Whenever we print object of any collection it will print inside []
              //[A,B,5]
              
              ArrayList l2=new ArrayList();
              System.out.println(l2.size()); //0
              l2.addAll(l1);
              System.out.println(l2); //[A,B,5]
              
              System.out.println(l1.contains(5));  //true
              System.out.println(l1.containsAll(l2)); //true
              System.out.println(l1.indexOf(5)); //2
              
              List l3=new ArrayList();  //DMD
              l3.add("A");
              l3.add("B");
              l3.add(5);
              l3.add(6);
              l3.add(7);
              System.out.println(l3); //[A,B,5,6,7]
              
              List l4=new ArrayList();
              l4.add("A");
              l4.add("B");
              l4.add(5); 
              System.out.println(l4); //[A,B,5]
              
              l3.retainAll(l4);
              System.out.println(l3); //[A,B,5]
    }
}

Generics
    - Available from JDK1.5 onwards
    - used to specify what type of object stored in the collection, avoid type casting
    - denoted by <>

List<String> l1=new ArrayList<String>(); //JDK1.5
List<Integer> l2=new ArrayList<>(); //JDK1.7

public class Main {
    public static void main(String[] args) {
              List<String> l1=new ArrayList<>();
              System.out.println(l1.size()); //0
              l1.add("C");
              l1.add("F");
              l1.add(1,"O");
              l1.add("T");
              l1.add("R");
              System.out.println(l1); //[C,O,F,T,R]
              System.out.println(l1.get(1)); //0
              System.out.println(l1.contains("Z")); //false
              
              List<String> l2=new ArrayList<>();
              l2.add("C");
              l2.add("F");
              System.out.println(l1.containsAll(l2)); //true
              System.out.println(l1.indexOf("U")); //-1
              l1.remove("T"); //C,O,F,R
              l1.remove(1);
              System.out.println(l1); //[C,F,R]
    }
}

2. LinkedList class
       - It is also called as Dynamic array 
       - used for faster insertion and deletion, slower in selection

Syntax: public class LinkedList extends AbstractSequentialList implements List,Cloneable, Serializable, Deque

Deque - Double Ended Queue - we can do insertion and deletion at both ends 

Constructor
1. LinkedList()
2. LinkedList(Collection c)

Methods
1. void addFirst()
2. void addLast()
3. Object getFirst()
4. Object getLast()
5. Object removeFirst()
6. Object removeLast()
7. void push(Object o)
8. Object pop()
9. boolean offerFirst(Object o) - insert specified elt front of the list
10. boolean offerLast(Object o) - insert specified elt last of the list
11. Object peekFirst() - retrieve first elet of the list but does not remove 
12. Object peekLast() - retrieve last elet of the list but does not remove 
13. Object pollFirst() - retrieve first elet of the list and remove it
14. Object pollLast() - retrieve last elet of the list and remove it

public class Main {
    public static void main(String[] args) {
              LinkedList<Integer> l1=new LinkedList<>();
              l1.add(3);
              l1.add(5);
              l1.add(2);
              l1.add(1,7);
              l1.addFirst(8);
              l1.addLast(9);
              System.out.println(l1.size()); //6
              System.out.println(l1); //[8,3,7,5,2,9]
              System.out.println(l1.get(5)); //9
              System.out.println(l1.getFirst());  //8
              System.out.println(l1.getLast()); //9
              l1.remove(1); //8,7,5,2,9
              l1.removeFirst();
              l1.removeLast();
              System.out.println(l1); //[7,5,2]
              System.out.println(l1.peekFirst()); //7
              System.out.println(l1.pollLast()); //2
              System.out.println(l1); //[7,5]
              
    }
}

3. Vector class
       - It is a legacy(older) class
       - It is also similar to ArrayList (ie) dynamic array, but  it is synchronized or thread safe so gives lower performance
       - Default capacity is 10

Syntax: public class Vector extends AbstractList implements List, Cloneable, Serializable

Constructor
1. Vector()
2. Vector(int capacity)
3. Vector(int capacity, int increment)
4. Vector(Collection c)

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

Set interface
    - unordered and no duplicates allowed

1. HashSet class (best impl)
       - does not maintain the insertion order, it will be inserted based on hashcode value
       - default capacity is 16

Syntax: public class HashSet extends AbstractSet implements Set, Cloneable, Serializable

Constructor
1. HashSet()
2. HashSet(int capacity)
3. HashSet(int capacity, float fillratio)
       fillratio used to increase the capacity, default value is 0.75, ranges from 0.0 to 1.0
4. HashSet(Collection c)

Set<Integer> hs=new HashSet<>();      Map<Integer,Object> hm=new HashMap<>();
sop(hs.size()); //0
hs.add(2);                            hm.put(2,PRESENT);
hs.add(3);                            hm.put(3,PRESENT);
hs.add(2);                            hm.put(2,PRESENT);
sop(hs.size()); //2

When we create object for HashSet, internally it will create HashMap(unique key value pairs), with key as what element we are inserting into hashset and value as dummy object called PRESENT

If hm.put(key,value) returns null then the statement hm.put(2,PRESENT)==null will return true, then the elt will be added into hashset 

If hm.put(key,value) returns old value of the key then the statement hm.put(2,PRESENT)==null will return false, then the elt will not be added into hashset 

Set<Integer> hs=new HashSet<>(3);  
hs.add(1);
hs.add(2);
hs.add(3);
hs.add(4);  //3*0.75=2.25+3=5.25
hs.add(5);
hs.add(6);  //5.25*0.75= 3.93+5.25=9

2. LinkedHashSet class
        - used to maintain the insertion order (ie) wht order we are inserted same order it will printed

Syntax: public class LinkedHashSet extends HashSet implements Set, Cloneable, Serializable

Constructor
1. LinkedHashSet()
2. LinkedHashSet(int capacity)
3. LinkedHashSet(int capacity, float fillratio)
       fillratio used to increase the capacity, default value is 0.75, ranges from 0.0 to 1.0
4. LinkedHashSet(Collection c)

3. TreeSet class
      - Print elements of Set intf in Sorted order (ie) number in asc order and String in alphabetical order

Syntax: public class TreeSet extends AbstractSet implements NavigableSet, Cloneable, Serializable

Constructor
1. TreeSet()
2. TreeSet(Comparator c)
3. TreeSet(Collection c)
4. TreeSet(SortedSet s)


public class Main {
    public static void main(String[] args) {
        Set<Integer> hs=new HashSet<>();
        System.out.println(hs.size()); //0
        hs.add(4);
        hs.add(2);
        hs.add(3);
        hs.add(1);
        System.out.println(hs); //[1,2,3,4]
        Set<String> hs1=new HashSet<>();
        hs1.add("Ram");
        hs1.add("Sam");
        hs1.add("Raj");
        System.out.println(hs1);
        
        LinkedHashSet<String> ls=new LinkedHashSet<>();
        ls.add("B");
        ls.add("S");
        ls.add("Q");
        ls.add("E");
        ls.add("A");
        System.out.println(ls); //[B,S,Q,E,A]
              
        TreeSet<String> ts=new TreeSet<>();
        ts.add("B");
        ts.add("S");
        ts.add("Q");
        ts.add("E");
        ts.add("A");
        System.out.println(ts);  //[A,B,E,Q,S]
        TreeSet ts1=(TreeSet) ts.descendingSet();
        System.out.println(ts1); //[S,Q,E,B,A]
    }
}

To print individual elements of collections - 5 ways
1. Normal for loop
2. for each stmt
3. Iterator interface
        - used to access individual elements of collection only in forward direction
        - Using Iterator iterator(), we create object for Iterator interface
        - Methods
           1. boolean hasNext() - check whether it contains next next elt
           2. Object next() - retrieve each elt
           3. void remove() - at time of accessing we can remove the elt

4. ListIterator interface
        - used to access individual elements of collection both in forward and backward direction
        - Using ListIterator listIterator(), we create object for ListIterator interface
        - Methods
           1. boolean hasNext() - check whether it contains next next elt
           2. Object next() - retrieve each elt
           3. void remove() - at time of accessing we can remove the elt
           4. boolean hasPrevious()
           5. Object previous()
           6. void set(Object o) - replace the value
           7. void add(Object o)

5. Enumeration interface
          - It is legacy interface
          - used to access individual elements of collection only in forward direction
          - Using Enumeration elements(), we create object for Enumeration interface
          - Methods
             1. boolean hasMoreElements()
             2. Object nextElement()

public class Main {
    public static void main(String[] args) {
        List<Integer> l1=new ArrayList<>();
        l1.add(2);
        l1.add(1);
        l1.add(4);
        l1.add(5);
        System.out.println(l1); //[2,1,4,5]
        
        System.out.println("1. Normal For loop");
        for(int i=0;i<l1.size();i++) {
              System.out.println(l1.get(i));
        }
        System.out.println("2. For each stmt");
        for(Integer i1:l1)
              System.out.println(i1);
        
        System.out.println("3. Using Iterator");
        Iterator<Integer> it=l1.iterator();
        while(it.hasNext()) {
                     //Integer i=(Integer)it.next();
                     Integer i=it.next();
                     System.out.println(i);
        }
        
        List<Student> l2=new ArrayList<>();
        l2.add(new Student(1,"Ram",24));
        l2.add(new Student(2,"Sam",21));
        l2.add(new Student(3,"Raj",22));
        l2.add(new Student(4,"Tam",22));
        
        ListIterator<Student> li=l2.listIterator();
        while(li.hasNext()) {
              Student st=li.next();
              System.out.println(st.getName());
        }
        System.out.println();
        while(li.hasPrevious()) {
              Student st=li.previous();
              System.out.println(st.getName());
        }
        
        List<String> l3=new ArrayList<>();
        l3.add("Ram");
        l3.add("Sam");
        l3.add("Tam");
        ListIterator<String> li1=l3.listIterator();
        while(li1.hasNext()) {
              String str=li1.next();
              li1.set(str+"mmmm");
        }
        while(li1.hasPrevious()) {
              String st=li1.previous();
              System.out.println(st);
        }
        
        Vector<Integer> v=new Vector<>();
        v.add(1);
        v.add(2);
        v.add(3);
        v.add(4);
        System.out.println(v); //[1,2,3,4]
        
        Enumeration<Integer> e=v.elements();
        while(e.hasMoreElements()) {
              System.out.println(e.nextElement());
        }
    }
}


Collections class
     - contains static methods/static algorithms that support util package 

Methods
1. static int binarySearch(List l, int val) - search elt in list 
2. static void copy(List dest,List src)
3. static List nCopies(int n,Object val) - create immutable list with list of values
4. static boolean disjoint(List l1, List l2) - return true if there is no common elt
5. static List emptyList() - create immutable empty list
6. static Set emptySet() - create immutable empty set
7. static Map emptyMap() - create immutable empty map
8. static void fill(List l, Object o) - fill the list with particular value
9. static int frequency(List l, Object o) - return how many times an elt occur in list
10. static boolean replaceAll(List l, Object oldvalue, Object newValue)
11. static Object max(List l)
12. static Object min(List l)
13. static void reverse(List l)
14. static void shuffle(List l) - randomly shuffle the elt

Unmodifiable list - readonly views of the original collection, we can perform modifying operation on original collection and those modification will be reflected in the collection

Immutable list - you cant modify once they are created 
JDK10 - List.of(T...t), Set.of(T...t)

15. static List unmodifiableList(List l)
16. static Set unmodifiableSet(Set s)
17. static Map unmodifiableMap(Map m)
18. static void sort(List l)
19. static void sort(List l, Comparator c)
20. static void swap(List l, int oldindex, int newindex)
21. static List singletonList(Object o) - create list with single elt
22. static Set singleton(Object o)
23. static Map singletonMap(Object k, Object v)
24. static List synchronziedList(List l)
25. static Set synchronziedSet(Set s)
26. static Map synchronziedMap(Map m)


public class Main {
    public static void main(String[] args) {
        List<Integer> l1=new ArrayList<>();
        l1.add(3);
        l1.add(5);
        l1.add(2);
        l1.add(1);
        System.out.println(Collections.binarySearch(l1, 1)); //3
        
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
        
        List l4=Collections.nCopies(3, "Hello");
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
        
        List l8=Collections.emptyList();
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
        Collections.sort(l10,Comparator.reverseOrder());
        System.out.println(l10); //[20,8,-8,-20]  desc order
        
        Collections.swap(l10,0,3);
        System.out.println(l10); //[-20,8,-8,20]
        
        l10=Collections.singletonList(10);
        System.out.println(l10);  //[10]
        //l10.add(12);
        //System.out.println(l10);  //exception
        
        List l11=Collections.synchronizedList(l9);
        System.out.println(l11);   //threadsafe
    }
}
