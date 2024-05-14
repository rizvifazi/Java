
*Date : 05.03.2024*

Map interface

1. HashMap class

2. LinkedHashMap class
       - used to maintain insertion order

Syntax: public class LinkedHashMap extends HashMap

Constructor
1. LinkedHashMap()
2. LinkedHashMap(int capacity)
3. LinkedHashMap(int capacity,float fillratio)
4. LinkedHashMap(Map m)

3. TreeMap class
       - used to sort the elements only based on key

Syntax: public class TreeMap extends AbstractMap implements NavigableMap, Cloneable, Serializable

4. Hashtable class
       - It is a legacy class
       - similar to HashMap but it is synchronized or thread safe

Syntax: public class Hashtable extends Dicitionary implements Map, Cloneable, Serializable

Constructor
1. Hashtable()
2. Hashtable(int capacity)
3. Hashtable(int capacity,float fillratio)
4. Hashtable(Map m)

5. Properties class
       - contains key value pair but both key and value should be in the form of String, print in random order
    
Syntax: public class Properties extends Hashtable

Constructor
1. Properties()
2. Properties(String default)

public class Main {
    public static void main(String[] args) {
       LinkedHashMap<Integer,String> lm=new LinkedHashMap<>();
       System.out.println(lm.size()); //0
       lm.put(10, "mango");
       lm.put(3, "apple");
       lm.put(20, "grapes");
       lm.put(11, "banana");
       System.out.println(lm);//{10=mango, 3=apple, 20=grapes, 11=banana}
       
       TreeMap<Integer,String> tm=new TreeMap<>();
       tm.put(10, "mango");
       tm.put(3, "apple");
       tm.put(20, "grapes");
       tm.put(11, "banana");
       System.out.println(tm);//{3=apple, 10=mango, 11=banana, 20=grapes}
       
       Hashtable<Integer,Double> ht=new Hashtable<>();
       System.out.println(ht.size()); //0
       ht.put(3, 4.56);
       ht.put(1, 1.23);
       ht.put(4, 2.33);
       ht.put(2, 7.88);
       System.out.println(ht); //{4=2.33, 3=4.56, 2=7.88, 1=1.23}
       Enumeration<Integer> e=ht.keys();
       while(e.hasMoreElements()) {
                 Integer key=e.nextElement();
                 System.out.println(key+" "+ht.get(key));
       }
      
       Properties p=new Properties();
       p.put("cow", "milk");
       p.put("dog", "bark");
       p.put("goat", "meat");
       p.put("bird", "fly");
       System.out.println(p);
       
       Set set=p.keySet();
       Iterator<String> it=set.iterator();
       while(it.hasNext()) {
                 String key=it.next();
                 System.out.println(key+" "+p.getProperty(key));
       }
       
    }
}

JDK1.5
1. Generics
2. for each stmt
3. var args
4. static import
5. Assertions
6. Covariant return type
7. Autoboxing and Unboxing
8. Annotation

JDK1.7
1. In switch stmt, we can pass String as expr
2. try with resources
3. Multi catch statement
4. Generics
5. Underscore literal - meant for representation
      int a=100000;
      int a=1_00_000; //correct
      int a=10_000; //correct
      int a=10_;  //error
      int a=_10; //error
      float f1=3.1_4f; //correct
      float f1=3_.14f; //error
      float f1=3._14f; //error
      float f1=3.14_f; //error
6. Binary literal
       int a=0b10;  //2
       int a=0B100; //4


JAVA 8
1. Lambda expression 
       - used to enable functional programming in Java, until JDK1.7 we cant write anything that exists on its own, first we have to create a class and access the class with the help of object 

public class Main {
              public void greet() {
                             System.out.println("Hello");
              }
    public static void main(String[] args) {
       Main m=new Main();
       m.greet();      
    }
}

Now greet() always print only "Hello", but we need greet() to print different information, until JDK1.7 if we need different implementation then we have to go for interface 

