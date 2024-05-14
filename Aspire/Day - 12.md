
*Date : 05.10.2024*


Before JDK1.8, Date class present in java.util.* package

1. Date class
      - print data and time 

2. Calendar class
      - abstract class, used to extract some useful info from date and time component

3. GregorianCalendar class
      - concrete implementation of Calendar class, used to extract some useful info from date and time component

4. DateFormat class - present in java.text.* package
       - abstract class, used for formatting(convert date to String) and at time of formatting we can display date in different format - SHORT, LONG, FULL, MEDIUM
      - used for parsing(convert String to Date)

5. SimpleDateFormat class - present in java.text.* package
        - concrete implementation of DateFormat class, used for formatting(convert date to String) and display in our own format and parsing(convert String to Date)

public class Main {
    public static void main(String[] args) {
       Date d1=new Date();  //default constructor, prints current date and time
       System.out.println(d1); //Fri May 10 13:05:23 IST 2024
       Date d2=new Date(100000); //print date and time from Jan 1st 1970
       System.out.println(d2); //Thu Jan 01 05:31:40 IST 1970
       
       Calendar c1=Calendar.getInstance();  //current date and time
       System.out.println(c1.get(Calendar.YEAR)); //2024
       System.out.println(c1.get(Calendar.MONTH)); //4
       System.out.println(c1.get(Calendar.DAY_OF_MONTH));
       
       GregorianCalendar g1=new GregorianCalendar(); //current date and time
       System.out.println(g1.get(Calendar.YEAR)); //2024
       System.out.println(g1.get(Calendar.MONTH)); //4
       
       GregorianCalendar g2=new GregorianCalendar(2000,10,20,14,23,34); //create ur own date and time
       System.out.println(g2.get(Calendar.YEAR)); //2000
       System.out.println(g2.get(Calendar.MONTH)); //9
       
       DateFormat df=DateFormat.getInstance(); //by default display both date and time in short format
       String s=df.format(d1);
       System.out.println(s); //5/10/24, 1:18 PM
       df=DateFormat.getDateInstance(DateFormat.MEDIUM); //only date in medium format
       String s1=df.format(d1);
       System.out.println(s1); //May 10, 2024
       df=DateFormat.getTimeInstance(DateFormat.LONG); //only time in long format
       String s2=df.format(d1);
       System.out.println(s2); //1:20:49 PM IST
       df=DateFormat.getDateTimeInstance(DateFormat.FULL,DateFormat.MEDIUM); //display both date and time in full and medium format resp
       String s3=df.format(d1);
       System.out.println(s3);
       
       String s4="10/04/2024";
       SimpleDateFormat sdf=new SimpleDateFormat("dd/MM/yyyy");
       Date d3=null;
       try {
                 d3=sdf.parse(s4);
                 System.out.println(d3); //Wed Apr 10 00:00:00 IST 2024
       }catch(ParseException p) {
                 System.out.println(p);
       }
       SimpleDateFormat sdf1=new SimpleDateFormat("yyyy-MM-dd");
       String s5=sdf1.format(d3);
       System.out.println(s5);//2000-04-10
       
       
    }
}

1. Date API
    - Available from JDK1.8 onwards
    - present in java.time.* package
    - Date is immutable class whereas lower version of Date is not immutable 

class and interface
1. LocalDate class - print only date - yyyy-MM-dd
2. TemporalAdjuster interface - used to get extra info about date and time
3. TemporalAdjusters class 
4. LocalTime class - print only time
5. LocalDateTime class - print both date and time yyyy-MM-ddThh::mm:ss
6. Period class - used to find difference between 2 dates
7. Duration class - used to find difference between 2 times
8. DateTimeFormatter interface - used to format the date and time in different style

