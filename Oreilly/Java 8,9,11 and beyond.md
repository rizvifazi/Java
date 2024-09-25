

**GitHub Source**: [java91011beyond](https://github.com/henri-tremblay/java91011beyond)

---

## Versions of Java

- **Java 8**
- **Java 9-10**
- **Java 11**
- **Java 12-16**
- **Java 17**
- **Java 18-20**
- **Java 21**

### Java Delivery Process
- **LTS Every 3 Years**  
- Regular releases are supported for 6 months until the next version.  
- Java 21 is a **Long-Term Support (LTS)** version.

### Major JVM Vendors
- **Oracle JDK**  
- **Oracle OpenJDK**
- **Eclipse Adoptium Temurin**
- **Amazon Corretto**
- **IBM J9**
- **Azul Zing**
- **RedHat**

---

## Java Governance

- **JCP (Java Community Process)**: Responsible for Java governance.  
- **JLS (Java Language Specification)**: Defines the Java language.  
- **JSR (Java Specification Request)**: Large changes proposed to JCP.  
- **JEP (Java Enhancement Proposal)**: Small enhancements.

**Example of JEPs:**
- **JEP 361**: Switch Expressions
- **JEP 395**: Records
- **JEP 406**: Pattern matching for switch (Preview)

---

## Major Projects

### **Valhalla**: Introduces value types.  
### **Loom**: New threads called fibers for lightweight concurrency.  
### **Panama**: Improved I/O handling.  
### **Amber**: Focus on improving developer productivity.  
### **Leyden**: Startup time optimizations for Java applications.

---

## Deprecation
Deprecation in Java has become stricter. Example:
```java
@Deprecated(since="1.2", forRemoval=true)
public native int countStackFrames();
```

Classes and methods removed across versions:
- **Java 8**: `Unsafe.defineClass()`
- **Java 9 and beyond**: Progressive removal of unsafe methods and modules.

---

## Java Garbage Collectors

**Java < 8**
- Serial, Parallel, CMS, iCMS

**Java 9**: G1 (Default GC)

**Java 11**
- **Epsilon GC**: A no-op garbage collector.
- **Z GC**: Experimental.

**Java 15**: Introduction of Shenandoah and further improvements to G1.

**Java 21**: Generational Z Garbage Collector.

---

## Key Java Trends

1. **Deprecation**: Stricter rules for deprecated methods.
2. **Garbage Collection**: Evolving with every release.
3. **Encapsulation**: Stronger internal API encapsulation.
4. **Developer Efficiency**: Introduction of features like local variable type inference (`var`).
5. **Performance**: Constant improvements in efficiency and performance.

---

## Example Code Snippets

### **Switch Expressions**
```java
private boolean isWeekDay(DayOfWeek day) {
    return switch(day) {
        case MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY -> true;
        case SATURDAY, SUNDAY -> false;
        default -> throw new IllegalStateException("A new day was added in my week: " + day);
    };
}
```

### **Text Blocks**
```java
String script = """
    function hello() {
        print("Hello, world");
    }
    hello();
""";
```

---

## Features by Version

### **Java 9 (Sept 2017)**
- **JEP 200**: Modular JDK
- **JEP 238**: Multi-Release JAR Files
- **JEP 282**: Java Linker (`jlink`)

### **Java 10 (March 2018)**
- **JEP 286**: Local-Variable Type Inference (`var`)

### **Java 11 (Sept 2018)**
- **JEP 321**: Standard HTTP Client API
- **JEP 323**: Local-Variable Syntax for Lambda Parameters

### **Java 13 (Sept 2019)**
- **JEP 355**: Text Blocks (Preview)

### **Java 15 (Sept 2020)**
- **JEP 360**: Sealed Classes (Preview)

### **Java 17 (Sept 2021)**
- **JEP 356**: Enhanced Pseudo-Random Number Generators

### **Java 21 (Sept 2023)**
- **JEP 443**: Unnamed Patterns and Variables (Preview)
- **JEP 452**: Key Encapsulation Mechanism API

---

## Resources

- **Java is still free**: [Article](https://medium.com/@javachampions/java-is-still-free-3-0-0-ocrt-2021-bca75c88d23b)
- **JDK Documentation**: [Docs](https://docs.oracle.com/en/java/javase/)
- **GitHub Source**: [java91011beyond](https://github.com/henri-tremblay/java91011beyond)
  
---

### Notes for Developers
- Use **JEPs** to track Java enhancements and plan upgrades.
- Pay attention to deprecated features to avoid future breaks.
- Optimize memory management by leveraging the latest **Garbage Collectors**.
- Consider new syntax features like **Switch Expressions** and **Pattern Matching** to simplify code logic.

---




