

*Date : 04.05.2024*

# Execution Control Statement in Java - 3 types

## Conditional statement - 2 types

a.  `if/if-else/if-then-else/nested if` - check for boolean condition

In C and C++, **other than 0** if we provide any `+ve or -ve` value it will return true, otherwise false. _But in case of Java it is error_

```java
	int a = 0;
	if(a){  //error - compilation error
	}
	else {
	}
	
	int a = 11;
	if(a = 10){  //error - compilation error
	}
	
	if(a == 10){  //correct , checks for equality and returns bool
	}
	
	if(a > 10){  //correct
	}
	
	boolean b = true;
	if(b){  //correct
	}
	
	if(b = true){  //correct
	}
	
	//above is not the same as below, above is an assignation, below is checking for
	//condition
	
	if(b == true){  //correct
	}

```

Always check for condition, not assignation or initialization 
And we don't have `= = =` operator in Java, like in JavaScript where we used to check type equality.



b . `switch case` - check multiple condition

Syntax: 
```java
     switch(expr)  {
        case arg:
           //stmt
           break;
        --
        --
        --
        default:
           //stmt
           break;
     }

```



1. `expr` can be either` int/byte/char/short/enum/String`(JDK1.7)+
2. `arg` should be always **final** (i.e. :it will act like constant)

```java
int a=1;
switch(a)
   case 1:
      SOP("1");
      break;
   case 1:  //error because arg is final
```

3. `default` stmt can be present anywhere inside switch case
4. If we want to come out from switch case we have to use `break` stmt, *don't ever use "continue"* inside switch case which leads to [compilation error]       

```java
public class Test {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

		if (10 == 10) {
			System.out.println("Hello");
		}
		if (true)
			System.out.println("true");

		int a = 12;
		if (a > 12)
			System.out.println("yes");
		else
			System.out.println("No");

		// if(1) ///error
		// System.out.println("helolo");

		switch (5) {
		case 1:
			System.out.println("1");
			break;
		case 5:
			System.out.println("5");
			break;
		}

		/*
		 * switch(5) { case 5: System.out.println("1"); break; case 5: //error
		 * System.out.println("5"); break; }
		 */

		switch (5) {
		case 1:
			System.out.println("1");
			break;
		default:
			System.out.println("any");
			break;
		case 5:
			System.out.println("5");
			break;
		}

		switch (50) {
		case 1:
			System.out.println("1");
			break;
		default:
			System.out.println("any");
			break;
		case 5:
			System.out.println("5");
			break;
		}

		switch (1) { // 1 any 5
		case 1:
			System.out.println("1");

		default:
			System.out.println("any");

		case 5:
			System.out.println("5");

		}

		switch (1) { // 1 any
		case 1:
			System.out.println("1");
			// break;
		default:
			System.out.println("any");
			break;
		case 5:
			System.out.println("5");
			break;
		}

		char c = 'a';
		switch (c) { // nothing will be printed
		case 'b':
			System.out.println("B");
			break;
		case 'c':
			System.out.println("C");
			break;
		}

		switch ("c") { // JDK1.7+
		case "b":
			System.out.println("B");
			break;
		case "c":
			System.out.println("C");
			break;
		}

	}

}

```


## Looping statement - 3 types

a. `for` loop - used for iteration
   
Syntax: 
	`for(initialization;condition;inc/dec operator){ }
`
```java
for(;;){   //infinite for loop
}
```

b. `do while`

syntax: 
```java
do {
    //stmt
}
while(condition); //in C/C++ can pass numbers, but here only numbers
```

c. `while`
Syntax: 
`while(condition)`

### Flow breaking statement

a. `break` - used to stop entire iteration
b. `continue` - used to stop current iteration
c. `return` - transfer the control back to calling program

```java
public class Main {
	public static void main(String[] args) {
		for (int i = 0; i < 10; i++) {
			if (i % 2 == 0) // Checking for Even
				// break;
				continue;
			System.out.print(i + " "); // 1 3 5 7 9 - Printing odd
		}
	}
}
```



# Array 
   - collection of similar datatypes