public class Main {
    public static void main(String[] args) {
       LocalDate l1=LocalDate.now(); //current date
       System.out.println(l1); //2024-05-10
       
       Clock c1=Clock.systemDefaultZone();
       LocalDate l2=LocalDate.now(c1);
       System.out.println(l2); //2024-05-10
       
       ZoneId z=ZoneId.of("Europe/Paris");
       LocalDate l3=LocalDate.now(z);
       System.out.println(l3); //2024-05-10
       
       LocalDate l4=LocalDate.of(2000, 10, 20); //create our own date
       System.out.println(l4); //2000-10-20
       
       LocalDate l5=LocalDate.parse("2000-10-20"); //convert string to date
       System.out.println(l5); //2000-10-20
       
       LocalDate l6=l5.plusMonths(2);
       System.out.println(l6); //2000-12-20
       LocalDate l7=l6.plus(20, ChronoUnit.YEARS);
       System.out.println(l7); //2020-12-20
       
       LocalDate l8=l7.minusDays(200);
       System.out.println(l8);
       LocalDate l9=l8.minus(20, ChronoUnit.WEEKS);
       System.out.println(l9);
       
       DayOfWeek d1=LocalDate.parse("2024-05-10").getDayOfWeek();
       System.out.println(d1); //Friday
       int m1=LocalDate.parse("2024-05-10").getDayOfMonth();
       System.out.println(m1); //10
       int y1=LocalDate.parse("2024-05-10").getDayOfYear();
       System.out.println(y1);
       int m2=LocalDate.parse("2024-05-10").getMonthValue();
       System.out.println(m2); //5
       System.out.println(l9.isLeapYear());
       
       boolean b1=LocalDate.parse("2024-05-10").isAfter(LocalDate.parse("2024-05-11"));
       System.out.println(b1); //false
       boolean b2=LocalDate.parse("2024-05-10").isBefore(LocalDate.parse("2024-05-11"));
       System.out.println(b2); //true
       boolean b3=LocalDate.parse("2024-05-10").isEqual(LocalDate.parse("2024-05-11"));
       System.out.println(b3); //false
       
       LocalDate l10=LocalDate.now().with(TemporalAdjusters.firstDayOfMonth());
       System.out.println(l10); //2024-05-01
       LocalDate l11=LocalDate.now().with(TemporalAdjusters.lastDayOfMonth());
       System.out.println(l11); //2024-05-31
       LocalDate l12=LocalDate.now().with(TemporalAdjusters.firstDayOfYear());
       System.out.println(l12); //2024-01-01
       LocalDate l13=LocalDate.now().with(TemporalAdjusters.next(DayOfWeek.SATURDAY));
       System.out.println(l13); //2024-05-11
       LocalDate l14=LocalDate.now().with(TemporalAdjusters.previous(DayOfWeek.THURSDAY));
       System.out.println(l14); //2024-05-09
       
       LocalTime t1=LocalTime.now(); //current time
       System.out.println(t1);
       LocalTime t2=LocalTime.now(z);
       System.out.println(t2);
       LocalTime t3=LocalTime.of(9, 30);
       System.out.println(t3); //9:30
       LocalTime t4=LocalTime.parse("09:30");
       System.out.println(t4);
       
       LocalTime t5=t4.plusMinutes(23);
       System.out.println(t5); //9:53
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
       System.out.println(ld1); //2024-05-10T13:54:49.427964700
       LocalDateTime ld2=LocalDateTime.of(LocalDate.now(), LocalTime.now());
       System.out.println(ld2);
       LocalDateTime ld3=LocalDateTime.parse("2024-05-10T13:54:49");
       System.out.println(ld3);
       System.out.println(ld3.toLocalDate());
       System.out.println(ld3.toLocalTime());
       System.out.println(LocalDateTime.MAX);
       System.out.println(LocalDateTime.MIN);
       
       //convert JDK1.5 date to JDK1.8
       Date d11=new Date(); 
       LocalDateTime ld4=LocalDateTime.ofInstant(d11.toInstant(), ZoneId.systemDefault());
       System.out.println(ld4);
       
       //Convert Calendar to JDK1.8 localdate
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

2. Optional class
     - present in java.util.* package
     - Object will contain memory reference or null reference, so if we access anything using null reference we get NullPointerException
     - To avoid NPE we have to write code to do null check, so to avoid the unpredicatable NPE we can go for Optional class

Methods
1. static Optional empty() - create empty optional
2. static Optional of(T...t) - return an non empty optional, if value is null returns NPE
3. static Optional ofNullable(T...t) - return an non empty optional, if value is null returns empty optional
4. Object get() - return original value from Optional
5. void ifPresent(Consumer) - if value is present it invokes related Consumer
6. boolean isPresent() - return true if value is present otherwise false 
7. boolean isEmpty() - Java11 - check whether optional is empty or not 
8. Object orElse(Object) - return the value if present otherwise return other value
9. Object orElseGet(Supplier) - return the value if present otherwise it invokes another logic 
10. Object orElseThrow(Supplier) - return the value if present otherwise it throws an exception 

public class Main {
    public static void main(String[] args) throws Throwable {
      Optional op1=Optional.empty();
      System.out.println(op1); //Optional.empty
      Optional op2=Optional.of("John");
      System.out.println(op2); //Optional[John]
      //Optional op3=Optional.of(null);
      //System.out.println(op3); //NPE
      Optional op4=Optional.ofNullable("Jack");
      System.out.println(op4); //Optional[Jack]
      Optional op5=Optional.ofNullable(null);
      System.out.println(op5); //Optional.empty
      
      Optional op6=Optional.of("John");
      System.out.println(op6); //Optional[John]
      System.out.println(op6.get()); //John
      op6.ifPresent(System.out::println); //John
      System.out.println(op6.isPresent()); //true
      op6.empty();
      op6.ifPresent(System.out::println);
      System.out.println(op6.isEmpty()); //true
      
      Optional op7=Optional.empty();
      System.out.println(op7.isPresent()); //false
      System.out.println(op7.orElse("Jim")); //Jim
      System.out.println(op7.orElseGet(()->"Jam")); //Jam
      System.out.println(op7.orElseThrow(NullPointerException::new));
      
      
    }
}

3. Default and static method in interface
       - Till JDK1.7, interface will contain only abstract methods and public static final variables
       - From JDK1.8, apart from abstract method interface also contains default and static methods
       - Without affecting the implemented classes, if we want to add any new methods inside the interface then we can go for default methods
       - If my functionality is no way related with object (ie)static method, instead of defining inside the class we can define inside the interface
       - From JDK1.9, the interface also contains private and private static method, if we have common functionalities inside default method and to avoid duplicate code, we can define those common functionality inside private method and access whenever it is needed 

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

Interface Access members
1. Accessible from default and private methods within interface
        constant variable = yes
        abstract method = yes
        another default method = yes
        private method = yes
        static method = yes
        private static method = yes

2. Accessible from static methods within interface
        constant variable = yes
        abstract method = no
        another default method = no
        private method = no
        static method = yes
        private static method = yes

3. Accessible from instance methods by implementing interface
        constant variable = yes
        abstract method = yes
        another default method = yes
        private method = no
        static method = yes
        private static method = no

4. Accessible outside interface without implementing
        constant variable = yes
        abstract method = no
        another default method = no
        private method = no
        static method = yes
        private static method = no

interface MyInterface {
              //Till JDK1.7
              /*public static final*/int CONSTANT =1;
              /*public abstract*/ int abstractMethod();
              
              //From JDK1.8
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
              
              //From JDK1.9
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

var keyword
    - Available from JDK10
    - used to infer the datatype at runtime based on the value
          var a=10;
    - used only inside constructor, methods, loops and compound blocks

Rules
1. var cant declare without initial value
2. var can be declared in first line and initialized in second line
3. var cannot be initialized with null value without a type
4. var is not permitted in multiple variable declaration 
5. var cannot be used initalize an array 
6. var is reserved type name but not reserved keyword, so we can use var as an identifier except for interface,class,enum
7. var in lambda expr, but you cant mix var and non-var parameters 

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
//interface var { } //error
//class var { }//error
//enum var { }//error
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
        
        //var x; //error
        var x=1;
        var y
             =2;
       // var c1=null; //error
        var c1=(String) null;
        var c2="hello";
        c2=null;
        
        int a=10,b=20;
        //var a1=10,b1=20; ///error
        //var a[]= {1,2,3}; //error
        
        MyInterface m1=(var a1,var b1)->System.out.println(a1+b1);  //correct
        //MyInterface m2=(var a1,int b1)->System.out.println(a1+b1);  //error
    }
}

enum 
   - It is type of class that mainly stores constants or fixed set of values 
   - It is implicitly abstract class, by default it is final so we cant inherit but it can be implemented by a interface 

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

Rules
1. enum values are declared first, then only we can define anything

enum Day{
              //int a=10; //error
    SUNDAY,MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY;
              int a=10; //correct
}

2. A non final enum method can be 
enum Day{
              
