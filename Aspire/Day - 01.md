
*Date : 04.01.2024*

# Java
### Java Versions

#### J2SE - Java 2 Standard Edition - system/networking oriented project
Network based application, communication and chatting
#### J2EE - Java 2 Enterprise Edition - Web oriented Application
#### J2ME - Java 2 Micro Edition - Mobile based Application

##### Misc Facts
Developed by **Sun Microsystem**, taken over by **Oracle** .
Older name of **Java** is **Oak**(1980)
Java Introduction - 1990, Patrick Naughton, Chris Wirth, James Gosling
Latest Version - **21**

Till JDK 1.8 Executable File paid version(usually pirated) - From Java 9 onwards OpenJDK is a opensource project and it is a zip file. Maintained by Oracle

###### Version Naming
JDK1.0 - Oak
JDK2.0 - Playground
JDK3.0 - Kestrel
JDK4.0 - Mustang
JDK5.0 - Tiger
JDK6.0 - Minor Upgrade , no naming
JDK7.0 - Dolphin 
JDK8.0 - Spider

Naming stopped after becoming OpenJDK


# Difference between Java and Other Languages

Only **Scala** is Fully Object Oriented Language

| C                                                                       | Java                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ----------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Procedural Language                                                     | Partially OOPs Language                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Header Files<br>`#include<stdio.h>`<br>`#include<graphic.h>`            | No header files, instead we use packages.<br>Packages - folder which contains collection of class files using `"import"` keyword.<br>eg:<br>`import java.io.*;`- We are selecting all the class files in java.io folder.<br>- Not a good practice to import all classes/ consumes more memory. Can be used when Developing but need to e replaced with the specific class files.<br>`import java.io.File;`<br>`import java.util.Scanner;`<br>       |
| 32 Keywords                                                             | 51 Keywords<br>no - sizeof, extern, register, signed, unsigned                                                                                                                                                                                                                                                                                                                                                                                      |
| Primitive Data Types - int, char...<br>User Defined Data Types - struct | Only Primitive Data Types.<br>Do not support User Defined Data Types                                                                                                                                                                                                                                                                                                                                                                                |
| Global Keyword<br>`#define A 40`<br>(macros)                            | No Global Declaration. but we have to use specific keyword.                                                                                                                                                                                                                                                                                                                                                                                         |
| Pointer Support                                                         | No Pointers<br>This design choice enhances security and stability by preventing common pointer-related errors such as buffer overflows, null pointer dereferencing, and memory corruption.                                                                                                                                                                                                                                                          |
| **Functions** exist independently                                       |  **Methods** exists inside class                                                                                                                                                                                                                                                                                                                                                                                                                    |


# Object Oriented Programming

 1. Object - real world entity or instance of the class, contains memory reference or address.
 2. Class - Template/Blueprint
		 - made up of variables, methods and constructors. 
		 - access the class by creating an object.

3. Encapsulation - Wrapping of data (variables and methods) into a single unit(class)
			  - Data hiding/ Information hiding.
			  - class contains private variables and public methods to achieve encapsulation.

4. Abstraction - Without knowing the background detail of the class, we are using that class.
5. Inheritance - accessing the properties of one class into another class.
			- Code reusability.

6. Polymorphism - one class takes many forms, different implementations.
	1. Static/compile time polymorphism - using overloading
	2. Dynamic/Runtime polymorphism - Using Overriding 

| C++                                                                     | Java                                                                                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Partially OOP                                                           | Partially OOP                                                                                                                                                                                                                                                                                                         |
| Inheritance<br>singles, multiple, multilevel, hybrid, hierarchical      | Do not have **multiple inheritance**, we use **interface** to implement that.                                                                                                                                                                                                                                         |
| Have method overloading, constructor overloading, operator overloading. | Does not have operator overloading.                                                                                                                                                                                                                                                                                   |
|                                                                         | Only Method Overriding                                                                                                                                                                                                                                                                                                |
| - Deallocation of memory.<br>- ~(tilde) operator                        | - There is no destructor, instead.<br>- Automatic garbage collection at the end of the program.<br>- Manual Deallocation `System.gc()/ Runtime.gc()` will internally call finalize(). This is invoked **only once** in the lifecycle of the program. Call be called multiple times, but it will be invoked only once. |
| String is a datatype                                                    | String is a class/literal                                                                                                                                                                                                                                                                                             |
|                                                                         |                                                                                                                                                                                                                                                                                                                       |



