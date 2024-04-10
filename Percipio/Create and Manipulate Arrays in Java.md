
1. Create a project `ADJ-001` and use the `JavaSE1.8`  Runtime
2. Create package `com.adj`
3. Create classes MyArray and MyArrayTest with main() method.
- MyArray.java

```java
package com.adj;

public class MyArray{

	private String messages[];
	//Always create private variables unless theres a specific need to do otherwise, Good OOP practice

	//Constaructor will have the same name as the class with no return type. Constructors will always be public 
	public MyArray(){
		messages = new String[5]; //initialize to a size of 5
		messages[0] = "Hi";
		messages[1] = "Hello";
		messages[2] = "Welcome";
		messages[3] = "Howdy";
		messages[4] = "Aloha";
	}

	punlic void printArray(){
		//foreach loop, use as frequent as possible
		for(String m:messsages){
			System.out.println(m);
		}
	}

}

```

- MyArrayTest
```java
package com.adj;

public class MyArrayTest{

	public static void main(String[] args){

		MyArray myArray = new MyArray();
		myArray.printArray();
	}
}
```
