

*Date : 04.19.2024*

java.lang.*

1. Object class

2. Wrapper class
- Float class
- Double class 

- Integer, Short, Byte, Long wrapper class

Constructors
1.  Integer(int i)
        Integer i=new Integer(42);
    Integer(String s) throws NumberFormatException
         Integer i=new Integer("42");
         Integer i=new Integer("abc");  //NFE

2. Short(short s)
         Short s=new Short(23);  //error
         Short s=new Short((short)23);   //correct
   Short(String s) throws NFE
         Short s=new Short("23"); 

3. Byte(byte b)
         Byte b1=new Byte(20);  //error
         Byte b1=new Byte((byte)20);  //correct
   Byte(String s) throws NFE
         Byte b1=new Byte("20");

4. Long(long l)
        Long l1=new Long(10);   //correct
        Long l2=new Long(10l);   //correct
   Long(String s) throws NFE
       Long l1=new Long("10");   //correct 

Methods
1. static int parseInt(String s) throws NFE
2. static int parseInt(String s, int radix) throws NFE

public class Main {
    public static void main(String[] args) {
       String s="42";
       int i=Integer.parseInt(s);
       System.out.println(i);  //42
       int j=Integer.parseInt(s,5);
       System.out.println(j); //22   //2*5^0=2
                                //4*5^1=20
       System.out.println(Integer.toBinaryString(2));  //10
       System.out.println(Integer.toOctalString(9)); //11
       System.out.println(Integer.toHexString(10));  //a
       
       System.out.println(Integer.MAX_VALUE);
       System.out.println(Integer.MIN_VALUE);
       System.out.println(Integer.TYPE); //int
    }
}

4. Boolean class
       - used to perform operation on boolean datatype

Constructors
1. Boolean(boolean b)

Boolean b1=new Boolean(true);
SOP(b1);  //true
Boolean b2=new Boolean(false);
SOP(b2);  //false
Boolean b3=new Boolean(True);
SOP(b3);  //error
Boolean b4=new Boolean(hello);
SOP(b4);  //error

2. Boolean(String s) - we can give only true in any format then it will print true, other than true if we provide anything it return false 

Boolean b1=new Boolean("true");
SOP(b1);  //true
Boolean b2=new Boolean("false");
SOP(b2);  //false
Boolean b3=new Boolean("True");
SOP(b3);  //true
Boolean b4=new Boolean("null");
SOP(b4);  //false
Boolean b5=new Boolean("TRUE");
SOP(b5);  //true

5. Character class
      - used to perform operation on char datatype

Constructor
   1. Character(char c)

Methods
1. static boolean isDigit(char c)
2. static boolean isLetter(char c)
3. static boolean isLetterOrDigit(char c)
4. static boolean isUpperCase(char c)
5. static boolean isLowerCase(char c)
6. static boolean isWhiteSpace(char c)
7. static char toUpperCase(char c)
8. static char toLowerCase(char c)

Autoboxing and Unboxing
     - Available from JDK1.5 onwards
     - Autoboxing is automatic conversion of primitive datatype to wrapper class
     - Unboxing is automatic conversion of wrapper class to primitive datatype 

Short s=20;
Boolean b=s instanceof Short;

With Autoboxing                                Without Autoboxing
Integer i;                                      Integer i;
int j;                                          int j;
i=25;  //Autoboxing                             i=new Integer(25);
j=i;  //Unboxing                                j=i.intValue();

3. String class
       - String is final class in java.lang.*
       - fixed length of char, it is immutable class (ie) we cant increase or decrease its size

Syntax: public final class String extends Object implements Cloneable, Serializable, Comparable, CharSequence

Constructors
1. String()
2. String(String s)
3. String(byte[] b)
4. String(byte[] b, int start, int numofbytes)
5. String(char[] c)
6. String(char[] c, int start, int numofchar)
7. String(StringBuffer sb)