              SUNDAY{
                             public void print() {
                                           System.out.println("very hot");
                             }
              },
              MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY;
              public void print() {
                             System.out.println("hot");
              }
}

public class Main {
    public static void main(String[] args)  {
       Day d1=Day.TUESDAY;
       d1.print(); //hot
       Day.SUNDAY.print(); //very hot
    }
}

3. If we have abstract method then it should be overridden by all enum value

enum Day{
              
              SUNDAY{
                             public void print() {
                                           System.out.println("very hot");
                             }
              },
              MONDAY{
                             public void print() {
                                           System.out.println("hot");
                             }
              },
              TUESDAY{
                             public void print() {
                                           System.out.println("cold");
                             }
              },
              WEDNESDAY{
                             public void print() {
                                           System.out.println("very cold");
                             }
              },
              THURSDAY{
                             public void print() {
                                           System.out.println("mist");
                             }
              },FRIDAY{
                             public void print() {
                                           System.out.println("very mist");
                             }
              },SATURDAY{
                             public void print() {
                                           System.out.println("average hot");
                             }
              };
              abstract void print();
}

public class Main {
    public static void main(String[] args)  {
       Day d1=Day.TUESDAY;
       d1.print(); //cold
       Day.SUNDAY.print(); //very hot
    }
}

4. Constructor is implicitly private, called only once in the beginning to create enum value 

enum Day{
              
