

*Date : 04.08.2024*

## Scanner class
- present in java.util.* .  (java.util.Scanner) package.
- used to get input from user based on primitive datatype.
- If we provide the input in *all String* or in *all number* there is *no issues*. But if we provide combination of String and numbers, then we have to provide a *dummy line called `nextLine()`* or try to get *all input as String* and based on requirement u can convert to related datatype. (This is most preferred).

### Methods
1. `int nextInt()`
2. `short nextShort()`
3. `float nextFloat()`
4. `double nextDouble()`
5. `long nextLong()`
6. `boolean nextBoolean()`
7. `String nextLine()` - //multiple word with space
8. `String next()` - only one word 




Polymorphism - one class takes many forms - 2 types

1. Static/compile time polymorphism
2. Dynamic/runtime polymorphism

Static/Compile time polymorphism
     - Using overloading
     - 2 types - Method and Constructor overloading

Method Overloading
     - same method name, but different number, order and datatype of the argument, different return type but present in same class 

class OverloadDemo {
              //Method overloading
              void test() {
                             System.out.println("No parameter");
              }
              /*void test(int a) {
                             System.out.println("a = "+a);
              }*/
              void test(int a, int b) {
                             System.out.println("a = "+a+" b = "+b);
              }
              double test(double a) {
                             System.out.println("a = "+a);
                             return a*a;
              }
}

public class Main {
              public static void main(String[] args) {
                             OverloadDemo ob=new OverloadDemo();
                             ob.test();
                             ob.test(10); //Implicit conversion
                             ob.test(10,20);
                             double res=ob.test(123.4);
                             System.out.println(res);
              }
}

Constructor overloading
      - same constructor name, but different number, order and datatype of the argument, but present in same class 

//Base class
class Box {
              //Instance variable
    double width;
    double height;
    double depth;
    
    double volume() {
              return (width*height*depth);
    }
    //Constructor overloading
    Box() {
              width=-1;
              height=-1;
              depth=-1;
    }
    Box(double width,double height,double depth){
              this.width=width;
              this.height=height;
              this.depth=depth;
    }
    Box(double len){
              width=height=depth=len;
    }
}
public class Main {
              public static void main(String[] args) {
                             Box b1=new Box();
                             Box b2=new Box(10,20,30);
                             Box b3=new Box(7);
                             double vol;
                             vol = b1.volume();
                             System.out.println("Volume is "+vol);  //Volume is -1.0
                             vol = b2.volume();
                             System.out.println("Volume is "+vol);  //Volume is 6000.0
                             vol = b3.volume();
                             System.out.println("Volume is "+vol);  //Volume is 343.0
              }
}

Passing an object as an argument

void show(int a){}
void show(Test t){}
void show(Sample s){}

//Base class
class Box {
              //Instance variable
    double width;
    double height;
    double depth;
    
    double volume() {
              return (width*height*depth);
    }
    //Constructor overloading
    Box() {
              width=-1;
              height=-1;
              depth=-1;
    }
    Box(double width,double height,double depth){
              this.width=width;
              this.height=height;
              this.depth=depth;
    }
    Box(double len){
              width=height=depth=len;
    }
    Box(Box b){
              width=b.width;
              height=b.height;
              depth=b.depth;
    }
}
public class Main {
              public static void main(String[] args) {
                             Box b1=new Box();
                             Box b2=new Box(10,20,30);
                             Box b3=new Box(7);
                             Box b4=new Box(b2);
                             double vol;
                             vol = b1.volume();
                             System.out.println("Volume is "+vol);  //Volume is -1.0
                             vol = b2.volume();
                             System.out.println("Volume is "+vol);  //Volume is 6000.0
                             vol = b3.volume();
                             System.out.println("Volume is "+vol);  //Volume is 343.0
                             vol = b4.volume();
                             System.out.println("Volume is "+vol);  //Volume is 6000.0
              }
}

