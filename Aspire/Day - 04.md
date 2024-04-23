

*Date : 04.12.2024*


Method overriding
     - same method name, same number, order and datatype of argument, same return type of method and present in different class and the class should be inherited
  
class A {
              int i;
              int j;
              A(int a,int b){
                             i=a;
                             j=b;
              }
              void show() {
                             System.out.println("i = "+i+" j = "+j);
              }
}
class B extends A {
              int k;
              B(int a,int b,int c) {
                             super(a,b);
                             k=c;
              }
              void show() {
                             //super.show();
                             System.out.println("k = "+k);
              }
}
public class Main {
              public static void main(String...args) {
                             B b=new B(1,2,3);
                             b.show();
              }
}
  
  
Dynamic Method Dispatch
     - In order to have effective method overriding, then we have to use Dynamic Method Dispatch
     - We always create an object for base class but we have to store the reference of derived class but not vice versa, so the compiler thinks that the object is created for base class, but only at runtime it comes to know it contains the reference of derived class, in this way we achieve runtime polymorphism  
  
class Sphere {
              void volume() {
                             System.out.println("Sphere volume");
              }
}
class Hemisphere extends Sphere {
              void volume() {
                             System.out.println("Hemisphere volume");
              }
}
public class Main {
              public static void main(String[] args) {
                             /*Hemisphere h=new Hemisphere();
                             h.volume(); //Hemisphere volume
                             Sphere s=new Sphere();
                             s.volume(); */ //Sphere volume;
                             Sphere s=new Hemisphere();  //DMD
                             s.volume();   //Hemisphere volume
                             s=new Sphere();  //intially s contains of Hemisphere class, hemisphere reference will be garbage collected and s contains Sphere reference
                             s.volume();  //Sphere volume
              }
}
  
class A  {
              void callback() {
                             System.out.println("Inside A's callback");
              }
}
class B extends A  {
              void callback() {
                             System.out.println("Inside B's callback");
              }
}
class C extends A  {
              void callback() {
                             System.out.println("Inside C's callback");
              }
}
public class Main {
              public static void main(String[] args) {
         A a=new A();
         a.callback();
         a=new B();
         a.callback();
         a=new C();
         a.callback();
              }
}
  
No Constructor overriding
  
How constructors are invoked in inheritance?
     - Invoked as top down approach 
  
//Multi level inheritance
class A  {
              A() {
                             System.out.println("1");
              }
}
class B extends A  {
              B() {
                             System.out.println("2");
              }
}
class C extends B  {
              C() {
                             System.out.println("3");
              }
}
public class Main {
              public static void main(String[] args) {
        C c=new C();  //123
              }
}
  
//Multi level inheritance
class A  {
              A(int a) {
                             System.out.println("1");
              }
}
class B extends A  {
              B() {
                             System.out.println("2");
              }
}
class C extends B  {
              C() {
                             System.out.println("3");
              }
}
public class Main {
              public static void main(String[] args) {
        C c=new C();  //Compilation error
              }
}
  
First it will go to the related constructor (ie) into C class constructor and check whether we have used super() or this(), if we used then it will work according to that. But if we not used then by default it will try to invoke only default constructor of the base class 
  
  
//Multi level inheritance
class A  {
              A(int a) {
                             System.out.println("1");
              }
       /* A() {
        }*/
}
class B extends A  {
              B() {
                super(2);
                             System.out.println("2");
              }
}
class C extends B  {
              C() {
                             System.out.println("3");
              }
}
public class Main {
              public static void main(String[] args) {
        C c=new C();  //123
              }
}
  
  
//Multi level inheritance
class A  {
              A(int a) {
                             System.out.println("1");
              }
       /* A() {
        }*/
}
class B extends A  {
              B() {
                super(2);
                             System.out.println("2");
              }
}
class C extends B  {
              C(String s) {
                             System.out.println("3");
              }
}
public class Main {
              public static void main(String[] args) {
        C c=new C("hi");  //123
              }
}
  
final keyword
    - It is a non access specifier
    - When a class is declared as final, then it cannot be inherited 
  
final class A  {
              A() {
                             System.out.println("1");
              }
}
class B extends A  {  //error
              B() {
                             System.out.println("2");
              }
}
  
    - When a method is declared as final, then method overriding is not possible
  
class A  {
              final void show() {
                             System.out.println("1");
              }
}
class B extends A  {  
              void show() {   //error
                             System.out.println("2");
              }
}
  
    - When a variable is declared as final, it will acts like constant
  