| Feature               | C                                                          | C++                                                          | Java                                                                                          |
| --------------------- | ---------------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| Paradigm              | Procedural                                                 | Object-Oriented and Procedural                               | Object-Oriented and Procedural                                                                |
| Syntax Style          | Low-level, complex                                         | Complex, supports object-oriented syntax                     | High-level, easy to read and write                                                            |
| Memory Management     | Manual memory management                                   | Supports both manual and automatic memory management         | Automatic memory management (Garbage Collection)                                              |
| Pointers              | Full support for pointers                                  | Supports pointers                                            | No pointer arithmetic, safer pointer handling                                                 |
| Inheritance           | Not built-in, but can be achieved with structs             | Supports single, multiple, and hierarchical inheritance      | Supports single and hierarchical inheritance through classes                                  |
| Polymorphism          | Achievable through function pointers or struct inheritance | Supports runtime polymorphism using virtual functions        | Achieved through method overloading and inheritance                                           |
| Exception Handling    | Lacks built-in support                                     | Supports exception handling using try-catch blocks           | Exception handling using try-catch-finally blocks                                             |
| Standard Library      | Small and less extensive                                   | Extensive standard library                                   | Comprehensive standard library with robust APIs                                               |
| Platform Independence | Highly platform dependent                                  | Moderately platform dependent                                | Highly platform-independent through the Java Virtual Machine (JVM)                            |
| Compilation           | Compiled directly to machine code                          | Compiled to intermediate code (object files) and then linked | Compiled to bytecode, which is interpreted by JVM or compiled to machine code by JIT compiler |
| Community             | Large community support                                    | Large community support                                      | Huge community support and active development                                                 |


## Constructors

1. What is a constructor?
	- Whenever we create a =n object for a class, memory will be allocated and the allocation of memory is called constructor.
	- Whenever we create an object for a class, the constructor will  be invoked.

2. Why constructor?
	- Used to initialize the value to the variable at time of Object creation.
	- By default all class will contain one default constructor (constructor without parameters) . We can create our own constructor where your class name and constructor name should be same, at that time the already present default constructor will be overlapped.
	- Constructor can be created with or without parameters.
	- Constructor should not have return type.
	- Constructor can have access specifiers.



eg : 

```java
class Box {

	Box(){ //default constructor
	}
	void Box(){ // will not throw any error at all, this will be considered as method
	}
}
```


## Destructors

C/C++
- Deallocation of memory.
- ~(tilde) operator

Java
- There is no destructor, instead.
	- Automatic garbage collection at the end of the program.
	- Manual Deallocation `System.gc()/ Runtime.gc()` will internally call finalize(). This is invoked **only once** in the lifecycle of the program.


## Strings

C++
- String is a datatype

Java
- String is a class/literal



# Fundamentals of Java

## Identifiers
- Names given for class, variables and methods.
- should always start with char, can contain digit in-between, special char( $, _ ) are allowed.
- Always need to follow coding standards.

### Java coding standards

1. class - starting letter of each word should be capital.
		eg: `ExampleProgram, StringExamples`

2. methods - camelCase, from 2nd word onwards each starting letter should be capital.
		e.g.: `getSize(), getAgeOfEmployee()` 

3. variables - all lowercase

4. constants - all UPPERCASE

6. Always create your program inside a package.

7. Should always be formatted - `Ctrl+A -> Ctrl+shift+F`


## Keywords
- 51 keywords - no - sizeof, extern, register, signed, unsigned.
- `goto` and `const` are keywords of Java but if we use we get a compilation error.
	- Instead use `goto -> continue` and `const -> final`

- 3 reserved words
	- `true / false` - Boolean
	- `null` - object

## Data type
 - what type of value we are stored in a variable - only primitive


