
## **Question**

### 01. **What benefit does value checking in setter methods provide in Java Encapsulation?**

**Instruction:** Choose the option that best answers the question.

- It automatically throws an exception when an error occurs
- It is more memory efficient
- It allows the caller to set the data without instantiating an object
- It ensures the validity of data

**Answer:**

- It ensures the validity of data.

**Explanation:**

Value checking in setter methods ensures that only valid data is assigned to the object's fields, maintaining the integrity and consistency of the object's state.

---

### **Question**

02. ### **Select the method used to convert a string to a primitive int type**

**Instruction:** Choose the option that best answers the question.

- String.toInt
- Double.parseDouble
- Integer.parseInt
- Integer.fromString

**Answer:**

- Integer.parseInt

**Explanation:**

This method is used to convert a `String` to a primitive `int` type in Java.

---

### **Question**

03. ### **What happens if someone attempts to change the value of a constant after it has already been assigned a value?**

**Instruction:** Choose the option that best answers the question.

- An exception is thrown when the program is run
- The code will be ignored
- The compiler will give an error
- An object will be created with the new value

**Answer:**

- The compiler will give an error

**Explanation:**

In Java, if you attempt to change the value of a constant (typically defined using the `final` keyword), the compiler will produce an error because `final` variables cannot be reassigned after they have been initialized.

---

### **Question**

### 04. **Select the benefits of access control.**

**Instruction:** Choose all options that best answer the question.

- Determine how internal data gets changed
- Keep the implementation separate from the public interface
- Implement static methods
- Determine how memory is stored
- Hide fields and methods from other classes

**Answers:**

- Determine how internal data gets changed
- Keep the implementation separate from the public interface
- Hide fields and methods from other classes

**Explanation:**

These options reflect the primary benefits of access control, such as encapsulation, abstraction, and data integrity, which are fundamental principles in object-oriented programming.

---

### **Question**

### 05. **Given the following code snippet, what happens to the `myShirt` reference when `theShirt` is reassigned to a new `Shirt`?**

```java
public static void main(String[] args) {
    Shirt myShirt = new Shirt();        
    changeShirtColor(myShirt, 'B');        
}

public static Shirt changeShirtColor(Shirt theShirt, char color) {     
    theShirt.setColorCode(color);
    theShirt = new Shirt();
    return theShirt;
}
```

**Instruction:** Choose the option that best answers the question.

- myShirt is assigned to a new object
- myShirt still references its original object
- The original myShirt referenced object is deleted
- theShirt and myShirt always reference the same object

**Answer:**

- myShirt still references its original object

**Explanation:**

When `theShirt` is reassigned to a new `Shirt` object, it no longer references the original object. However, this reassignment does not affect `myShirt`, which still references the original `Shirt` object.

---

### **Question**

### 06. **Match the type change example with its type change description (Promotion/Casting).**

**Answer Choices:**

- **A: long –> int**: Casting
- **B: int –> double**: Promotion
- **C: byte –> short**: Promotion
- **D: double –> float**: Casting

---

### **Question**

### 07. **Specifying the `static` modifier applies which properties to class methods or variables.**

**Instruction:** Choose all options that best answer the question.

- Is unique to an individual object instance
- Is not unique to an object instance
- Can only be accessed with an object reference to a class instance
- Is shared by all objects of the class
- Can be accessed without instantiating the class

**Answers:**

- Is not unique to an object instance
- Is shared by all objects of the class
- Can be accessed without instantiating the class

**Explanation:**

Static members are associated with the class itself, not with any individual instance. They are shared by all objects of the class and can be accessed directly using the class name without needing to create an instance.

---

### **Question**

### 08. **What keyword is used to call an overloaded constructor from another constructor?**

**Instruction:** Choose the option that best answers the question.

- static
- new
- class
- this
- switch

**Answer:**

- this

**Explanation:**

The `this` keyword is used to call an overloaded constructor from another constructor in the same class.

---

### **Question**

### 09. **Select the description which describes the problem with the following code snippet:**

```java
private String name = "Steve";

public static String getName() {
    return name;
}
```

**Instruction:** Choose the option that best answers the question.

- getName must declare a parameter
- name must be declared public
- getName can only access other static members of the class
- getName must be declared private

**Answer:**

- getName can only access other static members of the class

**Explanation:**

The `getName()` method is declared as `static`, which means it can only access static members of the class. However, `name` is an instance variable (non-static), so the `getName()` method cannot directly access it.

---

### **Question**

### 10. **Select the description of how object references are passed to methods.**

**Instruction:** Choose the option that best answers the question.

- The object itself is transferred to the method
- The object itself is copied into a new object
- The object reference value is copied
- The actual object reference is transferred

**Answer:**

- The object reference value is copied

**Explanation:**

In Java, when an object reference is passed to a method, the value of the reference (i.e., the memory address pointing to the object) is copied. The method receives this copied reference, allowing it to access and modify the original object.

---

### **Question**

### 11. **What benefits does encapsulation provide?**

**Instruction:** Choose all options that best answer the question.

- Fields can be accessed directly through an object reference
- A method can change the data type to match the field
- Getters and setters are not required
- A class can be changed as long as the interface remains the same
- Encapsulation encourages good object-oriented design
- Encapsulation encourages good procedural design

**Answers:**

- A class can be changed as long as the interface remains the same
- Encapsulation encourages good object-oriented design

**Explanation:**

Encapsulation allows the internal implementation of a class to be modified without affecting the code that uses the class, as long as the public interface remains consistent. It also encourages good object-oriented design by promoting modularity, maintainability, and security.

---
