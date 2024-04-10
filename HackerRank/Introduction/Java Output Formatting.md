
Java's _System.out.printf_ function can be used to print formatted output. The purpose of this exercise is to test your understanding of formatting output using _printf_.

To get you started, a portion of the solution is provided for you in the editor; you must format and print the input to complete the solution.

**Input Format**

Every line of input will contain a _String_ followed by an _integer_.  
Each _String_ will have a maximum of  alphabetic characters, and each _integer_ will be in the inclusive range from  to .

**Output Format**

In each line of output there should be two columns:  
The first column contains the _String_ and is left justified using exactly  characters.  
The second column contains the _integer_, expressed in exactly  digits; if the original input has less than three digits, you must pad your output's leading digits with zeroes.

**Sample Input**

```
java 100
cpp 65
python 50
```

**Sample Output**

```
================================
java           100 
cpp            065 
python         050 
================================
```

**Explanation**

Each _String_ is left-justified with trailing whitespace through the first  characters. The leading digit of the _integer_ is the  character, and each _integer_ that was less than  digits now has leading zeroes.


## Solution 1

```java
import java.util.Scanner;

public class Solution {

    public static void main(String[] args) {
    
		Scanner sc=new Scanner(System.in);
	
		String myNames[] = new String[3];
		int myVals[] = new int[3];
	
		for(int i=0;i<3;i++)
		{
			String s1=sc.next();
			myNames[i] = s1;
			int x=sc.nextInt();
			myVals[i] = x;
			//Complete this line
		}
	
		sc.close();

		System.out.println("================================");
	
		for(int i=0;i<3;i++)
		{
		   System.out.printf("%-14s %0,3d%n",myNames[i], myVals[i]);
			//Complete this line
		}
		System.out.println("================================");
    }
}

```

## Solution 2 

- If the inputs are given one at a time 

```java
import java.util.Scanner;

public class Solution {
public static void main(String[] args) {
        Scanner sc=new Scanner(System.in);
        System.out.println("================================");
        for(int i=0;i<3;i++){
            String s1=sc.next();
            int x=sc.nextInt();
            System.out.printf("%-15s%03d%n", s1, x);
        }
        System.out.println("================================");
	}
}
```



## Reference

[[printf]] - Print f usage