Relationship - 2 types
1. is-a relationship - when we perform inheritance
  
class Animal {
}
class Dog extends Animal{
}
  
Dog is a Animal
  
2. has-a relationship - Composition - one class contains another class
  
class Tyre{
}
class Car{
    Tyre t=new Tyre();
}
  
Car has a Tyre
  
Covariant return type
      - Available from JDK1.5 onwards
      - Before JDK1.5, it is not possible to override any method by changing its return type
      - It is possible to override method by changing its return type (ie) only non primitive (ie) object 
      - Avoid type casting, wrong casting leads to ClassCastException at runtime
  
class A  {
              A show() {
                             return this;
              }
              void print() {
                             System.out.println("Inside A's method");
              }
}
class B extends A  {  
              B show() {
                             return this;
              }
              void print() {
                             System.out.println("Inside B's method");
              }
}
class C extends B {
              C show() {
                             return this;
              }
              void print() {
                             System.out.println("Inside C's method");
              }
}
public class Main {
              public static void main(String[] args) {
       A a1=new A();
       a1.print();
       B b1=new B();
       b1.show().print();
              }
}
  
Compound block/Instance block
    - It will be invoked before the constructor invokes
  
Syntax:  {
            //logic
         }
  
Only in case of inheritance, first it will invoke all static block from top to bottom if it is present
  
18 21 19 1 6 11 15 17 5 7 2 4 3 8 10 9 14 16 12 13 20
  
  
//Multilevel
class A {
              static {   //static block
                             System.out.println("1");
              }
              A() {
                             System.out.println("2");
              }
              A(String s) {
                             this(10);
                             System.out.println("3");
              }
              A(int a){
                             this();
                             System.out.println("4");
              }
              {  //Compound block
                             System.out.println("5");
              }
              static {
                             System.out.println("6");
              }
              {
                             System.out.println("7");
              }
}
class B extends A {
              {
                             System.out.println("8");
              }
              B() {
                             super("hello");
                             System.out.println("9");
              }
              {
                             System.out.println("10");
              }
              static {
                             System.out.println("11");
              }
}
class C extends B {
              C() {
                             System.out.println("12");
              }
              C(int a) {
                             this();
                             System.out.println("13");
              }
              {
                             System.out.println("14");
              }
              static {
                             System.out.println("15");
              }
              {
                             System.out.println("16");
              }
              static {
                             System.out.println("17");
              }
}
public class Main {
              static {
                             System.out.println("18");
              }
              public static void main(String[] args) {
       System.out.println("19");
       C c=new C(5);
       System.out.println("20");
              }
              static {
                             System.out.println("21");
              }
}
  
abstract keyword
     - It is a non access specifier
     - When a class is declared as abstract, we cannot create an object for that class 
     - When a method is declared as abstract, it does not contain any defination it just ends with ;
     - Variables cant be declared as abstract
     - When a class contain abstract method then that particular class should be declared as abstract, but not necessarily all abstract class should contain abstract method
     - Abstract class can also contain non-abstract method(normal method)
     - Abstract class can also be inherited, so when u inherit an abstract class then complusorly we have to provide the defination of abstract method in the inherited class or we have to define the inherited class itself to be abstract 
     - Abstract class contains constructor but we cant invoke it 
  
abstract class A {
              abstract void show();
              void concreteMethod() {
                             System.out.println("Concrete method");
              }
}
/*abstract*/ class B extends A {
              void show() {
       System.out.println("Abstract method");
              }
}
public class Main {
              public static void main(String[] args) {
        B b=new B();
        b.show();
        b.concreteMethod();
              }
}
  
Anonmyous Inner class
    - used to access concrete method of abstract class without inheritence     
  
abstract class A {
              abstract void show();
              void concreteMethod() {
                             System.out.println("Concrete method");
              }
}
  
public class Main {
              public static void main(String[] args) {
         A a=new A() {  //Anonmyous Inner class
              public void show() {
                             System.out.println("Abstract method");
              }
              public void concreteMethod() {
                             System.out.println("Concrete method1");
              }
         };
         a.show();
         a.concreteMethod();
              }
}
  
Interface
      - No multiple inheritance instead we use Interface
    class A extends B,C,D {  //ERROR
    }
      - Interface are syntacially similar to classes but contains only method declaration and variable declaration and initialization
  