              SUNDAY("very hot"){
                             public void print() {
                                           System.out.println("very hot");
                             }
              },
              MONDAY("hot"){
                             public void print() {
                                           System.out.println("hot");
                             }
              },
              TUESDAY("cold"){
                             public void print() {
                                           System.out.println("cold");
                             }
              },
              WEDNESDAY("very cold"){
                             public void print() {
                                           System.out.println("very cold");
                             }
              },
              THURSDAY("mist"){
                             public void print() {
                                           System.out.println("mist");
                             }
              },FRIDAY("very mist"){
                             public void print() {
                                           System.out.println("very mist");
                             }
              },SATURDAY("average hot"){
                             public void print() {
                                           System.out.println("average hot");
                             }
              };
              String temp;
              /*private*/ Day(String temp){
                this.temp=temp;           
              }
              abstract void print();
}

public class Main {
    public static void main(String[] args)  {
       Day d1=Day.TUESDAY;
       d1.print(); //cold
       Day.SUNDAY.print(); //very hot
       
       for(Day d:Day.values()) {
                 System.out.println(d+" "+d.temp);
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
              Marks(int mark){
                             this.mark=mark;
              }
}
public class Main {
    public static void main(String[] args)  {
      for(Marks m:Marks.values()) {
                System.out.println(m+" "+m.mark);
      }
    }
}

5. enum can also used in switch case

enum Day{
              //int a=10; //error
    SUNDAY,MONDAY,TUESDAY,WEDNESDAY,THURSDAY,FRIDAY,SATURDAY;
              int a=10; //correct
}
public class Main {
    public static void main(String[] args)  {
     Day d1=Day.FRIDAY;
     System.out.println(d1.a); //10
     switch(d1) {
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