| datatype   | byte                        | min                   | max                     |
| ---------- | --------------------------- | --------------------- | ----------------------- |
| 1. byte    | 1                           | -2^7 = **(-128)**     | (2^7) - 1 = **127**     |
| 2. short   | 2                           | -2^15 = **(-32,768)** | (2^15) - 1 = **32,767** |
| 3. int     | 4                           | -2^31                 | (2^31) -1               |
| 4. long    | 8                           | -2^63                 | (2^63) - 1              |
| 5. float   | 4                           | ~exp                  | ~exp                    |
| 6. double  | 8                           | ~exp                  | ~exp                    |
| 7. char    | 2 (16 bit unsigned integer) | 0                     | 65535                   |
| 8. boolean | 1                           | false                 | true                    |


## Literal
- How we can define the value to a variable.

1. Numeric literal - 3 ways to represent `int` values in Java.
	1. **Decimal literal** - base 10
			`int a = 31;`
			`int b = 56788
	2. **Octal literal** - base 8 - always preceded with 0.
			`int a = 01; //1`
			`int b = 02; //2`
			... 03, 04, 05, 06, 07
			`int c = 010; //8`
				0*\8^0 = 0
				1\*8^1 = 8
				0\*8^2 = 0
			`int d = 011; //9`
				1*\8^0 = 1
				1\*8^1 = 8
				0\*8^2 = 0
			`int e = 012; //10`
	3. **Hexadecimal literal** - base 16 - always preceded with `0x` or `0X`
			`int a = 0x23; //35`
				3\*16^0 = 3
				2\*16^1 = 32

2. Short literal
	`short s1 = 10; //correct`
	`short s2 = 10s //error`
	`short s3 = 10S //error`

3. Long literal
	`long l1 = 10 //correct 
	`long l2 = 10l //correct`
	`long l3 = 10L //correct`
	by default in Java, all (+ve) and (-ve) numbers considered as int datatype, so the first statement is accepted as int is 4 bytes and long is 8 bytes.

4. Float literal
	`float f1 = 3.15 //error`
	`float f2 = 3.15f //correct`
	`float f3 = 3.15F //correct`

5. Double literal
	`double d1 = 3.14; //correct`
	`double d2 = 3.14d; //correct`
	`double d3 = 3.14D //correct`
	by default in Java, all (+ve) and (-ve) decimal values are considered as double datatype, so the first statement is accepted as float is 4 bytes and double is 8 bytes. That why `float f1 = 3.15 //error`

6. Boolean literal
	`boolean b1=true;  //correct
	`boolean b2=false; //correct
	`boolean b3=True;  //error
	`true` and `fasle` all should be in simple letter. No CAPs allowed.


7. char literal - always single char in 'single quote'
	`char c1='a';  //correct
	`char c2="a";  //error
	`char c3='ab'; //error
	`char c4="ab"; //error
	`char c5=25;  //correct (print ascii value of 25)
	`char c6=-26; //error
	`char c7=10000;  //correct 
	`char c8=(char)70000;  //correct 70000 ascii value is out of range so correct it by typecasting as char
	In Java, char can also be represented as unicode format and recognized at time of compilation itself
	    `char c='\u0000';

8. String literal - sequence of char with double quotes
	`String s1="hello";  //literal

9. null literal
	`String s1=null;
	`Box b1=null;
	Only objects can have `null` value, `String is an Object`

  
## Variables
- identifier used to store a value - 2 types

1. Instance/class variable 
	Any variable that is declared inside the class and outside the method
	```java
	class Box {
	    int a;   //instance variable 
	    void show() {
	    }
	} 	```
	- No need to initialize the instance variable, it will be taking the default value depending on the datatype.
	  
	`int,byte,short,long - 0`
	`float,double - 0.0`
	`boolean - false`
	`char - \u0000`
	`any object - null`

  
2. Local variable
	- Any variable that are declared inside the method and *compulsorily it should be initialized* otherwise compilation error
	```java
	class Box {
		    int a;   //instance variable 
		    void show() {
		       int b=0;  //local variable
		    }
		} 
	```


## Access specifiers/Access Modifiers - 4 types

1. `public` - it can be accessed anywhere
2. `private` - it can be accessed only within the class in which it is declared
3. `protected` - it can be accessed within the class as well in its inherited class
4. `default`
	- If we not specify public, private, protected, then by default it is considered as default access specifier, so it is default access specifier in Java.
	- We can't specify anything as default, compiler will consider as default.




| Visibility                     | default | private | protected | public |
| ------------------------------ | ------- | ------- | --------- | ------ |
| 1. Same pkg, Same class        | yes     | yes     | yes       | yes    |
| 2. Same pkg, Diff class        | yes     | no      | no        | yes    |
| 3. Diff Package, sub Class     | no      | no      | yes       | yes    |
| 4. Diff package, non sub class | no      | no      | no        | yes    |

## Type conversion

- converting from one datatype to another datatype

1. Implicit conversion - automatic conversion from lower to higher datatype
       `int a=3;
       `double s=a;  //implicit

2. Explicit conversion - converting from higher to lower datatype
	`int i=128;     -128 to 127
	`byte b=(byte)i;
	`System.out.println(b);  //-128
	It print -128 as after 127 it will again start from -128, this is go in loops infinite amount of time.


  ## Operators