Syntax:  <<accessspecifier>> interface interfacename {
             //method declaration and variable declaration and initialization
          }
  
      - By default all interface are abstract, so we cant create object for an interface
      - By default all interface methods are public and abstract, so interface method dosent contain any defination it just ends with semicolon
      - By default all interface variable are public, static, final, so we can access interface variable using "interfacename.variablename"
      - Using "implements" keyword we can use interface in class
      - If a class implements an interface then compulsorly we have to provide the defination of method declared in the interface with public access specifier or define the implemented  class itself abstract
      - The implemented class can also have non interface method
      - Interface can also be inherited
1 class extends 1 class
1 class implements n interface
1 interface extends n interface
      - Marker interface - interface which dosent contain anything like Cloneable, Serializable, Remote 
      - From JDK1.8 onwards, interface will contain default method and static methods also
      - From JDK1.9 onwards, interface will contain private and private static methods also 
  
interface Maths {
              void calculation(int a,int b);
              int c=20;
}
/*abstract*/ class A implements Maths {
              @Override
              public void calculation(int a, int b) {
                             System.out.println(a+b);
                             System.out.println(Maths.c);
              }    
}
class B implements Maths {
              @Override
              public void calculation(int a, int b) {
                             System.out.println(a-b);
              }             
}
public class Main {
              public static void main(String[] args) {
        /*A a=new A();
        a.calculation(5, 3);  //8
        B b=new B();
        b.calculation(8, 3);*/  //5
                             Maths m=new A();  //DMD
                             m.calculation(5, 3);  //8
                             m=new B();
                             m.calculation(5, 3);  //2
              }
}
  
interface A {
              void method1();
}
interface B{
              void method2();
}
interface C extends A,B {
              void method3();
}
class D implements C {
  
              @Override
              public void method1() {
                             System.out.println("Method1");
              }
  
              @Override
              public void method2() {
                             System.out.println("Method2");
              }
  
              @Override
              public void method3() {
                             System.out.println("Method3");
              }
}
public class Main {
              public static void main(String[] args) {
       D d=new D();
       d.method1();
       d.method2();
       d.method3();
              }
}
  
Predefined Packages
1. java.lang.* - Language package - only one optional package
  
1. Object class
      - super class of all classes (ie) all predefined and userdefined class by default will inherit Object class 
  
void add(int c) - int as arg
void add(String s) - String as arg
void add(Box b) - object of Box class as arg
void add(Sample s) - object of Sample class as arg
void add(Object o) - object of any class as arg
  
Constructor 
1. Object()
  
Methods
1. String toString() - String representation of an  object 
  
String s1=new String("hello");  //all predefined classes by default contains toString(), so if we print object any predefined class automatically it will invoke toString() and it print some content
Sop(s1);   //hello
  
Sample s2=new Sample("hello"); //user defined class 
sop(s2);  //object reference 
  
Whenever we print object of any class, it will print only memory reference, but we dont want to print reference instead we want to print some content then in that case we have to override toString()
  
class A {
              String s1;
              A(String s1) {
                             this.s1=s1;
              }
  
              @Override
              public String toString() {
                             return s1;
              }             
}
public class Main {
              public static void main(String[] args) {
       String s1=new String("hello");
       System.out.println(s1);  //hello
       A a1=new A("hello");
       //System.out.println(a1); //reference
       System.out.println(a1); //hello
       System.out.println(a1.toString()); //hello
              }
}
  
2. boolean equals(Object o) - check the equality of content
3. == (equals versus) - check the equality of object reference
  
If we are not new operator, then == also works like equals()
  
public class Main {
              public static void main(String[] args) {
       String s1=new String("hello");   //class
       String s2=new String("hello");   //class
       System.out.println(s1.equals(s2));   //true
       System.out.println(s1==s2);  //false
       String s3=s2;
       System.out.println(s2==s3); //true
       System.out.println(s2.equals(s3)); //true
       String s4="Hello";  //literal
       String s5="Hello";  //literal
       System.out.println(s4.equals(s5));  //true
       System.out.println(s4==s5);  //true
              }
}
  
4. int hashCode()
       - When we store some value into object, internally an address will be generated for that value, to return that address we use hashCode()
       - If two objects are equal according to equals() then hashcode will return same
  
public class Main {
              public static void main(String[] args) {
       String s1=new String("hello");  
       String s2=new String("hello1");   
       System.out.println(s1.hashCode());
       System.out.println(s2.hashCode());
              }
}
  
5. protected void finalize()
6. final void wait()
7. final void wait(long msec)
8. final void notify()
9. final void notifyAll()
10. Object clone()
