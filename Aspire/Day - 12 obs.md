
*Date : 05.10.2024*

// Before JDK1.8, Date class present in java.util.* package

### 1. Date class
   - Print data and time
### 2. Calendar class
   - Abstract class, used to extract some useful info from date and time component
### 3. GregorianCalendar class
   - Concrete implementation of Calendar class, used to extract some useful info from date and time component
### 4. DateFormat class - present in java.text.* package
   - Abstract class, used for formatting (convert date to String) and at the time of formatting, we can display date in different format - SHORT, LONG, FULL, MEDIUM
   - Used for parsing (convert String to Date)

### 5. SimpleDateFormat class - present in java.text.* package
   - Concrete implementation of DateFormat class, used for formatting (convert date to String) and display in our own format and parsing (convert String to Date)

```java
public class Main {
    public static void main(String[] args) {
       Date d1=new Date();  // Default constructor, prints current date and time
       System.out.println(d1); // Fri May 10 13:05:23 IST 2024
       Date d2=new Date(100000); // Print date and time from Jan 1st 1970
       System.out.println(d2); // Thu Jan 01 05:31:40 IST 1970
       
       Calendar c1=Calendar.getInstance();  // Current date and time
       System.out.println(c1.get(Calendar.YEAR)); // 2024
       System.out.println(c1.get(Calendar.MONTH)); // 4
       System.out.println(c1.get(Calendar.DAY_OF_MONTH));
       
       GregorianCalendar g1=new GregorianCalendar(); // Current date and time
       System.out.println(g1.get(Calendar.YEAR)); // 2024
       System.out.println(g1.get(Calendar.MONTH)); // 4
       
       GregorianCalendar g2=new GregorianCalendar(2000,10,20,14,23,34); // Create your own date and time
       System.out.println(g2.get(Calendar.YEAR)); // 2000
       System.out.println(g2.get(Calendar.MONTH)); // 9
       
       DateFormat df=DateFormat.getInstance(); // By default display both date and time in short format
       String s=df.format(d1);
       System.out.println(s); // 5/10/24, 1:18 PM
       df=DateFormat.getDateInstance(DateFormat.MEDIUM); // Only date in medium format
       String s1=df.format(d1);
       System.out.println(s1); // May 10, 2024
       df=DateFormat.getTimeInstance(DateFormat.LONG); // Only time in long format
       String s2=df.format(d1);
       System.out.println(s2); // 1:20:49 PM IST
       df=DateFormat.getDateTimeInstance(DateFormat.FULL,DateFormat.MEDIUM); // Display both date and time in full and medium format respectively
       String s3=df.format(d1);
       System.out.println(s3);
       
       String s4="10/04/2024";
       SimpleDateFormat sdf=new SimpleDateFormat("dd/MM/yyyy");
       Date d3=null;
       try {
                 d3=sdf.parse(s4);
                 System.out.println(d3); // Wed Apr 10 00:00:00 IST 2024
       }catch(ParseException p) {
                 System.out.println(p);
       }
       SimpleDateFormat sdf1=new SimpleDateFormat("yyyy-MM-dd");
       String s5=sdf1.format(d3);
       System.out.println(s5);// 2000-04-10
       
    }
}
```

## 1. Date API
   - Available from JDK1.8 onwards
   - Present in java.time.* package
   - Date is immutable class whereas lower version of Date is not immutable
### class and interface
1. LocalDate class - print only date - yyyy-MM-dd
2. TemporalAdjuster interface - used to get extra info about date and time
3. TemporalAdjusters class 
4. LocalTime class - print only time
5. LocalDateTime class - print both date and time yyyy-MM-ddThh::mm:ss
6. Period class - used to find difference between 2 dates
7. Duration class - used to find difference between 2 times
8. DateTimeFormatter interface - used to format the date and time in different style


