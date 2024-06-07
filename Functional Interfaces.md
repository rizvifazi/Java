- Introduces in Java8
- Interface that contains exactly **one** Abstract method is a Functional Interface.
- FI  can contain any number of default, static methods but can contain **only one abstract method**.

```java
interface MyFunctionalInterface{
	
	public void execute(); //only abstract method, implemented in child classes
		
	public default void print(String text){   //default method
		System.out.println(text);
	}
		
	public static void print(){ // Static method
		writer.write(text);
	} 

}
```