Methods
1. String toString() - String representation of object 
2. char charAt(int pos) - return a single char
3. void getChars(int start,int end,char buf[],int targetstart) - return group of chars
4. byte[] getBytes() - convert String to byte[]
5. char[] toCharArray() - convert String to char[]
6. boolean equals(String s) - check the equality of content by taking case into consideration
7. boolean equalsIgnoreCase(String s) - check the equality of content without taking case into consideration
8. ==(equals versus) - check equality of object reference
9. boolean startsWith(String s)
10. boolean endsWith(String s)
11. String toUpperCase()
12. String toLowerCase()
13. int compareTo(String s) - comparing two string taking case into consideration and do sorting, if two values are equal it returns 0, greater means +1, and lesser means -1
14. int compareToIgnoreCase(String s) - comparing two string without taking case into consideration and do sorting, if two values are equal it returns 0, greater means +1, and lesser means -1

https://engage.cloud.microsoft/main/org/hcl.in/threads/eyJfdHlwZSI6IlRocmVhZCIsImlkIjoiMjQzNTYzNzE0MjA1Mjg2NCJ9?trk_copy_link=V2

15. String intern() - stores String object into String pool

String s1="hello";
String s2="hello";
String s3="hi";
String s4=new String("hello");
String s5=new String("hello").intern();

String pool is a storage space in the Java heap memory where string literals are stored. It is also known as String Constant Pool or String Intern Pool. It is privately maintained by the Java String class. By default, the String pool is empty.

In stack memory, only the primitive data types like- int, char, byte, short, boolean, long, float and double are stored. Whereas, in the heap memory, non-primitive data types like strings are stored. A reference to this location is held by the stack memory.

The String Pool is empty by default, and it is maintained privately by the String class.
When we create a string literal, the JVM first checks that literal in the String Constant Pool. If the literal is already present in the pool, its reference is stored in the variable.
However, if the string literal is not found, the JVM creates a new string object in the String Constant Pool and returns its reference.


String str = "Java";
String str1 = new String("Java");

Using String.intern() method

Creating strings using the new keyword allocates memory to the string object in the heap but outside the string constant pool. When we use the String.intern() method, JVM puts the string literal in the String Pool (if not already present), and its reference is stored in the variable.

String str = "Java";
String str1 = new String("Java").intern();
String str2 = new String("Code");
str2.intern();

16. int indexOf(char c)
    int indexOf(String s)
    int indexOf(int charvalue, int startindex)
    int indexOf(String s, int index)
        - used to return position of first occurence of char in given string

17. int lastIndexOf(char c)
    int lastIndexOf(String s)
    int lastIndexOf(int charvalue, int startindex)
    int lastIndexOf(String s, int index)
        - used to return position of last occurence of char in given string
18. String subString(int start) - return part of string from start position
19. String subString(int start, int end) - return part of String from start to end-1
20. int length()
21. String concat(String s) or + operator
22. String trim() - remove leading and trailing character
23. String replace(char oldvalue,char newvalue)

Immutable means we are changing only the address not the value. So immutabilkity means once any value is created it will still present in string pool and not overridder by another value

24. String[] split(String delimiter)
    String[] split(String delimiter, int limit)
        - used to split the string based on some delimiter 
25. boolean matches(String regex) - used to match the string based on regex
26. boolean regionMatches(boolean ignorecase, int toffset, String search, int offset, int length) - used to match part of string
27. int codePointAt(int index)
28. int codePointBefore(int index)
29. int codePointCount(int beginindex, int endindex)
30. boolean contains(String s)
31. static String join(String delimiter, String...s)
32. static String copyValueOf(char c[])
    static String copyValueOf(char c[], int offset, int count)
33. static String format(String format, Object val)

```java
	int a=10;
	printf("%d",a);  //10
```

Syntax:  %+-0wspecifier.precision
+ - add space before number
- - add space after number
0 - pad with zeros
w - total width
specifier - d,f,o,x,s
precision - place after decimal point