class Sample {
    void add(int a,int b) {  //Parameter
        sop(a+b);
    }
    void add(int a, int b, int c){
       SOP(a+b+c);
    }
    void add(int a, int b, int c,int d, int e){
       SOP(a+b+c+d+e);
    }
    
}

Sample s=new Sample();
s.add(10,20); //argument

Var args 
    - used to define variable number of arguments (ie) 0 to any number 
    - Available from JDK1.5 onwards
    - denoted by ...
    - If we pass combination of arg with var arg, then var args should be always present as last argument
    - One method can have only one var args and that should be present as last argument

void show(int...a) { //0 or any number of int arg
}
void show(float...f,String s){ //error
}
void show(int a,boolean...b,double...d){ //error
}

class Demo {
              void add(int...a) {
                             for(int a1:a)
                                           System.out.println(a1);
              }
              void add(boolean...b) {
                             for(boolean b1:b)
                                           System.out.println(b1);
              }
              void add(String s,float...f) {
                             System.out.println(s);
                             for(float f1:f)
                                           System.out.println(f1);
              }
}
public class Main {
              public static void main(String...args) {
                             Demo d=new Demo();
                             //d.add();
                             d.add(1,2,3,4,5,6,7,8);
                             d.add(1,2);
                             d.add(true,true,false,false);
                             d.add("hello",1.2f,3.4f,5.6f);
              }
}

Access specifiers - public, private, protected, default - can be applied for all (ie) class, interface, variable, method, constructor

Non access specifiers - it has its own limitation (ie) cannot be applied for everything

static keyword
    - It is a non access specifier
    - Whenever a class is declared as static, there is no need to create an object for that class, outer class cannot be declared as static, only inner classes can be static 

class A {  //outer class
  class B  { //inner class
  }
}
    - Whenever a method is declared as static, if it is present in same class then we can access using "methodname", if it is present in different class then we can access using "classname.methodname"
     - Whenever a variable is declared as static it will act as global variable, if it is present in same class then we can access using "variablename", if it is present in different class then we can access using "classname.variablename"
     - any static method can access only static content, if it is not static we have to access by creating an object

class Main {
    int a;
    public static void main(String[] args) {
         System.out.println(a);  //error
    }
}

class Main {
    static int a;
    boolean b;
    public static void main(String[] args) {
         System.out.println(a);  //0
         Main m=new Main();
         System.out.println(m.b); //false
    }
}

    - when we want to execute any task before main(), then we can go for static block which will be executed before main()

Syntax:  static  {
            //logic
         }
    - static method can override only static method 

public class Main {
              static int a=4;
              static int b;
              static void method(int x) {
                             System.out.println(x);
                             System.out.println(a);
                             System.out.println(b);
              }
              static {
                             System.out.println("Static block initialized");
                             b=a*2;
              }
              public static void main(String...args) {
                             method(10);
              }
}

class Base {
              static {
                             System.out.println("static block 2");
              }
              static int a=10;
              static int b=20;
              static void demo() {
                             System.out.println(a);
              }
}
public class Main {
              static {
                             System.out.println("static block 1");
              }
              public static void main(String...args) {
                             Base.demo();
                             System.out.println(Base.b);
              }
}


System.out.println()/System.in

System is a predefined class in java.lang.* package

out is an object of PrintStream class and it is a static variable in System class

println() is a instance method of PrintStream class  

public class System {
   static PrintStream out;
   static InputStream in;
}

static import
    - Available from JDK1.5 onwards, only for static methods and variables
    - Normally we can invoke static methods and static variables using "classname.methodname" and "classname.variablename", but if we want to invoke static methods and static variables without using "classname.methodname" and "classname.variablename" then we can use static import


public class Main {
              public static void main(String...args) {
                             double d=Math.sqrt(16);
                             System.out.println(d);
              }
}

import static java.lang.System.out;
import static java.lang.Math.sqrt;

public class Main {
              public static void main(String...args) {
                             double d=sqrt(16);
                             out.println(d);
              }
}


Nested class and Inner class
    - A class present inside another class

//Nested class
class A {
   class B {
   }
}