1. `int a[]={1,2,3};`  //correct - declaring and initializing values to an array, and its size is fixed depending upon the no of elements, so size=3.
2. `int a[3]={1,2,3};`  //*error* - if we want to provide the size of an array then **compulsory** we have to use `new` operator 
3. `int a[]=new int[3];` //correct - declare an array of size 3, memory allocated is 4\*3=12 bytes.
4. `int[] a=new int[3];`  //correct
5. `int a[]=new int[]{1,2,3};` //correct - Anonymous array - where we can declare and initialize an array in same line 
6. `int a[]=new int[3]{1,2,3}; *`//*error* - In Anonymous array, we *should not specify* its size 
7. `int a[]=new int[-3];` //correct - In Java we can declare an array with negative size but at *runtime* we get [NegativeArraySizeException]
8. `int a[]=new int[3]; ` //correct - declare an array of size 3
    `a[0]=1;  a[1]=2;  a[2]=3;` //initialize the array 
9. `int a[]={1,2,3};`
   `sop(a);`  //memory reference

10. We want to access individual element of array - 2 ways
	`arrayname.length` - used to find length of the array
	
	a. Normal for loop
	
	```java
	public static void main(String[] args) {
		int a[] = { 1, 2, 3 };
		int i; // can declare outside of loop, but in C++ only inside for loop
		for (i = 0; i < a.length; i++)
			System.out.println(a[i]); // 1 2 3

		double d[] = { 1.2, 3.4, 5.6 };
		for (int j = 0; j < d.length; j++)
			System.out.println(d[j]); // 1.2 3.4 5.6
	}
	
```

		`i` - loop-counter variable 


	b. `for each statement` - available only from JDK1.5 onwards, used to access individual element of array 
	
	Syntax:
	```java
	for(loopcountervariable : array) {
	             //logic
	    }
	```

a. loop-counter variable should be *declared only inside the foreach statement*, and it should of *same datatype as array* 

b.1D array has to put inside a variable, 2D array has to put inside 1D, 3D array has to put inside 2D etc.

```java
	public static void main(String[] args) {

		int a[] = { 1, 2, 3 };
		for (int i : a)
			System.out.println(i);

		double d[] = { 1.2, 3.4, 5.6 };
		for (double d1 : d)
			System.out.println(d1);

	}
```

## 2D Array

1. `int a[][]={{1,2},{3,4}};` //correct - declaring and initializing an array of size 16 bytes(2\*2\*4)
2. `int a[2][2]={{1,2},{3,4}};`  //*error* -*compulsory* to use `new` operator if giving size
3. `int a[][]=new int[3][3];` //correct - 36bytes
4. `int[][] a=new int[3][3];` //correct
5. `int[] a[]=new int[3][3];` //correct
6. `int a[][]=new int[5][5];` //correct - 100bytes
7. `int a[][]=new int[5][5]; `//correct - 100 bytes, only 8 bytes are used remaining 92 bytes are wasted 
    `a[0][0]=1;`
    `a[1][0]=2;`
8. `int a[][]=new int[5][]; `//correct - *Arrays of Array* - we have to declare only rows, based on requirement we have to allocate our columns
	  `a[0]=new int[1];   a[0][0]=1;` //initialized only one column
	  `a[1]=new int[2];` //initialized only 2 columns
	  `a[1][0]=2; a[1][1]=3;` //only allocate 12 bytes
   
9. `int a[][]=new int[][5];` //*error* - in arrays of array we have to give only rows, not columns

```java
public class Main {

	public static void main(String[] args) {
		float f1[][] = { { 1.2f, 3.4f }, { 5.6f, 7.8f } };
		System.out.println(f1); // memory reference will be printed

		for (int i = 0; i < 2; i++)
			for (int j = 0; j < 2; j++)
				System.out.println(f1[i][j]); // 1.2 3.4 5.6 7.8

		// @foreach loop of a 2D array
		for (float f2[] : f1) // 2D array should be stored in a 1D array
			for (float f3 : f2) // 1D array should be stored in a variable
				System.out.println(f3); // print the variable - 1.2 3.4 5.6 7.8
	}
}
```


## 2 types of classes
1. Main class
     - entry point of program, there will always only one main class.
     - If it contain `public static void main(String[] args)`
     - used to create an object for base class and finally print the output.
     - Main class should not contain any logic