```java
public class Main {
    public static void main(String[] args) {
       LocalDate l1=LocalDate.now(); // Current date
       System.out.println(l1); // 2024-05-10
       
       Clock c1=Clock.systemDefaultZone();
       LocalDate l2=LocalDate.now(c1);
       System.out.println(l2); // 2024-05-10
       
       ZoneId z=ZoneId.of("Europe/Paris");
       LocalDate l3=LocalDate.now(z);
       System.out.println(l3); // 2024-05-10
       
       LocalDate l4=LocalDate.of(2000, 10, 20); // Create our own date
       System.out.println(l4); // 2000-10-20
       
       LocalDate l5=LocalDate.parse("2000-10-20"); // Convert string to date
       System.out.println(l5); // 2000-10-20
       
       LocalDate l6=l5.plusMonths(2);
       System.out.println(l6); // 2000-12-20
       LocalDate l7=l6.plus(20, ChronoUnit.YEARS);
       System.out.println(l7); // 2020-12-20
       
       LocalDate l8=l7.minusDays(200);
       System.out.println(l8);
       LocalDate l9=l8.minus(20, ChronoUnit.WEEKS);
       System.out.println(l9);
       
       DayOfWeek d1=LocalDate.parse("2024-05-10").getDayOfWeek();
       System.out.println(d1); // Friday
       int m1=LocalDate.parse("2024-05-10").getDayOfMonth();
       System.out.println(m1); // 10
       int y1=LocalDate.parse("2024-05-10").getDayOfYear();
       System.out.println(y1);
       int m2=LocalDate.parse("2024-05-10").getMonthValue();
       System.out.println(m2); // 5
       System.out.println(l9.isLeapYear());
       
       boolean b1=LocalDate.parse("2024-05-10").isAfter(LocalDate.parse("2024-05-11"));
       System.out.println(b1); // false
       boolean b2=LocalDate.parse("2024-05-10").isBefore(LocalDate.parse("2024-05-11"));
       System.out.println(b2); // true
       boolean b3=LocalDate.parse("2024-05-10").isEqual(LocalDate.parse("2024-05-11"));
       System.out.println(b3); // false
       
       LocalDate l10=LocalDate.now().with(TemporalAdjusters.firstDayOfMonth());
       System.out.println(l10); // 2024-05-01
       LocalDate l11=LocalDate.now().with(TemporalAdjusters.lastDayOfMonth());
      

 System.out.println(l11); // 2024-05-31
       LocalDate l12=LocalDate.now().with(TemporalAdjusters.firstDayOfYear());
       System.out.println(l12); // 2024-01-01
       LocalDate l13=LocalDate.now().with(TemporalAdjusters.next(DayOfWeek.SATURDAY));
       System.out.println(l13); // 2024-05-11
       LocalDate l14=LocalDate.now().with(TemporalAdjusters.previous(DayOfWeek.THURSDAY));
       System.out.println(l14); // 2024-05-09
       
       LocalTime t1=LocalTime.now(); // Current time
       System.out.println(t1);
       LocalTime t2=LocalTime.now(z);
       System.out.println(t2);
       LocalTime t3=LocalTime.of(9, 30);
       System.out.println(t3); // 9:30
       LocalTime t4=LocalTime.parse("09:30");
       System.out.println(t4);
       
       LocalTime t5=t4.plusMinutes(23);
       System.out.println(t5); // 9:53
       LocalTime t6=t5.plus(4, ChronoUnit.HOURS);
       System.out.println(t6);
       LocalTime t7=t6.minusNanos(20000);
       System.out.println(t7);
       LocalTime t8=t7.minus(200, ChronoUnit.SECONDS);
       System.out.println(t8);
       System.out.println(LocalTime.MAX);
       System.out.println(LocalTime.MIN);
       System.out.println(LocalTime.MIDNIGHT);
       
       LocalDateTime ld1=LocalDateTime.now();
       System.out.println(ld1); // 2024-05-10T13:54:49.427964700
       LocalDateTime ld2=LocalDateTime.of(LocalDate.now(), LocalTime.now());
       System.out.println(ld2);
       LocalDateTime ld3=LocalDateTime.parse("2024-05-10T13:54:49");
       System.out.println(ld3);
       System.out.println(ld3.toLocalDate());
       System.out.println(ld3.toLocalTime());
       System.out.println(LocalDateTime.MAX);
       System.out.println(LocalDateTime.MIN);
       
       // Convert JDK1.5 date to JDK1.8
       Date d11=new Date(); 
       LocalDateTime ld4=LocalDateTime.ofInstant(d11.toInstant(), ZoneId.systemDefault());
       System.out.println(ld4);
       
       // Convert Calendar to JDK1.8 localdate
       Calendar c11=Calendar.getInstance();
       LocalDateTime ld5=LocalDateTime.ofInstant(c11.toInstant(), ZoneId.systemDefault());
       System.out.println(ld5);
       
       LocalDate l15=LocalDate.now();
       LocalDate l16=LocalDate.of(2000, 10, 20);
       int diff1=Period.between(l15, l16).getYears();
       System.out.println(diff1);
       int diff2=Period.between(l15, l16).getMonths();
       System.out.println(diff2);
       long diff3=ChronoUnit.DAYS.between(l16, l15);
       System.out.println(diff3);
       
       LocalTime t9=LocalTime.now();
       LocalTime t10=LocalTime.of(10, 30);
       long diff4=Duration.between(t9, t10).getSeconds();
       System.out.println(diff4);
       long diff5=Duration.between(t9, t10).toMinutes();
       System.out.println(diff5);
       long diff6=Duration.between(t9, t10).toHours();
       System.out.println(diff6);
       long diff7=ChronoUnit.SECONDS.between(t9, t10);
       System.out.println(diff7);
       
       LocalDateTime ld6=LocalDateTime.now();
       String s=ld6.format(DateTimeFormatter.ISO_LOCAL_DATE);
       System.out.println(s);
       String s1=ld6.format(DateTimeFormatter.ofPattern("dd/MM/yyyy"));
       System.out.println(s1);
       String s2=ld6.format(DateTimeFormatter.ofLocalizedDate(FormatStyle.SHORT));
       System.out.println(s2);
       String s3=ld6.format(DateTimeFormatter.ofLocalizedTime(FormatStyle.MEDIUM));
       System.out.println(s3);
       String s4=ld6.format(DateTimeFormatter.ofLocalizedDateTime(FormatStyle.LONG,FormatStyle.FULL));
       System.out.println(s4);
    }
}
```

