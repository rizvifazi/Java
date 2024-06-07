
# Lambda Expressions
- Introduced in Java 8
- Anonymous Functions, without name and does not belong to any class.
- Mainly used to implement [[Functional Interfaces]].

## Lambda vs Method
- In Java Method always belongs to a class or object.
- But Lambda does not belong to any class or object


e.g.:
```java
	public int addition(int a, int b){
		return a+b;
	}
```

#### Properties of Lambda
- **No Name - Anonymous**
- **No Return type** - Java 8+ compiler infer the return type by checking the code.
- **Parameter list**
- **Body**

e.g. :
```java
Addable withLambdaD = (a,b) -> (a+b);
```


##### Lambda Expression Syntax
```
( lambda input parameters )   ->lambda sign    { lambda body }
```

### Example Program 1 
```java
package com.pack;

interface Shape {
	abstract void draw();
}

class Rectangle implements Shape { //this can be removed due to lambda implementation.

	@Override
	public void draw() {
		System.out.println("Rectangle class :: Draw method");
	}
}

class Square implements Shape { //this can be removed due to lambda implementation.

	@Override
	public void draw() {
		System.out.println("Square class :: Draw method");
	}
}

class Circle implements Shape { //this can be removed due to lambda implementation.

	@Override
	public void draw() {
		System.out.println("Circle class :: Draw method");
	}
}

public class Lambda {

	public static void main(String[] args) {
		Shape rectangle = () -> System.out.println("Rectangle class :: Draw method");
		rectangle.draw(); // must call the assigned method;

		Shape square = () -> System.out.println("Square class :: Draw method");
		square.draw(); // must call the assigned method;

		Shape circle = () -> System.out.println("Circle class :: Draw method");
		circle.draw(); // must call the assigned method;
	}

}

```

Output
```cmd
Rectangle class :: Draw method
Square class :: Draw method
Circle class :: Draw method
```


### Example Program 2 -> Passing Lambda to method

```java
public class Lambda {

	public static void main(String[] args) {
		Shape rectangle = () -> System.out.println("Rectangle class :: Draw method");
		//rectangle.draw(); // must call the assigned method;
		print(rectangle);

		Shape square = () -> System.out.println("Square class :: Draw method");
		//square.draw(); // must call the assigned method;
		print(square);

		Shape circle = () -> System.out.println("Circle class :: Draw method");
		//circle.draw(); 
		print(circle);
	}
	
	private static void print(Shape shape) {
		shape.draw();
	}

}
```

Output
```cmd
Rectangle class :: Draw method
Square class :: Draw method
Circle class :: Draw method
```


Instead of assigning the lambda to a reference object, we can pass the the lambda expression straight to the method call.

```java
public class Lambda {

	public static void main(String[] args) {

		print(() -> System.out.println("Rectangle class :: Draw method"));
		print(() -> System.out.println("Square class :: Draw method"));
		print(() -> System.out.println("Circle class :: Draw method"));
	}
	
	private static void print(Shape shape) {
		shape.draw();
	}

}
```

Output
```cmd
Rectangle class :: Draw method
Square class :: Draw method
Circle class :: Draw method
```

> Passing Lambda expression as a behavior to the method. Meaning **Functional Programming** 