2. Base class
     - we have to write all your logic inside base class, there will be multiple base classes.

#shortcuts
sysout - press `ctrl+spacebar -> Enter` 
type main - press `ctrl+spacebar -> Enter`



# class and object 


Base class
```java
class Box {
	// instance variable
	double width;
	double height;
	double depth;
}

public class Main {
	public static void main(String[] args) {
		Box b1 = new Box(); // creating an object called b1 which contain memory reference and invoking
							// default constructor
		b1.width = 10;
		b1.height = 20;
		b1.depth = 30;

		Box b2 = new Box();
		b2.width = 1;
		b2.height = 2;
		b2.depth = 3;

		double vol; // local variable
		vol = b1.width * b1.height * b1.depth;
		System.out.println("Volume is " + vol); // Volume is 6000.0
		vol = b2.width * b2.height * b2.depth;
		System.out.println("Volume is " + vol); // Volume is 6.0
	}
}
```


**Method** - used to write any logic
In the above code snippet we have written the logic inside Main() method which is not a good practice, instead we must use a method to calculate volume.

Syntax: 
```java 
returntype methodname(arguments) {
    //logic
}
```

Base class with volume method
```java
class Box {
	// instance variable
	double width;
	double height;
	double depth;

	
	//logic for volume
	void volume() { 
		System.out.println(width * height * depth);
	}
}

public class Main {
	public static void main(String[] args) {
		Box b1 = new Box(); // creating an object called b1 which contain memory reference and invoking
							// default constructor
		b1.width = 10;
		b1.height = 20;
		b1.depth = 30;

		Box b2 = new Box();
		b2.width = 1;
		b2.height = 2;
		b2.depth = 3;

		b1.volume(); // 6000.0
		b2.volume(); // 6.0
	}
}
```
In the above code snippet we are printing the output in the Base class, which is not a good practice instead we should return the value from the method and print output in the Main class.

Base class
```java
class Box {
	// instance variable
	double width;
	double height;
	double depth;
	
	//returning from method instead printing here
	double volume() { 
		return (width * height * depth);
	}
}

public class Main {
	public static void main(String[] args) {
		Box b1 = new Box(); // creating an object called b1 which contain memory reference and invoking
							// default constructor
		b1.width = 10;
		b1.height = 20;
		b1.depth = 30;

		Box b2 = new Box();
		b2.width = 1;
		b2.height = 2;
		b2.depth = 3;

		double vol; // local variable
		vol = b1.volume();
		System.out.println("Volume is " + vol); // Volume is 6000.0
		vol = b2.volume();
		System.out.println("Volume is " + vol); // Volume is 6.0
	}
}
```
In the above code snipped we have initialized in the main class, it is a good practice to use a parameterized method to set the dimensions of the Box.

Parameterized method - method that can take parameters

Base class
```java
class Box {
	// instance variable
	double width;
	double height;
	double depth;

	double volume() {
		return (width * height * depth);
	}

	void setDim(double w, double h, double d) { // parameterized method
		width = w;
		height = h;
		depth = d;
	}
}

public class Main {
	public static void main(String[] args) {
		Box b1 = new Box(); // creating an object called b1 which contain memory reference and invoking
							// default constructor
		b1.setDim(10, 20, 30); // initialized using the parameterized method

		Box b2 = new Box();
		b2.setDim(1, 2, 3);

		double vol; // local variable
		vol = b1.volume();
		System.out.println("Volume is " + vol); // Volume is 6000.0
		vol = b2.volume();
		System.out.println("Volume is " + vol); // Volume is 6.0
	}
}

```


## 2 types of methods

1. **Mutator method** - setter method - used to set the value - `setName(), setAge(), setSize()`
2. **Accessor method** - getter method - used to get the value - `getName(), getAge(), getSize()`


## Constructor

- What is constructor?
	-  whenever we create an object for a class, memory will be allocated and the allocation of memory is called constructor
- When constructor invokes?
	- whenever we create an object for a class, the constructor will be invoked
- Why constructor?
    - used to initialize the value to the variable at time of object creation
    - By default all class will contain one default constructor (ie) constructor without any parameter, and we can create our own constructor where your class name and constructor name should be same, at that time the already present default constructor will be overlapped
    - Constructor can be created with or without parameters
    - Constructor should not have return type
    - Constructor can have access specifiers