## 2. Optional class
   - Present in java.util.* package
   - Object will contain memory reference or null reference, so if we access anything using null reference we get NullPointerException
   - To avoid NPE we have to write code to do null check, so to avoid the unpredictable NPE we can go for Optional class
### Methods
1. static Optional empty() - create empty optional
2. static Optional of(T...t) - return a non-empty optional, if value is null returns NPE
3. static Optional ofNullable(T...t) - return a non-empty optional, if value is null returns empty optional
4. Object get() - return original value from Optional
5. void ifPresent(Consumer) - if value is present it invokes related Consumer
6. boolean isPresent() - return true if value is present otherwise false 
7. boolean isEmpty() - Java11 - check whether optional is empty or not 
8. Object orElse(Object) - return the value if present otherwise return other value
9. Object orElseGet(Supplier) - return the value if present otherwise it invokes another logic 
10. Object orElseThrow(Supplier) - return the value if present otherwise it throws an exception


```java
public class Main {
    public static void main(String[] args) throws Throwable {
      Optional op1=Optional.empty();
      System.out.println(op1); // Optional.empty
      Optional op2=Optional.of("John");
      System.out.println(op2); // Optional[John]
      // Optional op3=Optional.of(null);
      // System.out.println(op3); // NPE


      Optional op4=Optional.ofNullable("Jack");
      System.out.println(op4); // Optional[Jack]
      Optional op5=Optional.ofNullable(null);
      System.out.println(op5); // Optional.empty
      
      Optional op6=Optional.of("John");
      System.out.println(op6); // Optional[John]
      System.out.println(op6.get()); // John
      op6.ifPresent(System.out::println); // John
      System.out.println(op6.isPresent()); // true
      op6.empty();
      op6.ifPresent(System.out::println);
      System.out.println(op6.isEmpty()); // true
      
      Optional op7=Optional.empty();
      System.out.println(op7.isPresent()); // false
      System.out.println(op7.orElse("Jim")); // Jim
      System.out.println(op7.orElseGet(()->"Jam")); // Jam
      System.out.println(op7.orElseThrow(NullPointerException::new));
    }
}
```

## 3. Default and static method in interface
   - Till JDK1.7, the interface will contain only abstract methods and public static final variables
   - From JDK1.8, apart from abstract method interface also contains default and static methods
   - Without affecting the implemented classes, if we want to add any new methods inside the interface then we can go for default methods
   - If my functionality is no way related to the object (i.e.) static method, instead of defining inside the class we can define inside the interface
   - From JDK1.9, the interface also contains private and private static methods, if we have common functionalities inside default method and to avoid duplicate code, we can define those common functionalities inside private method and access whenever it is needed 

