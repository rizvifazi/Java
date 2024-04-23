

*Date : 04.15.2024*


java.lang.*
  
1. Object class
  
Methods
1. String toString() - String representation of an  object 
2. boolean equals(Object o) - check the equality of content
3. == (equals versus) - check the equality of object reference
4. int hashCode()
5. protected void finalize()
6. final void wait()
7. final void wait(long msec)
8. final void notify()
9. final void notifyAll()
10. Object clone()
  
  
2 parts
1. Stack - store the local variable and object , LIFO, store data in different sequence
2. Heap - open space, store instance variable and its reference
  
Calculator obj=new Calculator();
(stack)          (heap)
obj=null;
  
Garbage collection
    - Removing unused variables from memory so that there is sufficient space for the new variable. To avoid OutOfMemoryError or memory leak
    - Java by itself does cleaning job in the background by running daemon thread
  
  
finalize() in Java is used to perform cleanup activity before destroying an object. It is called by Garbage collector before destroying an object. It is called by feault for every object before its deletion and only once in the lifecycle of the program
  
Unreferencing of objects - 3 ways
1. By anonmyous object
        - Anonmyous object are those object which are created without reference variable
     new Calculator();
  
2. By nulling reference
  
Calculator c=new Calculator();
c=null;
  
3. By assigning reference to another object 
  
Calculator c1=new Calculator();
Calculator c2=new Calculator();
c1=c2;
  
Explicitly call the Garbage collector
1. System.gc() - invoked garbage collector which will destroy the unreferenced objects, it will call finalize() only once for each object 
2. Runtime.gc()
  
1. finalize() method of which class is called
  
public class Main {
              public static void main(String[] args) {
       String s1="hello";
       s1=null;
       System.gc();
       System.out.println("Garbage collector is called");
              }
              protected void finalize() {
                             System.out.println("finalize method called");
              }
}
  
Output:
Garbage collector is called
  
public class Main {
              public static void main(String[] args) {
       Main m1=new Main();
       m1=null;
       System.gc();
       System.out.println("Garbage collector is called");
              }
              protected void finalize() {
                             System.out.println("finalize method called");
              }
}
  
Output:
finalize method called
Garbage collector is called
  
Explicit call finalize()
    - When we call finalize() explicitly, JVM will treat as normal method and it will not remove object from memory. finalize() can release memory only when it is called garbage collector
  
public class Main {
              public static void main(String[] args) {
       Main m1=new Main();
       Main m2=new Main();
       m1=m2;
       m1.finalize(); 
       System.out.println("Garbage collector is called");
       System.gc();
              }
              protected void finalize() {
                             System.out.println("finalize method called");
              }
}
  
Exceptions in finalize()
  
public class Main {
              public static void main(String[] args) {
       Main m1=new Main();
       m1=null;
       System.gc();
       System.out.println("Garbage collector is called");      
              }
              protected void finalize() {
                             System.out.println("finalize method called");
                             int a=10/0;
                             System.out.println("Exception");
              }
}
  
public class Main {
              public static void main(String[] args) {
       Main m1=new Main();
       m1=null;
       System.gc();
       System.out.println("Garbage collector is called"); 
       System.gc();
       System.out.println("Garbage collector is called by us");
              }
              protected void finalize() {
                             System.out.println("finalize method called");
              }
}
  
  
Object clone()
     - copy of an object 
  
public class Student{
   int rollNo;
}
  
public class Main {
              public static void main(String[] args) {
       Student s1=new Student();
       s1.rollNo=1;
       Student s2=s1;
       s2.rollNo=2;
       System.out.println(s1.rollNo);   //2
       System.out.println(s2.rollNo);   //2
              }
}
  
1. Class has to implement Cloneable interface(Marker interface - empty intf)
  
The main use of the Marker Interface in Java is to convey to the JVM that the class implementing some interface of this category has to be granted some special behavior.
  
2. override clone() of Object class to take copy of object, without implementing Cloneable intf, if we try to take copy of an object using clone() then we get CloneNotSupportedException
  
Shallow copy
    - Eventhough we copied reference, both object should be independent (ie) if we change one object it will not be reflected on other object 
    - clone() by default support shallow copy
  
public class Student implements Cloneable{
   int rollNo;
   protected Object clone() throws CloneNotSupportedException {
                 return super.clone();  //shallow copy
   }
}
  
public class Main {
              public static void main(String[] args) throws CloneNotSupportedException {
       Student s1=new Student();
       s1.rollNo=1;
       Student s2=(Student)s1.clone();
       s2.rollNo=2;
       System.out.println(s1.rollNo);   //1
       System.out.println(s2.rollNo);   //2
     }
}
  
- In case of object type variable
  
public class Address {
    String address;
}
  
public class Student implements Cloneable{
   int rollNo;
   Address address;
   protected Object clone() throws CloneNotSupportedException {
                 return super.clone();  //shallow copy
   }
}
  
public class Main {
              public static void main(String[] args) throws CloneNotSupportedException {
       Student s1=new Student();
       s1.rollNo=1;
       Address addr1=new Address();
       addr1.address="Chennai";
       s1.address=addr1;
       Student s2=(Student)s1.clone();
       s2.rollNo=2;
       System.out.println(s1.rollNo);   //1
       System.out.println(s2.rollNo);   //2
       System.out.println(s1.address.address);  //Chennai
       System.out.println(s2.address.address);  //Chennai
              }
}
  
