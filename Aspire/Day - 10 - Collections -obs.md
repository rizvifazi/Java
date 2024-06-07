
*Date : 05.03.2024*

## Map interface

1. HashMap class

2. LinkedHashMap class
   - used to maintain insertion order, similar to linked has set.

    ```java
    Syntax: public class LinkedHashMap extends HashMap
    ```

    **Constructor**

    1. LinkedHashMap()
    2. LinkedHashMap(int capacity)
    3. LinkedHashMap(int capacity, float fillratio)
    4. LinkedHashMap(Map m)

3. TreeMap class
   - used to sort the elements only **based on key**

    ```java
    Syntax: public class TreeMap extends AbstractMap implements NavigableMap, Cloneable, Serializable
    ```

4. Hashtable class
   - It is a legacy class
   - similar to HashMap but it is synchronized or thread safe

    ```java
    Syntax: public class Hashtable extends Dictionary implements Map, Cloneable, Serializable
    ```

    **Constructor**

    1. Hashtable()
    2. Hashtable(int capacity)
    3. Hashtable(int capacity, float fillratio)
    4. Hashtable(Map m)

5. Properties class
   - contains key value pair but both key and value should be in the form of String, print in random order

    ```java
    Syntax: public class Properties extends Hashtable
    ```

    **Constructor**

    1. Properties()
    2. Properties(String default)

    ```java
    public class Main {
        public static void main(String[] args) {
            LinkedHashMap<Integer, String> lm = new LinkedHashMap<>();
            System.out.println(lm.size()); // 0
            lm.put(10, "mango");
            lm.put(3, "apple");
            lm.put(20, "grapes");
            lm.put(11, "banana");
            System.out.println(lm); // {10=mango, 3=apple, 20=grapes, 11=banana} // Insertion order

            TreeMap<Integer, String> tm = new TreeMap<>();
            tm.put(10, "mango");
            tm.put(3, "apple");
            tm.put(20, "grapes");
            tm.put(11, "banana");
            System.out.println(tm); // {3=apple, 10=mango, 11=banana, 20=grapes} //Sorted keys

            Hashtable<Integer, Double> ht = new Hashtable<>();
            System.out.println(ht.size()); // 0
            ht.put(3, 4.56);
            ht.put(1, 1.23);
            ht.put(4, 2.33);
            ht.put(2, 7.88);
            System.out.println(ht); // {4=2.33, 3=4.56, 2=7.88, 1=1.23}
            Enumeration<Integer> e = ht.keys();  // HT is Legacy so Enumeration is also Legacy, can use iterator also
            while (e.hasMoreElements()) {
                Integer key = e.nextElement();
                System.out.println(key + " " + ht.get(key));
            }

            Properties p = new Properties(); // k-v both should be string
            p.put("cow", "milk");
            p.put("dog", "bark");
            p.put("goat", "meat");
            p.put("bird", "fly");
            System.out.println(p);

            Set set = p.keySet();
            Iterator<String> it = set.iterator();  // Prop also Legacy , but we can use Iterator
            while (it.hasNext()) {
                String key = it.next();
                System.out.println(key + " " + p.getProperty(key));
            }
        }
    }
    ```

> We can't apply Iterator directly on the Map interface, so we should convert to Set interface.
## JDK 1.5
1. Generics
2. for each stmt
3. var args
4. static import
5. Assertions
6. Covariant return type
7. Autoboxing and Unboxing
8. Annotation

## JDK 1.7
1. In switch stmt, we can pass String as expr
2. try with resources
3. Multi catch statement
4. Generics
5. Underscore literal - meant for representation

    ```java
    int a = 100000;
    int a = 1_00_000; // correct
    int a = 10_000; // correct
    int a = 10_;  // error
    int a = _10; // error
    float f1 = 3.1_4f; // correct
    float f1 = 3_.14f; // error
    float f1 = 3._14f; // error
    float f1 = 3.14_f; // error
    ```

6. Binary literal

    ```java
    int a = 0b10;  // 2
    int a = 0B100; // 4
    ```