Using a constructor to initialize the values of Box.
```java
//Base class
class Box {
	// instance variable
	double width;
	double height;
	double depth;

	double volume() {
		return (width * height * depth);
	}

	Box() { // default constructor
		width = -1;
		height = -1;
		depth = -1;
	}

}

//Main class
public class Main {
	public static void main(String[] args) {
		Box b1 = new Box(); // creating an object called b1 which contain memory reference and invoking
							// default constructor

		Box b2 = new Box();

		double vol; // local variable
		vol = b1.volume();
		System.out.println("Volume is " + vol); // Volume is -1.0
		vol = b2.volume();
		System.out.println("Volume is " + vol); // Volume is -1.0
	}
}
```


Parameterized constructor - constructor that takes parameters
```java
//Base class
class Box {
	// instance variable
	double width;
	double height;
	double depth;

	double volume() {
		return (width * height * depth);
	}

	Box(double w, double h, double d) { // parameterized constructor
		width = w;
		height = h;
		depth = d;
	}

}

public class Main {
	public static void main(String[] args) {
		Box b1 = new Box(10, 20, 30); // creating an object called b1 which contain memory reference and invoking
										// default constructor

		Box b2 = new Box(1, 2, 3);

		double vol; // local variable
		vol = b1.volume();
		System.out.println("Volume is " + vol); // Volume is 6000.0
		vol = b2.volume();
		System.out.println("Volume is " + vol); // Volume is 6.0
	}
}
```

### `this` keyword
- used to refer *current class* variable
- It is used if your parameter name and instance variable name are same, in order to avoid the confusion we use "this" keyword.

```java
class Box {
	// instance variable
	double width;
	double height;
	double depth;

	double volume() {
		return (width * height * depth);
	}

	Box(double width, double height, double depth) { // parameterized constructor
		this.width = width;
		this.height = height;
		this.depth = depth;
	}
}
```

Instead if we use without `this` keyword it will compile and give wrong output. IDE will show warning message.

```java
Box(double width, double height, double depth) { // parameterized constructor
		width = width;
		height = height;
		depth = depth;
	}
```
All the values will be initialized to 0 which is the default value.



### `this()` constructor 
- used to invoke different constructor of the same class, it should be *always present only in the first line* otherwise it leads to compilation error 


Without `this()` constructor
```java
class A {
	A() {
		System.out.println("1");
	}

	A(int a) {
		System.out.println("2");
	}

	A(String s) {
		System.out.println("3");
	}
}

public class Main {
	public static void main(String[] args) {
		A a1 = new A(); // 1
		A a2 = new A(10); // 2
		A a3 = new A("hello"); // 3
	}
}
```


Using `this()` constructor, it works like recurrent methods, one constructor calls the other constructor. First it executes the innermost methos and then outer and ... 
But it will *throw a compilation error* when we try to call the same constructor. We can't call recursively.
```java
class A {
	A() {
		this("hello");
		System.out.println("1");
	}

	A(int a) {
		System.out.println("2");
	}

	A(String s) {
		this(5);
		System.out.println("3");
	}
}

public class Main {
	public static void main(String[] args) {
		A a1 = new A(); // 2 3 1
		A a2 = new A(10); // 2
		A a3 = new A("hello"); //2 3
	}
}
```

Example2:
```java
class A {
	A() {
		this(10);
		System.out.println("1");
	}

	A(int a) {
		System.out.println("2");
	}

	A(String s) {
		this();
		System.out.println("3");
	}
}

public class Main {
	public static void main(String[] args) {
		A a1 = new A(); // 2 1
		A a2 = new A(10); // 2
		A a3 = new A("hello"); // 2 1 3
	}
}
```


Example3:
```java
class A {
	A() {
		this("he");
		System.out.println("1");
	}

	A(int a) {
		this();
		System.out.println("2");
	}

	A(String s) {
		System.out.println("3");
	}
}

public class Main {
	public static void main(String[] args) {
		A a1 = new A(); // 3 1
		A a2 = new A(10); // 3 1 2
		A a3 = new A("hello"); // 3
	}
}
```

