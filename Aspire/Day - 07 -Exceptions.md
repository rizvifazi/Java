

*Date : 04.22.2024*



java.lang.*
1. Object
2. Wrapper class
3. String 
4. StringBuffer
5. StringBuilder

Java (2 concept)
1. Error - generated at compile time - syntacial/human made error 
2. Exception - generated at runtime - logical error - eg: Divide by 0, File not found 

Throwable class 
    - present in java.lang.*, used to handle exceptions in Java

2 types of Exception
1. Checked Exception 
- all subclasses of Exception class excluding RuntimeException
- Eventhough we have written 100% correct prg, ur code has to be surrounded by try/catch block or throws keyword then only the compiler will allow to compile
- It will insist the programmer to surround the code using try/catch block or throws keyword otherwise the program will not compile

1. Unchecked Exception
        - all subclasses of RuntimeException class
        - Eventhough ur prg contains Exception, the compiler will just compile the prg but at runtime we get an exception
        - will not insist the programmer to surround the code using try/catch block or throws keyword, the prg will just compile but at runtime we get an related exception

Constructor
1. Throwable()
2. Throwable(String msg)
3. Throwable(String msg, Throwable t)

Methods
1. String toString()
2. String getMessage()
3. void printStackTrace()

Types of Exception
1. ArthimeticException - divide anything by 0
2. ArrayIndexOutOfBoundsException - only for datatype array
      int a[]=new int[3];
         a[3]=2;

3. StringIndexOutOfBoundsException - only for String array
      String a[]=new String[3];
         a[3]="2";
4. NegativeArraySizeException
      int a[]=new int[-3];
5. NumberFormatException
      int a=Integer.parseInt("abc");
6. ArrayStoreException
   int a[]=new int[3];
    a[0]="one"; 
7. NullPointerException

class Box {
    double volume(){
    }
}
class Main { PSVM {
   Box b=new Box();
   b.volume();
   b=null;
   b.volume();  //NPE
}}

8. ClassCastException
class A{
}
class B extends A{
}

A a=new A();
B b=new B();
a=b;
b=a; //Exception

5 keywords
1. try
      - Program to be monitored for exception has to put inside try block 
2. catch
      - used to catch the exception generated, mainly used to print user defined message when an exception occurs
3. finally
      - optional statement, it will be executed irrespective of exception occurs or not
      - used to close the resources or cleanup the resources
      - used in 3 cases - file, database, socket programming
try {
   fp=fopen("a.txt","r");
   //operation
}
catch(Exception e){
}
finally {
    fclose(fp);
}

3 ways
1. try {                   2. try{                    3. try{
   }                          }                          }
   catch(Exception e){        catch(Exception e){        finally {
   }                          }                          }
   finally {
   }

- We should not write anything between try catch and finally, u will be getting compilation error


To get input from user
1. Using Scanner/BufferedReader class 
2. Directly define in prg itself
3. Using commandline argument
        - we give input while running the program in command line
        - When we use args argument inside the prg, then for that prg we have to give input through commandline
        - Each command line should be separated by space

Right click - Run as - Run as Configuration - Arguments tab - Under Program Arguments we have to give input throught command line separated by space

public class Main {
    public static void main(String[] args) {
        for(int i=0;i<args.length;i++)
              System.out.println(args[i]);
    }
}

public class Main {
    public static void main(String[] args) {
      try {
       int a=Integer.parseInt(args[0]);
       int x=10/a;
       System.out.println(x);
      }
      catch(ArithmeticException e) {
                System.out.println("Divide by 0 "+e);
      }
    }
}

Multi catch statement
    - single try can have multiple catch block 

public class Main {
    public static void main(String[] args) {
      try {
       int a=Integer.parseInt(args[0]);
       int x=10/a;
       System.out.println(x);
       int c[]= {3};
       c[10]=100;
      }
      catch(ArithmeticException e) {
                System.out.println("Divide by 0 "+e);
      }
      catch(ArrayIndexOutOfBoundsException e) {
                System.out.println("Index out of bounds "+e);
      }
    }
}