## JAVA 8
1. Lambda expression 
   - used to enable functional programming in Java, until JDK1.7 we can't write anything that exists on its own, first we have to create a class and access the class with the help of object 

    ```java
    public class Main {
        public void greet() {
            System.out.println("Hello");
        }
        public static void main(String[] args) {
            Main m = new Main();
            m.greet();      
        }
    }
    ```

    Now greet() always print only "Hello", but we need greet() to print different information, until JDK1.7 if we need different implementation then we have to go for interface 

    ```java
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
            Main m = new Main();
            //m.greet();  
            Greeting gr = new HelloWorld(); // DMD
            m.greet(gr); // HelloWorld
            gr = new Welcome();
            m.greet(gr); // Welcome
        }
    }
    ```

    We want to pass the behaviour (ie) perform() as an argument to greet() and execute the behaviour directly, rather than passing the thing that contains the behaviour (ie) Greeting interface

    Lambda expressions are just functions that exist on their own and execute independently, so that we enable functional programming in Java 

    **How to write Lambda expressions?**
    1. We take a function and assign to a variable

    ```java
    a = public void perform() {
        System.out.println("Hello");
    }
    ```

    - public, private, protected make sense if we write any method inside class, but in lambda expressions, functions exist on their own, so when we write lambda expressions there is no need to define access specifiers

    2. 

    ```java
    a = void perform() {
        System.out.println("Hello");
    }
    ```

    - whenever we assign a function to a variable, we can access the function using the variable name, so when we write lambda expressions there is no need to define method name

    3. 

    ```java
    a = void () {
        // System.out.println("Hello");
        return 10;
    }
    ```

    - By seeing the function itself we can identify the return type of the function, so when we write lambda expressions there is no need to define return type

    4. 

    ```java
    a = () {
        System.out.println("Hello");
    }
    ```

    Lambda expressions contain parenthesis for input arg, logic, and we need to put -> symbol

    ```java
    a = () -> {
        System.out.println("Hello");
    }
    b = (int a, int b) -> {
        System.out.println(a + b);
    }
    ```

    5. 

    ```java
    FunctionalInterface<Void, Void> a = () -> {
        System.out.println("Hello");
    }
    ```

    ```java
    FunctionalInterface a = () -> {
        System.out.println("Hello");
    }
    ```

    Using functional interface as a return type of lambda expressions is called type inference
    - Lambda expressions are always used to write logic only for the methods in functional interface

    **Rules**
    1. If the body of lambda expression is just a single line then we can ignore curly braces

    ```java
    FunctionalInterface a = () -> System.out.println("Hello");
    ```

    2. If the body of lambda expression is just a single line then we can ignore return statement

    ```java
    FunctionalInterface a = (int a) -> {
        return a * 2;
    }

    FunctionalInterface a = (int a) -> a * 2;
    ```

    **Before JDK 1.8, how can we access methods of an interface?** 

    **2 ways**

    1. By implementing interface in a class 

    ```java
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
            Greeting gr = new HelloWorld(); // DMD - Dynamic Method Dispatch
            gr.perform(); // HelloWorld
        }
    }
    ```

    2. Using Anonymous inner class

    ```java
    interface Greeting {
        void perform();
    }
    public class Main {
        public static void main(String[] args)

 {
            Greeting gr = new Greeting() {
                public void perform() {
                    System.out.println("hello");
                }
            };
            gr.perform();
        }
    }
    ```

**Functional interface**
- contains only one abstract method and any number of default and static methods
- We will write logic for functional interface method using lambda expression
- Using @FunctionalInterface annotation - optional - present in java.lang.*
- It is also called SAM (Single Abstract Method)
- If an interface contains any method of only Object class as abstract, then it is also considered as Functional interface

```java
// Functional interface
interface A {
    void add();
}
```

```java
// Functional interface
interface A {
    void add();
    default void show() { }
    static void show1() { }
}
```

```java
// Not Functional interface
interface A {
    void add();
    int add1();
}
```