interface Greeting {
              void perform();
}
class HelloWorld implements Greeting {
              @Override
              public void perform() {
                             System.out.println("HelloWorld");
              }             
}
class Welcome implements Greeting {
              @Override
              public void perform() {
                             System.out.println("Welcome");
              }             
}
public class Main {
              /*public void greet() {
                             System.out.println("Hello");
              }*/
              public void greet(Greeting g) {
                             g.perform();
              }
    public static void main(String[] args) {
       Main m=new Main();
       //m.greet();  
       Greeting gr=new HelloWorld(); //DMD
       m.greet(gr); //HelloWorld
       gr=new Welcome();
       m.greet(gr); //Welcome
    }
}

We want to pass the behaviour (ie) perform() as an argument to greet() and execute the behaviour directly, rather than passing the thing that contains the behaviour (ie) Greeting interface

Lambda expression are just function that exists on its own and execute it independently, so that we enable functional programming in Java 

How to write Lambda expr?
1. We take a function and assign to a variable
   a=public void perform() {
          System.out.println("Hello");
     }
-public, private, protected make sense if we write any method inside class, but in lambda expr, functions are exists on its own, so when we write lambda expr there is no need to define access specifiers

2. a=void perform() {
          System.out.println("Hello");
     }
- whenever we assign a function to a variable, we can access the function using ur variable name, so when we write lambda expr there is no need to define method name

3. a=void () {
          //System.out.println("Hello");
          return 10;
     }
- By seeing the function itself we can identify the return type of the function, so when we write lambda expr there is no need to define return type

4. a=() {
          System.out.println("Hello");
     }

Lambda expr contains parenthesis for input arg, logic and we need to put -> symbol

a=() -> {
          System.out.println("Hello");
     }
b=(int a,int b) -> {
        System.out.println(a+b);
     }

5. FunctionType<Void,Void> a=() -> {
                                    System.out.println("Hello");
                                 }

FunctionalInterface a=() -> {
                              System.out.println("Hello");
                            }

Using functional interface as a return type of lambda expr is called as type inference
  - Lambda expr is always used to write logic only for the methods in functional interface

Rules
1. If ur body of lambda expr is just single line then we can ignore curly braces

FunctionalInterface a=() -> System.out.println("Hello");
                            
2. If ur body of lambda expr is just single line then we can ignore return stmt
FunctionalInterface a=(int a) -> {
                                       return a*2;
                                  }

FunctionalInterface a=(int a) -> a*2;

Before JDK1.8, how we can access methods of an interface ? 2 ways
1. By implementing interface in a class 

interface Greeting {
              void perform();
}
class HelloWorld implements Greeting {
              @Override
              public void perform() {
                             System.out.println("HelloWorld");
              }             
}
public class Main {
    public static void main(String[] args) {
       Greeting gr=new HelloWorld(); //DMD
       gr.perform(); //HelloWorld
       
    }
}

2. Using Anonmyous inner class

interface Greeting {
              void perform();
}
public class Main {
    public static void main(String[] args) {
      Greeting gr=new Greeting() {
                public void perform() {
                               System.out.println("hello");
                }
      };
       gr.perform();
    }
}

Functional interface
    - contains only one abstract method and any number of default and static method
    - We will write logic for functional interface method using lambda expr
    - Using @FunctionalInterface annotation - optional - present in java.lang.*
    - It is also called as SAM(Single Abstract Method)
    - If an interface contains any method of only Object class as abstract, then it is also considered as Functional interface

//Functional interface
interface A {
    void add();
}

//Functional interface
interface A {
    void add();
    default void show() { }
    static void show1() { }
}

//Not Functional interface
interface A {
    void add();
    int add1();
}

//Functional interface
interface A {
    void add();
    String toString(); //Object class
}


//Not Functional interface
interface A {
    void add();
    boolean equals();
}


//Functional interface
interface A {
    void add();
    boolean equals(Object o);  //Object class
}

//Functional interface
@FunctionalInterface
interface A {
    void add();
}

//Functional interface
interface A {
    void add();
}
interface B extends A {  //Not functional interface
    void add1();
}


interface Greeting {
              void perform();
}
public class Main {
    public static void main(String[] args) {
      Greeting g=()->System.out.println("Using lambda");
      g.perform();  //Using Lambda
    }
}