```java
public class Main {
	public static void main(String[] args) {
       byte[] b= {65,66,67,68,69};
       String s1=new String(b);
       System.out.println(s1);  //ABCDE
       String s2=new String(b,0,3);
       System.out.println(s2);  //ABC
       
       char c[]= {'J','a','v','a'};
       String s3=new String(c);
       System.out.println(s3); //Java
       String s4=new String(c,1,2);
       System.out.println(s4); //av
       String s5=new String(s4);
       System.out.println(s5); //av
       
       String s6="hello";   //literal
       System.out.println(s6.charAt(1));  //e
       
       String s7="This is a demo of getChars methods";
       int start=10, end=14;
       char buf[]=new char[end-start]; //4
       s7.getChars(start,end,buf,0);
       System.out.println(buf); //demo
       
       String s8="ABCD";
       byte[] b1=s8.getBytes();
       for(byte b2:b1)
                 System.out.println(b2); //65 66 67 68
       
       char c1[]=s8.toCharArray();
       for(char c2:c1)
                 System.out.println(c2); //A B C D
       
       String s9=new String("Hello");
       String s10=new String("Hello");
       String s11=new String("HELLO");
       System.out.println(s9.equals(s10));  //true
       System.out.println(s9.equals(s11));  //false
       System.out.println(s9.equalsIgnoreCase(s11)); //true
       System.out.println(s9==s10); //false
       String s12=s9;
       System.out.println(s9==s12); //true
       
       System.out.println("Foobar".startsWith("Foo")); //true
       System.out.println("Foobar".endsWith("bar")); //true
       System.out.println("Foobar".toUpperCase()); //FOOBAR
       System.out.println("Foobar".toLowerCase()); //foobar
       
       System.out.println("hello".compareTo("hello"));  //0
       System.out.println("carl".compareTo("hello")); //-5
       System.out.println("hello".compareTo("carl")); //5
       System.out.println("hell".compareTo("heck")); //9
       
       String s13="It is the time for all good men to come to their "
                             + "country and pay their due tax";
       System.out.println(s13.indexOf('t')); //1
       System.out.println(s13.indexOf("the")); //6
       System.out.println(s13.indexOf("Z"));  //-1
       System.out.println(s13.indexOf(" ")); //2
       System.out.println(s13.indexOf(116, 7)); //10
       System.out.println(s13.indexOf("the",10));  //43
       System.out.println(s13.lastIndexOf('t')); //75
       System.out.println(s13.lastIndexOf("the")); //65
       System.out.println(s13.lastIndexOf("the", 65)); //43
       
       String s14="HelloWorld";
       System.out.println(s14.substring(5)); //World
       System.out.println(s14.substring(3, 7)); //loWo  //start to end-1
       
       String s15="hello";
       System.out.println(s15.length());  //5
       System.out.println(s15.concat("world")); //helloworld
       System.out.println(s15.length()); //5
       String s16=s15.concat("world");
       System.out.println(s16.length()); //10
       
       String s17=" Hello World ";
       System.out.println(s17.length()); //13
       System.out.println(s17.trim());  //Hello World
       System.out.println(s17.length()); //13
       String s18=s17.trim();
       System.out.println(s18.length()); //11
       
       System.out.println("Hello".replace('e', 'i')); //Hillo
       
       String s19="hello";
       //s19="worlds";
       //System.out.println(s19); //worlds
       String s20="hello";
       System.out.println(s19.equals(s20)); //true
       System.out.println(s19==s20); //true
       String s21=new String("hello");
       s19=s19+"Ram";
       System.out.println(s19); //hello Ram
       
       String s22="one-two-three";
       String tmp[]=s22.split("-");
       for(String t:tmp)
                 System.out.println(t);  //one two  three
       
       String s23="one.two.three";
       String tmp1[]=s23.split(\\.);
       for(String t:tmp1)
                 System.out.println(t);  //one two  three
       
       String s24="A*bunch*of*stars";
       String tmp2[]=s24.split("\\*");
       for(String t:tmp2)
                 System.out.println(t);  //A   bunch   of   stars
       
       String s25="A*bunch*of*stars";
       String tmp3[]=s25.split("\\*",2);
       for(String t:tmp3)
                 System.out.println(t);
       String s26="A*bunch*of*stars";
       String tmp4[]=s26.split("\\*",3);
       for(String t:tmp4)
                 System.out.println(t);
       
       String s27="string is a class";
       String tmp5[]=s27.split("s");
       for(String t:tmp5)
                 System.out.println(t);  //tring i
                                   // a cla
       
       String s28="No concession, no concillation,"
                             + " no compromise, and just give and take policy";
       String tmp6[]=s28.split("concession|concillation|compromise|(give and take)");
       for(String t:tmp6)
                 System.out.println(t);  //No 
                                   //, no 
                                   //, no 
                                   //, and just
                                   //policy
       
       String s29="Welcome to Java";
       System.out.println(s29.matches("Welcome to (.*)"));  //true
       System.out.println(s29.matches("Java"));  //false
       System.out.println(s29.matches("(.*) to (.*)"));  //true    
       System.out.println(s29.matches("(.*) to PHP"));  //false
       
       String s30="ABC Windows test";  //Windows test
       System.out.println(s30.regionMatches(4, "windows", 0, 7));  //false
       System.out.println(s30.regionMatches(true, 4, "windows", 0, 7)); //true
       
       System.out.println("abcd".codePointAt(0)); //97
       System.out.println("abcd".codePointBefore(2)); //98
       System.out.println("abcd".codePointCount(0, 4));  //4
       System.out.println("Hello".contains("e"));  //true
       System.out.println("Hello".contains("E"));  //false
       System.out.println(String.join("-", "one","two","three")); //one-two-three
       
       char c2[]= {'a','b','c','d','e','f','g'};
       String s31="";
       System.out.println(s31.copyValueOf(c2));  //abcdefg
       System.out.println(s31.copyValueOf(c2, 3, 2)); //de
       
       int a=46;
       System.out.println(a); //46
       System.out.println(String.format("%d", a)); //46
       System.out.println(String.format("|%d|", a));  //|46|
       System.out.println(String.format("|%5d|", a));  //|   46|
       System.out.println(String.format("|%-5d|", a));  //|46   |
       System.out.println(String.format("|%06d|", a));  //|000046|
       System.out.println(String.format("|%-06d|", a)); //exception
       System.out.println(String.format("|%f|", 123.456)); //|123.456000|
       System.out.println(String.format("|%.2f|", 123.456)); //|123.46|
       System.out.println(String.format("|%.2f|", 123.436)); //|123.43|
       System.out.println(String.format("|%8.2f|", 123.456)); //|   123.46|
    }
}
```

