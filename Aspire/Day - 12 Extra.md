

## 6. Functional Interface 
   - It is an interface that contains only one abstract method and any number of default or static methods
   - To check whether interface is functional interface or not, we can use @FunctionalInterface annotation
   - Predefined Functional Interfaces
	   1. Predicate<T> - boolean test(T t)
	   2. Function<T,R> - R apply(T t)
	   3. Consumer<T> - void accept(T t)
      1. Supplier<T> - T get()
      2. UnaryOperator<T> - T apply(T t)
      3. BinaryOperator<T> - T apply(T t1, T t2)
      4. Runnable - void run()
      5. Callable<V> - V call()









``` java
@FunctionalInterface
interface MyInterface {
    void show();
    default void add() {
        System.out.println("Inside add");
    }
    static void sum() {
        System.out.println("Inside sum");
    }
}
public class Main {
    public static void main(String[] args)  {
        MyInterface m=new MyInterface() {
            @Override
            public void show() {
                System.out.println("Inside show");
            }
        };
        m.show();
        m.add();
        MyInterface.sum();
        
        MyInterface m1=()->System.out.println("Inside show using lambda");
        m1.show();
        m1.add();
        MyInterface.sum();
    }
}
```

## 7. Lambda Expression
   - It is an anonymous function which doesn't contain any name, return type, modifier
   - It is mainly used to write more readable and maintainable code
   - There are mainly 2 types of lambda expression, one without arguments and another one with arguments
   - Without Arguments
      1. () -> {
              statement1;
              statement2;
              ...
         };
   - With Arguments
      1. (int a,int b) -> {
              statement1;
              statement2;
              ...
         };
   - It can be stored inside a variable and used whenever required

```java
interface A {
    void show();
}
public class Main {
    public static void main(String[] args)  {
        A a=new A() {
            @Override
            public void show() {
                System.out.println("Inside show");
            }
        };
        a.show();
        
        A a1=()->System.out.println("Inside show using lambda");
        a1.show();
    }
}
```

## 8. Stream API
   - It is used to process the object from a collection
   - There are mainly 3 types of operations available in the stream API
      1. Intermediate Operation - used to create a stream, applied to a stream and return the stream
      2. Terminal Operation - used to close the stream and return the final result
      3. Short-circuit Operation - used to stop the process in the middle and return the result
   - To create a stream there are 4 ways available
      1. From the collection
      2. Using stream of method
      3. Using stream ofNullable method
      4. Using iterate and generate method

```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;
public class Main {
    public static void main(String[] args) {
        List<Integer> l=new ArrayList<>();
        l.add(0);l.add(5);l.add(10);l.add(15);l.add(20);l.add(25);
        
        // Traditional way
        for(int i:l) {
            if(i%2==0) {
                System.out.println(i);
            }
        }
        
        // Stream API
        l.stream().filter(i->i%2==0).forEach(System.out::println); // Intermediate and Terminal operation
        
        List<Integer> l1=l.stream().filter(i->i%2==0).collect(Collectors.toList());
        System.out.println(l1); // Intermediate and Terminal operation
        System.out.println(l.stream().count());
        System.out.println(l.stream().findFirst());
        System.out.println(l.stream().findAny());
        System.out.println(l.stream().max((i1,i2)->i1.compareTo(i2)));
        System.out.println(l.stream().min((i1,i2)->i1.compareTo(i2)));
        System.out.println(l.stream().allMatch(i->i%2==0));
        System.out.println(l.stream().anyMatch(i->i%2==0));
        System.out.println(l.stream().noneMatch(i->i%2==0));
        System.out.println(l.stream().sorted((i1,i2)->-i1.compareTo(i2)).collect(Collectors.toList()));
        
        // Short circuit
        System.out.println(l.stream().skip(2).collect(Collectors.toList())); // Skip first 2 elements
        System.out.println(l.stream().limit(2).collect(Collectors.toList())); // Print first 2 elements
        
        // map method
        System.out.println(l.stream().map(i->i*2).collect(Collectors.toList()));
        
        // reduce method
        System.out.println(l.stream().reduce(0,(i1,i2)->i1+i2));
    }
}
```


## 9. New features in JDK 9
   - JShell - It is an interactive tool to test Java code
   - Platform Logging API and Service
   - Jigsaw - It is used to define the modules in the project
   - Java Platform Module System
   - Factory Methods for Collection - It is used to create unmodifiable collections
   - Private Methods in Interface
   - Try-With-Resource - Used to auto-close the resources after the try block
   - ImmutableSet, ImmutableMap, ImmutableList - create an immutable list, map, and set respectively

## 10. Module
   - It is used to split the project into different modules
   - It contains module-info.java file, which contains module keyword followed by module name and exports package name
   - It is mainly used to improve encapsulation, security, and performance
   - Module can only access the exported package from another module