- Whenever we define general class Exception or Throwable it should be always present in last catch block otherwise it leads to compilation error

public class Main {
    public static void main(String[] args) {
      try {
       int a=Integer.parseInt(args[0]);
       int x=10/a;
       System.out.println(x);
       int c[]= {3};
       c[10]=100;
      }
     /* catch(Exception e /*Throwable t) {
                System.out.println(e);
      }*/  //Compilation error
      catch(ArithmeticException e) {
                System.out.println("Divide by 0 "+e);
      }
      catch(ArrayIndexOutOfBoundsException e) {
                System.out.println("Index out of bounds "+e);
      }
      catch(NullPointerException e) {
                System.out.println(e);
      }
      catch(NumberFormatException e) {
                System.out.println(e);
      }
      catch(Exception e /*Throwable t*/) {
                System.out.println(e);
      }
    }
}

- From JDK1.7 onwards, we define multiple exception in single catch block using | 

public class Main {
    public static void main(String[] args) {
      try {
       int a=Integer.parseInt(args[0]);
       int x=10/a;
       System.out.println(x);
       int c[]= {3};
       c[10]=100;
      }
      catch(ArithmeticException | ArrayIndexOutOfBoundsException 
                               | NumberFormatException | NullPointerException e) {
                System.out.println(e);
      }
      catch(Exception e) {
                System.out.println(e);
      }
    }
}

4. throw keyword
       - used to manually throw an exception
       - whenever it invokes throw keyword it automatically goes to its related catch block 

Syntax: throw new Exception(String msg);

public class Main {
              static void demo() {
                             try {
                                throw new NullPointerException("Hello");
                             }
                             catch(NullPointerException e) {
                                           System.out.println("Caught");
                                           throw e;
                             }
              }
    public static void main(String[] args) {
              try {
          demo();
              }
              catch(NullPointerException e) {
                             System.out.println("Recaught");
              }
    }
}


5. throws keyword
       - used to declare the exception and used only in methods
       - used to indicate that the method might throw some of the exception

public class Main {
              static void demo() throws NullPointerException {
                             try {
                                              throw new NullPointerException("hello");
                                           }
                                           catch(NullPointerException e) {
                                                          System.out.println("Caught");
                                                          throw e;
                                           }
              }
    public static void main(String[] args) {
              try {
          demo();
              }
              catch(NullPointerException e) {
                             System.out.println("Recaught");
              }
    }
}


public class Main {
              static void demoA() {
                             try {
                                           System.out.println("Inside demoA");
                                           throw new RuntimeException();
                             }
                             /*catch(RuntimeException e) {
                             System.out.println("Exception caught");
              }*/
                             finally {
                                           System.out.println("demoA finally");
                             }
              }
              static void demoB() {
                             try {
                                           System.out.println("Inside demoB");
                                           return;
                             }
                             finally {
                                           System.out.println("demoB finally");
                             }
              }
    public static void main(String[] args) {
              try {
                demoA();
              }
              catch(RuntimeException e) {
                             System.out.println("Exception caught");
              }
              demoB();
    }
}


User defined Exception
      - Your userdefined exception class should extends Exception class and override toString()

class A extends Exception{
}

class NotValidException extends Exception {
              String s1="";
              
              public NotValidException(String s1) {
                             this.s1=s1;
              }

              @Override
              public String toString() {
                             return s1;
              }             
}
public class Main {
              static void validateAge() throws NotValidException {
                             Scanner sc=new Scanner(System.in);
                             System.out.println("Enter age");
                             int age=Integer.parseInt(sc.nextLine());
                             if(age<18) {
                                           throw new NotValidException("Your age is not eligible for voting");
                             }
                             else
                                           System.out.println("Your age is eligible for voting");
                                                          
              }
    public static void main(String[] args) {
              try {
                             validateAge();
              }
              catch(NotValidException e) {
                             System.out.println(e);
              }
    }
}