4. StringBuffer class
        - present in java.lang.*
        - It is a mutable class (ie) variable length of char
        - By default StringBuffer is synchronized or threadsafe, it always gives lower performance 
        - Default capacity of StringBuffer is 16
        - We cant override equals() in StringBuffer, using toString() we convert StringBuffer to String class and then we apply equals()

Constructor
1. StringBuffer()
2. StringBuffer(String s)
3. StringBuffer(int capacity)

Methods
1. int length()
2. char charAt(int pos)
3. void setCharAt(int index, char c)
4. void setLength(int length)
5. int capacity()
6. StringBuffer append(int i)
   StringBuffer append(char i)
   StringBuffer append(String i)
       - adds at end of the StringBuffer
7. StringBuffer insert(int index,int i)
   StringBuffer insert(int index,char i)
   StringBuffer insert(int index,String i)
       - insert the data in between
8. StringBuffer reverse()
9. StringBuffer replace(int start,int end, String s)
10. StringBuffer delete(int start,int end) - delete group of char
    StringBuffer deleteCharAt(int start) - delete single char

public class Main {
    public static void main(String[] args) {
        StringBuffer sb=new StringBuffer("Hello");
        System.out.println(sb); //Hello
        System.out.println(sb.length()); //5
        System.out.println(sb.capacity()); //21=16+5
        System.out.println(sb.charAt(1)); //e
        sb.setCharAt(1, 'i');
        System.out.println(sb); //Hillo
        sb.setLength(2);
        System.out.println(sb); //Hi

        int i=20;
        StringBuffer sb1=new StringBuffer();
        String s1=sb1.append("s=").append(i).append("!").toString();
        System.out.println(s1);  //s=20!
        
        StringBuffer sb2=new StringBuffer("I Java");
        System.out.println(sb2.insert(2, "like ")); //I like Java
        
        StringBuffer sb3=new StringBuffer("Hello");
        System.out.println(sb3.reverse()); //olleH
        
        StringBuffer sb4=new StringBuffer("This is a test");
        System.out.println(sb4.replace(5, 7, "was"));  //This was a test
        
        StringBuffer sb5=new StringBuffer("This is a test");
        System.out.println(sb5.delete(5, 7)); //This a test
        System.out.println(sb5.deleteCharAt(0)); //his a test
    }
}

5. StringBuilder class
       - Available from JDK1.5 onwards
       - similar to StringBuffer but it is not synchronized or threadsafe so it gives better performance than StringBuffer 