public class Main {
              public static void main(String[] args) throws CloneNotSupportedException {
       Student s1=new Student();
       s1.rollNo=1;
       Address addr1=new Address();
       addr1.address="Chennai";
       s1.address=addr1;
       Student s2=(Student)s1.clone();
       s2.rollNo=2;
       s2.address.address="Bangalore";
       System.out.println(s1.rollNo);   //1
       System.out.println(s2.rollNo);   //2
       System.out.println(s1.address.address);  //Bangalore
       System.out.println(s2.address.address);  //Bangalore
              }
}
  
If we have object type variabler in that case it will copy the reference, it wont copy the entire object, to deal with this if we have object type variable we use deep copy
  
Deep copy
    - In case of deep copy, for primitive type and object type it will copy entire object so that both object will exist independently
    1. First we have to take shallow copy of Student class
    2. Next shallow copy of Address class
  
  
public class Student implements Cloneable{
   int rollNo;
   Address address;
   protected Object clone() throws CloneNotSupportedException {
                 Student student=(Student)super.clone();  //shallow copy of Student 
                 student.address=(Address)address.clone();
                 return student;
   }
}
  
public class Address implements Cloneable {
    String address;
    protected Object clone() throws CloneNotSupportedException {
              return super.clone();
    }
}
  
  
public class Main {
              public static void main(String[] args) throws CloneNotSupportedException {
       Student s1=new Student();
       s1.rollNo=1;
       Address addr1=new Address();
       addr1.address="Chennai";
       s1.address=addr1;
       Student s2=(Student)s1.clone();
       s2.rollNo=2;
       s2.address.address="Bangalore";
       System.out.println(s1.rollNo);   //1
       System.out.println(s2.rollNo);   //2
       System.out.println(s1.address.address);  //Chennai
       System.out.println(s2.address.address);  //Bangalore
              }
}
  
Shallow copy
1. For object type variable, it copies only the reference of the object
2. It is not 100% independent of original object
3. Default implementation of clone() return shallow copy
  
Deep copy
1. For object type variable, it copies entire object
2. It is 100% independent of original object
3. We need to additionaly call clone() of the object type variable to achive deep copy
  
class A {
  int i;
  int j;
}
  
A obj=new A();
obj.i=5;
obj.j=6;
  
A obj1=obj;
  
  
2. Wrapper class
       - class support the primitive datatype, to perform any operation on datatype
       - All wrapper class are immutable class(u cant change)
       - Character, Boolean extends Object class
       - Integer, Byte, Long, Short, Float, Double extends Number abstract class
  
datatype    Class
int    -    Integer
byte   -    Byte
short  -    Short
long   -    Long
float  -    Float
double -    Double
char   -    Character
boolean -   Boolean
  
  
1. Float class
       - used to perform any operation on float datatype
  
Constructor
  1. Float(float f)
       Float f1=new Float(3.14f);
  2. Float(double d)
       Float f1=new Float(3.14);
  3. Float(String s) throws NumberFormatException
       Float f1=new Float("3.14");
       Float f1=new Float("ab");  //NumberFormatException
  
int a=10, b=10;
if(a==b)
  
float f1=3.14f, f2=3.14f;
if(f1==f2)  //error
  
Methods
1. static int compare(float f1,float f2) - compare two float datatype, if equal returns 0, if greater 1, if lesser -1
2. int compareTo(Float f1) - compare two Float object, if equal returns 0, if greater 1, if lesser -1
3. static boolean isInfinite() - check float datatype is infinite or not
4. boolean isInfinite() - check Float object is infinite or not
5. static boolean isFinite() - check float datatype is finite or not
6. boolean isFinite() - check Float object is finite or not
7. static boolean isNaN() - check float datatype is NAN(Not a Number) or not
8. boolean isNaN() - check Float object is Nan or not
9. static float parseFloat(String s) throws NumberFormatException - convert String to float datatype
10. static Float valueOf(String s) - convert String to Float wrapper class
11. float floatValue() - convert Float wrapper class to float datatype
12. int intValue()
13. double doubleValue()
14. short shortValue()
15. long longValue()
16. byte byteValue()
  
Constants
1. Float.MAX_VALUE
2. Float.MIN_VALUE
3. Float.POSITIVE_INFINITY
4. Float.NEGATIVE_INFINITY
5. Float.TYPE
  
public class Main {
              public static void main(String[] args)  {
      float f1=3.14f;
      float f2=3.14f;
      System.out.println(Float.compare(f1, f2));  //0
      Float f3=new Float(3.14f);
      Float f4=new Float(3.14f);
      System.out.println(f3.compareTo(f4));   //0
      float f5=(float)(1/0.);
      System.out.println(Float.isInfinite(f5));  //true
      Float f6=new Float(1/0.);
      System.out.println(f6.isInfinite());  //true
      float f7=(float)Math.sqrt(-4);
      System.out.println(Float.isNaN(f7));  //true
      Float f8=new Float(Math.sqrt(-4));
      System.out.println(f8.isNaN());  //true
      String s1="3.14";
      float f9=Float.parseFloat(s1);
      System.out.println(f9);  //3.14
      Float f10=Float.valueOf(s1);
      System.out.println(f10);  //3.14
      float f11=f10.floatValue();
      System.out.println(f11);  //3.14
      int i=f10.intValue();
      System.out.println(i); //3
      System.out.println(Float.MAX_VALUE);
      System.out.println(Float.MIN_VALUE);
      System.out.println(Float.POSITIVE_INFINITY);
      System.out.println(Float.NEGATIVE_INFINITY);
      System.out.println(Float.TYPE);
              }
}
  
2. Double class
      - used to perform operation on double datatype
  
Constructor
   1. Double(double d)
   2. Double(String s) throws NumberFormatException