Assertion
    - Available from JDK1.5 onwards
    - used to check boolean condition at runtime

Syntax:  assert <<expression>>;
         assert <<expression>>:String message;
  
   - By default assertion is disabled in Java, while running we have to enable the assertion by using "-ea" option
   - Java provided with assert keyword and AssertionError class which is a unchecked exception because it is inherited from Error class 
   - If the assert condition fails then it will raise AssertionError class 


public class Main {
              static double withdraw(double balance, double amount) {
                             assert balance>amount;  //Java will ignore this line
                             return balance-amount;
              }
    public static void main(String[] args) {
              System.out.println(withdraw(1000,500)); //500.0
              System.out.println(withdraw(1000,2000)); //-1000.0
    }
}

Right click - Run as - Run as Configuration - Arguments tab - Under VM Arguments we have to provide -ea

public class Main {
              static double withdraw(double balance, double amount) {
                             assert balance>amount;  
                             return balance-amount;
              }
    public static void main(String[] args) {
              System.out.println(withdraw(1000,500)); //500.0
              System.out.println(withdraw(1000,2000)); //AssertionError
    }
}

public class Main {
              static double withdraw(double balance, double amount) {
                             assert balance>amount:"Balance is not sufficent";  
                             return balance-amount;
              }
    public static void main(String[] args) {
              System.out.println(withdraw(1000,500)); //500.0
              System.out.println(withdraw(1000,2000)); //-1000.0
    }
}

Try with Resource
     - Available from JDK1.7 onwards
     - Instead of closing the resource inside finally block, if we want to close the resources automatically at the end of stmt using AutoCloseable interface which contains close()

Syntax:
   try(resources) {

   }
   catch(Exception e){
   }

public class Main {
    public static void main(String[] args) {
              String line="";
              try(BufferedReader br=new BufferedReader(new FileReader("Main.java"));
                                           PrintWriter pw=new PrintWriter(new File("a.txt"));) {
                             while((line=br.readLine()) != null) {
                                           System.out.println(line);
                             }
              }
              catch(Exception e) {
                             System.out.println(e);
              }
    }
}

From JDK1.9 onwards, enhancement in try with resources, we can define the resources outside the try block and use it 

public class Main {
    public static void main(String[] args) throws Exception {
              String line="";
              BufferedReader br=new BufferedReader(new FileReader("Main.java"));
                             PrintWriter pw=new PrintWriter(new File("a.txt"));
              try(br;pw) {
                             while((line=br.readLine()) != null) {
                                           System.out.println(line);
                             }
              }
              catch(Exception e) {
                             System.out.println(e);
              }
    }
}

Exception handling in Method overriding
1. If superclass method does not declare any exception, then subclass overridden method cannot declare the checked exception but it can declare unchecked exception

class A {
              void add() {
                             
              }
}
class B extends A {
              void add() throws IOException {   //error
                             
              }
}


class A {
              void add() {
                             
              }
}
class B extends A {
              void add() throws ArithmeticException {  //correct
                             
              }
}

2. If superclass method declares an exception, then subclass overridden method can declare same exception or subclass exception or no exception, but it cant declare parent exception

class A {
              void add() throws Exception{
                             
              }
}
class B extends A {
              void add() throws Exception{  //correct
                             
              }
}


class A {
              void add() throws Exception{
                             
              }
}
class B extends A {
              void add() throws ArithmeticException{ //correct
                             
              }
}


class A {
              void add() throws Exception{
                             
              }
}
class B extends A {
              void add() {  //correct
                             
              }
}

class A {
              void add() throws ArithmeticException{
                             
              }
}
class B extends A {
              void add() throws Exception {  //error
                             
              }
}