## 11. HttpClient
   - Used to send and receive the request and response in the form of JSON
   - java.net.http package
   - Get, Post, Put, Delete, and other methods available

## 12. java.util.logging
   - It is a platform logging API used to record the log messages
   - It is a part of the java.util.logging package
   - We can create a logger object and print the log messages using different levels (SEVERE, WARNING, INFO, CONFIG, FINE, FINER, FINEST)

## 13. Stream API improvements
   - Stream.iterate()
   - Stream.ofNullable()
   - Collectors.toUnmodifiableList(), Collectors.toUnmodifiableMap(), Collectors.toUnmodifiableSet()

## 14. Multi-Release JAR Files
   - Used to

 include different versions of classes for different JDK releases
   - Folder structure META-INF/versions/JDK_Version
   - It is used when JDK is backward compatible

## 15. Local Variable Type Inference
   - It is a part of the JEP 286
   - It is used to reduce the verbosity in the code
   - It is used to infer the datatype of the variable based on the initial value
   - Used inside the method, loop, constructor, and lambda expression

## 16. Process API Updates
   - It is a part of the JEP 102 and JEP 251
   - It is used to control and manage the operating system processes
   - ProcessHandle, ProcessHandle.Info, and ProcessBuilder classes available
   - ProcessHandle is an interface that contains methods to handle the operating system process
   - ProcessHandle.Info is an interface that contains methods to get the process information
   - ProcessBuilder is a class used to start the operating system process

## 17. Reactive Programming
   - It is a paradigm used to handle the asynchronous data streams
   - It is mainly used to handle the unbounded streams of data
   - Flow API contains 4 main components
      1. Publisher - It is used to publish the data
      2. Subscriber - It is used to receive the data
      3. Subscription - It is used to control the flow of data
      4. Processor - It is used to process the data

## 18. Optional class improvements
   - There are 3 new methods available
      1. or() - return the value if present otherwise return the value from the supplier
      2. ifPresentOrElse() - if value is present it invokes the consumer otherwise it invokes the runnable
      3. stream() - return a sequential stream with single element if the value is present otherwise return an empty stream

## 19. Stack-Walking API
   - It is a part of the JEP 259
   - It is used to walk over the stack trace elements
   - StackWalker and StackFrame classes are available
   - StackWalker is a final class used to walk over the stack trace
   - StackFrame is an interface that contains methods to get the information about the stack frame

## 20. Miscellaneous Updates
   - Performance improvement in G1 Garbage Collector
   - String in switch expression
   - New methods in the Optional class
   - New methods in the CompletableFuture class
   - New methods in the ProcessBuilder class
   - New methods in the Arrays class

## 21. Serialization Filtering
   - It is a part of the JEP 290
   - It is used to filter the stream before serialization and after deserialization
   - It is mainly used to prevent the security vulnerability

## 22. Z Garbage Collector
   - It is a part of the JEP 333
   - It is used to improve the performance of the garbage collector
   - It is a scalable low-latency garbage collector

## 23. Foreign Function and Memory API
   - It is a part of the JEP 191 and JEP 370
   - It is used to write the native code in Java
   - MemorySegment, MemoryAddress, and MemoryAccess classes available
   - MemorySegment is a final class used to represent a contiguous range of memory
   - MemoryAddress is a final class used to represent a memory address
   - MemoryAccess is a final class used to perform the memory access operation

## 24. Enhanced SecureRandom
   - It is a part of the JEP 273
   - It is used to generate the cryptographically strong random number

## 25. Collection Factory Methods
   - It is a part of the JEP 269
   - Used to create the unmodifiable collections

## 26. Deprecation
   - java.lang.SecurityManager.checkTopLevelWindow(Object) method
   - Stack walking API methods - StackStreamElement.getClassName(), StackStreamElement.getMethodName(), StackStreamElement.getFileName(), StackStreamElement.getLineNumber(), StackStreamElement.getByteCodeIndex() methods
   
## 27. Removal
   - Applet API
   
## 28. Locale enhancement
   - Compact Number Formatting (e.g., 4K, 2M)
   - Currency formatting with the currency code, currency symbol, and display name
   - Additional number system: Tamil, Bengali, Telugu, Kannada, Malayalam, Gujarati, Gurmukhi, Oriya

## 29. VarHandle
   - It is a part of the JEP 193
   - It is used to perform the volatile and atomic operation
   - Used to perform the unsafe operation

## 30. Pattern Matching for the instanceof Operator
   - It is a part of the JEP 305
   - It is used to simplify the code of the instanceof operator
   - instanceof followed by a pattern is used to test and assign the value of the variable
   
```java
public class Main {
    public static void main(String[] args) {
        Object o=new String("John");
        if(o instanceof String s) {
            System.out.println(s.length()); // 4
        }
    }
}
```