- Inside class can be either static or non static 

class A {
   class B {  //Inner class - non static inner class
   }
}

class A {
   static class B { //static class 
   }
}

- Outer class properties can be accessed inside the inner class only if it is an instance variable or declared with final, otherwise it is an error
- we cant access Inner class properties in outer class


class Outer {
              int outer=100;  //instance variable 
              void test() {
                             Inner in=new Inner();
                             in.show();
              }
              class Inner {
                             int x=10;
                             void show() {
                                           System.out.println(x+" "+outer);
                             }
              }
}

public class Main {
              public static void main(String...args) {
                             Outer o=new Outer();
                             o.test();
              }
}


class Outer {
              int outer=100;  //instance variable 
              class Inner {
                             int x=10;
                             void show() {
                                           System.out.println(x+" "+outer);
                             }
              }
}

public class Main {
              public static void main(String...args) {
                             Outer.Inner o=new Outer().new Inner();
                             o.show();
              }
}


class Outer {
              static int outer=100;  //instance variable 
              static class Inner {
                             int x=10;
                             void show() {
                                           System.out.println(x+" "+outer);
                             }
              }
}

public class Main {
              public static void main(String...args) {
                             Outer.Inner o=new Outer.Inner();
                             o.show();
              }
}

Inheritance
     - accessing the properties of one class into another class
     - code reusability
     - using "extends" keyword
     - single, multilevel, hybrid, hierachial
     - No multiple inheritence

class Parent{  //parent/base/super class
}
class Child extends Parent { //child/derived/subclass
}

//Single Inheritance
//Base class
class Box {
              double width;
              double height;
              double depth;
              
              double volume() {
                             return (width*height*depth);
              }
              
              Box() {
                             width=-1;
                             height=-1;
                             depth=-1;
              }
              Box(double width,double height,double depth){
                             this.width=width;
                             this.height=height;
                             this.depth=depth;
              }
              Box(double len){
                             width=height=depth=len;
              }
              Box(Box ob){
                             width=ob.width;
                             height=ob.height;
                             depth=ob.depth;
              }
}
//Derived class
class BoxWeight extends Box {
              double weight;
              
               BoxWeight() {
                             width=-1;
                             height=-1;
                             depth=-1;
                             weight=-1;
              }
              BoxWeight(double w, double h, double d, double we) {
                             width=w;
                             height=h;
                             depth=d;
                             weight=we;
              }
              BoxWeight(double len,double w){
                             width=height=depth=len;
                             weight=w;
              }
              BoxWeight(BoxWeight ob){
                             width=ob.width;
                             height=ob.height;
                             depth=ob.depth;
                             weight=ob.weight;
              }
}
public class Main {
              public static void main(String...args) {
                             BoxWeight b1=new BoxWeight();
                             double vol;
                             vol=b1.volume();
                             System.out.println("Volume is "+vol); //Volume is -1.0
                             System.out.println("Weigth is "+b1.weight); //Weight is -1.0
                             BoxWeight b2=new BoxWeight(10,20,30,40);
                             vol=b2.volume();
                             System.out.println("Volume is "+vol); //Volume is 6000.0
                             System.out.println("Weigth is "+b2.weight); //Weight is 40.0
                             BoxWeight b3=new BoxWeight(10,20);
                             vol=b3.volume();
                             System.out.println("Volume is "+vol); //Volume is 1000.0
                             System.out.println("Weigth is "+b3.weight); //Weight is 20.0
                             BoxWeight b4=new BoxWeight(b2);
                             vol=b4.volume();
                             System.out.println("Volume is "+vol); //Volume is 6000.0
                             System.out.println("Weigth is "+b4.weight); //Weight is 40.0
              }
}

super keyword
     - used to access base class constructor, base class method and base class variables
     - Only in the case of accessing base class constructor, super keyword should be present in first line
     - super() and this() cannot be used simulanteously


//Single inheritance
//Base class
class Box {
              private double width;
              private double height;
              private double depth;
              