1. Arithmetic operator `+,-,*,/`
2. Modulus operator `%`
3. Relational operator `>,<,> =,< =`
4. Assignment operator `=`
5. Conditional Assignment operator `+=,-=,*=,/=`
	`a+=2;  a=a+2;` both of these statements imply the same meaning
6. Equality and Inequality operator `==,! =`
7. Ternary operator `?:`
      `z=a>b?a:b;`
      `if(a>b){z=a;}else{z=b;}`
8. Increment and Decrement operator `++,--`
	Have 2 types post increment and pre increment.
9. Bitwise operator - *always works on truth table*
       `& - Bitwise AND
       `| - Bitwise OR
       `^ - Bitwise XOR
       `~ - 1's complement
       `>> - Right shift - n/2^s
       `<< - Left shift - n*2^s

		a=5, b=6

| a   | b   | a&b=4 | a\|b=7 | a^b=3 | ~a  |
| --- | --- | ----- | ------ | ----- | --- |
| 0   | 0   | 0     | 0      | 0     | 1   |
| 1   | 1   | 1     | 1      | 0     | 0   |
| 0   | 1   | 0     | 1      | 1     | 1   |
| 1   | 0   | 0     | 1      | 1     | 0   |

**Important**
`a=8(n), b=2(s)` according to `n/2^s`
	`a>>b=8/2^2=8/4=2` Right shift operator
	`a<<b=8*2^2= 32` Left shift operator

  
10. Boolean logical operator
      `& - Logical AND`
      `| - Logical OR`
      `! - Logical NOT` 
 - If the operands are numbers these operators work as bitwise operators, but if the operands are Boolean this works as Boolean logical operator. 
	 - `a=true, b=false, a&b=false`


11. Short-circuit logical operator  - used to check the condition, with if statement.
	`&&    ||
	`if((a==10)||(b>20)){   \\statement; }`


12. `new` operator - used to create an object for class - *3 ways*  
	```java
	class Box {
	    int a=10;
	    void show() {
	    }
	    Box(String s){}
	}
	```
	
	1. `Box b = new Box();`//This will not compile if a parameterized constructor is created. This is the most preferred way of creating an object	we are creating an object called "b", and we are allocating the memory using new operator and that memory stored inside the object and invokes your default constructor.
	
	   `Box b1=new Box("hello");


	2. 
		```java
		Box b;     //object declaration which contains null reference
		b=new Box();  //creating object, allocate memory, invoke default constructor
		b.show();
		System.out.println(b.a);
		b.show();
		```
		we create object to access the methods and variables


	3. 
		```java
		new Box();  //invokes constructor
		new Box().show(); //invokes constructor, calls show but not stored anywhere
		new Box().show(); //good if only calling once to invoke cost
		
		```

13. `instanceof` operator
     - used to check whether an object is an instance of that class
     ```java
     Box b=new Box();
     if(b instanceof Box) {
     //logic
     }
      ```
  
  
# 4 J's in Java

**JDK - Java Development Kit**
- JRE + extra tools that are needed to develop a java program such as `javac`(Java compiler), java(Java Interpreter)

**JVM - Java Virtual Machine**
- It is like motor of car - It is a software that reads the byte code and execute the bytecode
    JVM will be different for each OS 

**JIT - Just In time Compiler**
- JVM contains JIT, which translates the byte code to native machine code for the CPU where the program is running

**JRE - Java Runtime Environment**
- JRE is JVM and supporting libraries that are required to execute the Java program