```java
// Functional interface
interface A {
    void add();
    String toString(); // Object class
}
```

```java
// Not Functional interface
interface A {
    void add();
    boolean equals();
}
```

```java
// Functional interface
interface A {
    void add();
    boolean equals(Object o);  // Object class
}
```

```java
// Functional interface
@FunctionalInterface
interface A {
    void add();
}
```

```java
// Functional interface
interface A {
    void add();
}
interface B extends A {  // Not functional interface
    void add1();
}
```

```java
interface Greeting {
    void perform();
}
public class Main {
    public static void main(String[] args) {
        Greeting g = () -> System.out.println("Using lambda");
        g.perform();  // Using Lambda
    }
}
```

```java
interface MyInterface {
    int calculateLength(String s);
}
public class Main {
    public static void main(String[] args) {
        MyInterface m1 = (e) -> e.length();
        System.out.println(m1.calculateLength("hello")); // 5
    }
}
```

```java
interface MyInterface {
    void add(int a, int b);
}
public class Main {
    public static void main(String[] args) {
        MyInterface m1 = (x, y) -> System.out.println(x + y);
        m1.add(2, 3); // 5
    }
}
```

2. **Method reference**
   - also used to access the method of functional interface, instead of writing logic separately using lambda expressions we can refer already existing methods, when the signature of the interface method is same as the static method or instance method or constructor 
   - It is an alternative to lambda expressions
   - denoted using ::

**3 types**

1. Reference to static method
2. Reference to instance method

    ```java
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
            // MyInterface m1 = () -> System.out.println("using lambda");
            // m1.show(); // using lambda

            // MyInterface m2 = Main::add;
            // m2.show(); // Reference to static method

            Main m = new Main();
            MyInterface m3 = m::demo;
            m3.show(); // Reference to instance method
        }
    }
    ```

3. Reference to Constructor

    ```java
    interface MyInterface {
        // Main show();
        Main show(String s);
    }
    public class Main {
        Main() {
            System.out.println("Using default constructor");
        }
        Main(String s) {
            System.out.println("Using constructor " + s);
        }
        public static void main(String[] args) {
            // MyInterface m1 = Main::new;
            // m1.show(); // Using default constructor

            MyInterface m2 = Main::new;
            m2.show("hello");  // Using constructor hello
        }
    }
    ```

### Predefined Functional interface - present in java.util.function.* pkg

1. **Consumer interface**
   - `void accept(T t)`

    ```java
    JDK 1.8 - void forEach(Consumer c) - used to iterate the elements of List and Set interface individually 
	
		List<String> l = new ArrayList<>();
		l.add("Ram");
		l.add("Sam");
		l.add("Bam");
		l.add("Tam");
		System.out.println(l); // [Ram, Sam, Bam, Tam]
		// l.forEach((e) -> System.out.println(e)); // using lambda expression for the consumer interface accept method, which takes T as arg.
		l.forEach(System.out::println); // Reference to instance method
    ```

2. **BiConsumer interface**
   - `void accept(T t, U u)`

    ```java
    JDK 1.8 - void forEach(BiConsumer c) - used to iterate the elements of Map interface individually 
    
    Map<Integer, String> hm = new HashMap<>();
		hm.put(10, "B");
		hm.put(5, "C");
		hm.put(1, "L");
		hm.put(3, "T");
		System.out.println(hm); // curly brace in random order
		hm.forEach((k, v) -> System.out.println("key = " + k + " value = " + v));
    
    
    ```

3. **Function interface**
   - `R apply(T t)`

4. **BiFunction interface**
   - `R apply(T t, U u)`

5. **Predicate interface**
   - `boolean test(T t)`

6. **BiPredicate interface**
   - `boolean test(T t, U u)`

7. **Supplier interface**
   - `T get()`

8. **BooleanSupplier interface**
   - `boolean getAsBoolean()`

9. **BinaryOperator interface extends BiFunction interface**
	 2 Operands and result are of same type in BiFunction.   
   - `R apply(T t, U u)`