interface MyInterface {
              int calculateLength(String s);
}
public class Main {
    public static void main(String[] args) {
       MyInterface m1=(e)->e.length();
       System.out.println(m1.calculateLength("hello")); //5
    }
}

interface MyInterface {
              void add(int a,int b);
}
public class Main {
    public static void main(String[] args) {
      MyInterface m1=(x,y)->System.out.println(x+y);
      m1.add(2,3); //5
    }
}

2. Method reference
      - also used to access the method of functional interface, instead of writing logic separately using lambda expr we can refer already existing methods, when the signature of the interface method is same as the static method or instance method or constructor 
      - It is an alternative to lambda expr
      - denoted using ::

3 types
1. Reference to static method
2. Reference to instance method

interface MyInterface {
              void show();
}
public class Main {
              /*public static void add() {
                             System.out.println("Reference to static method");
              }*/
              public void demo() {
                             System.out.println("Reference to instance method");
              }
    public static void main(String[] args) {
     //  MyInterface m1=()->System.out.println("using lambda");
      // m1.show(); //using lamdba
              
              //MyInterface m2=Main::add;
              //m2.show(); //Reference to static method
              
              Main m=new Main();
              MyInterface m3=m::demo;
              m3.show(); //Reference to instance method
    }
}

3. Reference to Constructor

interface MyInterface {
              //Main show();
              Main show(String s);
}
public class Main {
              Main() {
                             System.out.println("Using default constructor");
              }
              Main(String s) {
                             System.out.println("Using constructor "+s);
              }
    public static void main(String[] args) {
      // MyInterface m1=Main::new;
      // m1.show(); //Using default constructor
              
              MyInterface m2=Main::new;
              m2.show("hello");  //Using constructor hello
    }
}

Predefined Functional interface - present in java.util.function.* pkg
1. Consumer interface 
       - void accept(T t)

JDK1.8 - void forEach(Consumer c) -  used to iterate the elts of List and Set interface individually 

2. Biconsumer interface
       - void accept(T t,U u)

JDK1.8 - void forEach(Biconsumer c) -  used to iterate the elts of Map interface individually 

3. Function interface
      - R apply(T t)

4. BiFunction interface
      - R apply(T t,U u)

5. Predicate interface
      - boolean test(T t)

6. BiPredicate interface
      - boolean test(T t,U u)

7. Supplier interface
      - T get()

8. BooleanSupplier interface
      - boolean getAsBoolean()

9. BinaryOperator interface extends BiFunction interface
       - R apply(T t, U u)

10. UnaryOperator interface extends Function interface
       - R apply(T t)


public class Main {
    public static void main(String[] args) {
      List<String> l=new ArrayList<>();
      l.add("Ram");
      l.add("Sam");
      l.add("Bam");
      l.add("Tam");
      System.out.println(l); //[Ram,Sam,Bam,Tam]
     // l.forEach((e)->System.out.println(e));
      l.forEach(System.out::println); //Reference to instance method
      
      Map<Integer,String> hm=new HashMap<>();
      hm.put(10, "B");
      hm.put(5, "C");
      hm.put(1, "L");
      hm.put(3, "T");
      System.out.println(hm); //curly brace in random order
      hm.forEach((k,v)->System.out.println("key = "+k+" value = "+v));
      
      Function<String,Integer> f=(s)->s.length();
      System.out.println(f.apply("hello")); //5
      
      BiFunction<Integer,Integer,Integer> bf=(x1,x2)->x1+x2;
      System.out.println(bf.apply(10, 20)); //30
      
      Predicate<String> p=(x)->x.startsWith("Foo");
      System.out.println(p.test("Foobar")); //true
      
      BiPredicate<Integer,String> bp=(s1,s2)->s1>20 && s2.startsWith("Foo");
      System.out.println(bp.test(25, "Foobar")); //true
      
      Supplier<String> su=()->"hello";
      System.out.println(su.get()); //hello
      
      BooleanSupplier bs=()->10>20;
      System.out.println(bs.getAsBoolean()); //false
      
      BinaryOperator<String> bo=(y1,y2)->y1.concat(y2);
      System.out.println(bo.apply("hello","world")); //helloworld
    }
}