```java
interface A {
    default void show() {
        System.out.println("Inside A's show");
    }
}
interface B {
    default void show() {
        System.out.println("Inside B's show");
    }
}
class C implements A,B {
    @Override
    public void show() {
        A.super.show();
        B.super.show();
    }
}

public class Main {
    public static void main(String[] args)  {
       C c=new C();
       c.show();
    }
}
```

## Interface Access members

1. Accessible from default and private methods within interface
   - Constant variable = yes
   - Abstract method = yes
   - Another default method = yes
   - Private method = yes
   - Static method = yes
   - Private static method = yes

2. Accessible from static methods within interface
   - Constant variable = yes
   - Abstract method = no
   - Another default method = no
   - Private method = no
   - Static method = yes
   - Private static method = yes

3. Accessible from instance methods by implementing interface
   - Constant variable = yes
   - Abstract method = yes
   - Another default method = yes
   - Private method = no
   - Static method = yes
   - Private static method = no

4. Accessible outside interface without implementing
   - Constant variable = yes
   - Abstract method = no
   - Another default method = no
   - Private method = no
   - Static method = yes
   - Private static method = no

```java
interface MyInterface {
    // Till JDK1.7
    /*public static final*/int CONSTANT =1;
    /*public abstract*/ int abstractMethod();
    
    // From JDK1.8
    /*public*/ default int defaultMethod() {
        abstractMethod();
        privateMethod();
        staticMethod();
        privateStaticMethod();
        return CONSTANT;
    }
    /*public*/ static int staticMethod() {
        privateStaticMethod();
        return CONSTANT;
    }
    
    // From JDK1.9
    private int privateMethod() {
        abstractMethod();
        defaultMethod();
        staticMethod();
        privateStaticMethod();
        return CONSTANT;
    }
    private static int privateStaticMethod() {
        staticMethod();
        return CONSTANT;
    }
}
class Example implements MyInterface {
    @Override
    public int abstractMethod() {
        defaultMethod();
        MyInterface.staticMethod();
        return CONSTANT;
    }
}
class Example1 {
    public int instanceMethod() {
        MyInterface.staticMethod();
        return MyInterface.CONSTANT;
    }
}

public class Main {
    public static void main(String[] args)  {
      
    }
}

```

## 4. var keyword
   - Available from JDK10
   - Used to infer the datatype at runtime based on the value
	   `var a = 10;`
   - Used only inside constructor, methods, loops, and compound blocks
### Rules
1. var can't declare without initial value
2. var can be declared in the first line and initialized in the second line
3. var cannot be initialized with a null value without a type
4. var is not permitted in multiple variable declaration 
5. var cannot be used to initialize an array 
6. var is a reserved type name but not a reserved keyword, so we can use var as an identifier except for interface, class, enum
7. var in a lambda expr, but you can't mix var and non-var parameters 

```java
interface MyInterface {
              void add(int a,int b);
}

class Var {
    Var() {
        var var="var"; //correct
    }
    public void var() { //correct
        Var var=new Var(); //correct
    }
}
// interface var { } // error
// class var { } // error
// enum var { } // error
public class Main {
    Main() {
        var a1="hello";
    }
    {
        var a2=10;
    }
    public static void main(String[] args)  {
        var size=20;
        for(var i=0;i<5;i++) {
            System.out.println(i);
        }
        
        // var x; // error
        var x=1;
        var y
             =2;
       // var c1=null; // error
        var c1=(String) null;
        var c2="hello";
        c2=null;
        
        int a=10,b=20;
        // var a1=10,b1=20; /// error
        // var a[]= {1,2,3}; // error
        
        MyInterface m1=(var a1,var b1)->System.out.println(a1+b1);  // correct
        // MyInterface m2=(var a1,int b1)->System.out.println(a1+b1);  // error
    }
}
```

## 5. enum 
   - It is a type of class that mainly stores constants or a fixed set of values 
   - It is implicitly an abstract class, by default it is final so we can't inherit but it can be implemented by an interface 