10. **UnaryOperator interface extends Function interface**
	1 Operand and result are of same type in Function.
   - `R apply(T t)`


```java
public class Main {
	public static void main(String[] args) {
		List<String> l = new ArrayList<>();
		l.add("Ram");
		l.add("Sam");
		l.add("Bam");
		l.add("Tam");
		System.out.println(l); // [Ram, Sam, Bam, Tam]
		// l.forEach((e) -> System.out.println(e));
		l.forEach(System.out::println); // Reference to instance method

		Map<Integer, String> hm = new HashMap<>();
		hm.put(10, "B");
		hm.put(5, "C");
		hm.put(1, "L");
		hm.put(3, "T");
		System.out.println(hm); // curly brace in random order
		hm.forEach((k, v) -> System.out.println("key = " + k + " value = " + v));

		Function<String, Integer> f = (s) -> s.length();
		System.out.println(f.apply("hello")); // 5

		BiFunction<Integer, Integer, Integer> bf = (x1, x2) -> x1 + x2;
		System.out.println(bf.apply(10, 20)); // 30

		Predicate<String> p = (x) -> x.startsWith("Foo");
		System.out.println(p.test("Foobar")); // true

		BiPredicate<Integer, String> bp = (s1, s2) -> s1 > 20 && s2.startsWith("Foo");
		System.out.println(bp.test(25, "Foobar")); // true

		Supplier<String> su = () -> "hello";
		System.out.println(su.get()); // hello

		BooleanSupplier bs = () -> 10 > 20;
		System.out.println(bs.getAsBoolean()); // false

		BinaryOperator<String> bo = (y1, y2) -> y1.concat(y2);
		System.out.println(bo.apply("hello", "world")); // helloworld
	}
}
```

#### More Examples
```java

import java.util.function.BiConsumer;
import java.util.function.BiFunction;
import java.util.function.BiPredicate;
import java.util.function.BinaryOperator;
import java.util.function.BooleanSupplier;
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Predicate;
import java.util.function.Supplier;
import java.util.function.UnaryOperator;

public class Test {
	public static void main(String[] args) throws Exception {
		
		Consumer<String> consumer1 = (x)-> System.out.println(x);  // no Return
		consumer1.accept("Hello World!");           //Hello WOrld!
		
		BiConsumer<Integer, Integer> consumer2 = (x,y)-> System.out.println(x+y); //no return
		consumer2.accept(2,6);               //8
		
		Function<String,Integer> c3 = (s)-> s.length(); 
		Integer i = c3.apply("Thank you!");
		System.out.println(i);               //10
		
		
		BiFunction<Integer,Integer,Integer> c4 = (a,b) -> a+b;
		Integer j= c4.apply(6,7);
		System.out.println(j);             //13
		
		Supplier<Integer> c5 = ()-> ("Hi!").length();  //only returns, no arg as parameter
		Integer k = c5.get();
		System.out.println(k);             //3
		
		BooleanSupplier bs = ()-> ("Apple").contains("a");  //returns boolean , no BiSuppiler as we can'r return 2 values
		Boolean b=bs.getAsBoolean();
		System.out.println(b); //false
		
		Predicate<String> pd = (t)-> t instanceof String;   //returns boolean
		Boolean pdb = pd.test("Apple");
		System.out.println(pdb);  //true
		
		BiPredicate<Integer,Integer>  bp = (t,u)-> t%u ==0;  //returns boolean
		Boolean bpb = bp.test(18,6);  
		System.out.println(bpb); //true
		
		BinaryOperator<String> bo = (t,u)-> t.concat(u); //Remember only one parameterized type
		String boa = bo.apply("Hello"," World!"); //Take 2 strings and returns string --> Same type
		System.out.println(boa);  // Hello World!
		
		UnaryOperator<Integer> uo = (t)->t*t; 
		Integer l = uo.apply(5);		//Takes an Integer and returns an Integer --> Same type
		System.out.println(l);   //25
		
	}
}
```