              double volume() {
                             return (width*height*depth);
              }
              
              Box() {
                             width=-1;
                             height=-1;
                             depth=-1;
              }
              Box(double width,double height,double depth){
                             this.width=width;
                             this.height=height;
                             this.depth=depth;
              }
              Box(double len){
                             width=height=depth=len;
              }
              Box(Box ob){
                             width=ob.width;
                             height=ob.height;
                             depth=ob.depth;
              }
}
//Derived class
class BoxWeight extends Box {
              double weight;
              
               BoxWeight() {
                             super();
                             weight=-1;
              }
              BoxWeight(double w, double h, double d, double we) {
                             super(w,h,d);
                             weight=we;
              }
              BoxWeight(double len,double w){
                             super(len);
                             weight=w;
              }
              BoxWeight(BoxWeight ob){
                             super(ob);
                             weight=ob.weight;
              }
}
public class Main {
              public static void main(String...args) {
                             BoxWeight b1=new BoxWeight();
                             double vol;
                             vol=b1.volume();
                             System.out.println("Volume is "+vol); //Volume is -1.0
                             System.out.println("Weigth is "+b1.weight); //Weight is -1.0
                             BoxWeight b2=new BoxWeight(10,20,30,40);
                             vol=b2.volume();
                             System.out.println("Volume is "+vol); //Volume is 6000.0
                             System.out.println("Weigth is "+b2.weight); //Weight is 40.0
                             BoxWeight b3=new BoxWeight(10,20);
                             vol=b3.volume();
                             System.out.println("Volume is "+vol); //Volume is 1000.0
                             System.out.println("Weigth is "+b3.weight); //Weight is 20.0
                             BoxWeight b4=new BoxWeight(b2);
                             vol=b4.volume();
                             System.out.println("Volume is "+vol); //Volume is 6000.0
                             System.out.println("Weigth is "+b4.weight); //Weight is 40.0
              }
}


//Multilevel inheritance
//Base class
class Box {
              private double width;
              private double height;
              private double depth;
              
              double volume() {
                             return (width*height*depth);
              }
              
              Box() {
                             width=-1;
                             height=-1;
                             depth=-1;
              }
              Box(double width,double height,double depth){
                             this.width=width;
                             this.height=height;
                             this.depth=depth;
              }
              Box(double len){
                             width=height=depth=len;
              }
              Box(Box ob){
                             width=ob.width;
                             height=ob.height;
                             depth=ob.depth;
              }
}
//Derived class
class BoxWeight extends Box {
              double weight;
              
               BoxWeight() {
                             super();
                             weight=-1;
              }
              BoxWeight(double w, double h, double d, double we) {
                             super(w,h,d);
                             weight=we;
              }
              BoxWeight(double len,double w){
                             super(len);
                             weight=w;
              }
              BoxWeight(BoxWeight ob){
                             super(ob);
                             weight=ob.weight;
              }
}
class Shipment extends BoxWeight {
              double cost;
              
              Shipment(double w,double h,double d,double we,double c){
                             super(w,h,d,we);
                             cost=c;
              }
}
public class Main {
              public static void main(String...args) {
                             Shipment s1=new Shipment(10,20,30,40,50);
                             double vol;
                             vol = s1.volume();
                             System.out.println("Volume is "+vol); //Volume is 6000.0
                             System.out.println("Weight is "+s1.weight); //Weight is 40.0
                             System.out.println("Cost is "+s1.cost); //Cost is 50.0
              }
}


class A {
              int i;
}
class B extends A {
              int i;
              
              B(int a,int b){
                             i=a;
                             super.i=b;
              }
              
              void display() {
                             System.out.println(i+" "+super.i);
              }
              
}
public class Main {
              public static void main(String...args) {
                             B b=new B(1,2);
                             b.display();
              }
}


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
                             super.show();
                             System.out.println("k = "+k);
              }
}
public class Main {
              public static void main(String...args) {
                             B b=new B(1,2,3);
                             b.show();
              }
}