```java
interface A {
    void add();
}
enum Day1 implements A{
    SUNDAY,MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY;

    @Override
    public void add() {
        // TODO Auto-generated method stub
    }
}
/*enum Day2 extends Day1 {  //error
              
}*/
enum Day{
    SUNDAY,MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY
}

public class Main {
    public static void main(String[] args)  {
        Day d1=Day.TUESDAY;
        System.out.println(d1); //TUESDAY
        Day d2=d1;
        System.out.println(d2); //TUESDAY
       // Day d3=10;  //error
        Day d4=Day.valueOf("MONDAY");
        System.out.println(d4); //MONDAY
       // Day d5=Day.valueOf("MONDAYS");
       // System.out.println(d5); //IllegalArgumentException
        System.out.println(d1==d2);  //true
        System.out.println(d1.equals(d2)); //true
        
        for(Day d:Day.values()) {
              System.out.println(d.name()+" "+d.ordinal());
        }
    }
}
```


## Rules
1. `enum` values are declared first, then only we can define anything

```java
enum Day {
    // int a=10; //error
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY;
    int a = 10; // correct
}
```

2. A non final enum method can be 
```java
enum Day {
    SUNDAY {
        public void print() {
            System.out.println("very hot");
        }
    },
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY;

    public void print() {
        System.out.println("hot");
    }
}

public class Main {
    public static void main(String[] args) {
        Day d1 = Day.TUESDAY;
        d1.print(); // hot
        Day.SUNDAY.print(); // very hot
    }
}

```

3. If we have abstract method then it should be overridden by all enum value
```java
enum Day {
    SUNDAY {
        public void print() {
            System.out.println("very hot");
        }
    },
    MONDAY {
        public void print() {
            System.out.println("hot");
        }
    },
    TUESDAY {
        public void print() {
            System.out.println("cold");
        }
    },
    WEDNESDAY {
        public void print() {
            System.out.println("very cold");
        }
    },
    THURSDAY {
        public void print() {
            System.out.println("mist");
        }
    },
    FRIDAY {
        public void print() {
            System.out.println("very mist");
        }
    },
    SATURDAY {
        public void print() {
            System.out.println("average hot");
        }
    };

    abstract void print();
}

public class Main {
    public static void main(String[] args) {
        Day d1 = Day.TUESDAY;
        d1.print(); // cold
        Day.SUNDAY.print(); // very hot
    }
}
```

4. Constructor is implicitly private, called only once in the beginning to create enum value 
```java
enum Day {
    SUNDAY("very hot") {
        public void print() {
            System.out.println("very hot");
        }
    },
    MONDAY("hot") {
        public void print() {
            System.out.println("hot");
        }
    },
    TUESDAY("cold") {
        public void print() {
            System.out.println("cold");
        }
    },
    WEDNESDAY("very cold") {
        public void print() {
            System.out.println("very cold");
        }
    },
    THURSDAY("mist") {
        public void print() {
            System.out.println("mist");
        }
    },
    FRIDAY("very mist") {
        public void print() {
            System.out.println("very mist");
        }
    },
    SATURDAY("average hot") {
        public void print() {
            System.out.println("average hot");
        }
    };

    String temp;

    /*private*/ Day(String temp) {
        this.temp = temp;
    }

    abstract void print();
}

public class Main {
    public static void main(String[] args) {
        Day d1 = Day.TUESDAY;
        d1.print(); // cold
        Day.SUNDAY.print(); // very hot

        for (Day d : Day.values()) {
            System.out.println(d + " " + d.temp);
        }
    }
}

enum Marks {
    ENGLISH(88),
    MATHS(100),
    SCIENCE(90),
    SOCIAL(100),
    LANGUAGE(90);

    int mark;

    Marks(int mark) {
        this.mark = mark;
    }
}

public class Main {
    public static void main(String[] args) {
        for (Marks m : Marks.values()) {
            System.out.println(m + " " + m.mark);
        }
    }
}
```



5. enum can also used in switch case
```java
enum Day {
    // int a=10; //error
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY;
    int a = 10; // correct
}

public class Main {
    public static void main(String[] args) {
        Day d1 = Day.FRIDAY;
        System.out.println(d1.a); // 10
        
        switch (d1) {
            case SUNDAY:
                System.out.println("Very hot");
                break;
            case MONDAY:
                System.out.println("hot");
                break;
            default:
                System.out.println("average hot");
                break;
        }
    }
}

```














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

