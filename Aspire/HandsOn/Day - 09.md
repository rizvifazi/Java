
*Date : 04.29.2024*

Handson

1. Write a Java program to read all the player information from the user and display the player name and their cap number sorted based on their cap number (descending order). The contact details consist of player name, skill and cap number. Use Collections.sort() method for sorting.

Create a main class "Main.java"
Create Player class with below private  attributes


playerName - String

skill - String

capNumber - Long

Add appropriate getter and setter methods for Player class
Include a constructor for Player class with the arguments player name, skill and cap number
Implement Comparable interface and implement the method compareTo() to perform sorting based on cap number

Input and Output Format:
First input corresponds to the number of players and followed by each player's information.
Refer sample input and output for formatting specifications.

[All text in bold corresponds to input and the rest corresponds to output]
Sample Input/Output :
Enter number of players:
2
Enter player 1 detail
Enter Name
Suresh Raina
Enter Skill
Batsman
Enter Cap Number
265
Enter player 2 detail
Enter Name
Virat Kohli
Enter Skill
Batsman
Enter Cap Number
268
Player list after sorting by cap number in descending order
Virat Kohli-268
Suresh Raina-265


2.Comparator - no of matches player

Write a Java program to get the team name and number of matches played by the team from the user and display a report with team name and number of matches sorted based on the number of matches in ascending order. Use Collection.sort() method to perform the sorting in your main class. Send the Comparator object as second argument to the sort method to use this comparator for sorting. 

Create a main class " Main.java" 
Create a class named Team with the following private member variables / attributes, 
name - String 
numberOfMatches - Long 
Include a constructor accepting Team name and number of matches as arguments 
Add appropriate getter and setter methods for Team class 

Create TeamComparator implementing Comparator interface 
Implement compare method to compare two team objects based on their number of matches played. 

Input and Output Format: 
First input corresponds to the number of teams and followed by each team information. 
Refer sample input and output for formatting specifications. 

[All text in bold corresponds to input and the rest corresponds to output]
Sample Input/Output : 
Enter number of teams: 
3 
Enter team 1 detail 
Enter Name 
Chennai super Kings 
Enter number of matches 
132 
Enter team 2 detail 
Enter Name 
Royal Challengers Bangalore 
Enter number of matches 
139 
Enter team 3 detail 
Enter Name 
Delhi Daredevils 
Enter number of matches 
131 
Team list after sort by number of matches 
131 
132 
139

3.Set - Revenue Manager
The audience for cricket and the population is growing in the largest democracy in the world and it would not decrease in the near future. Sponsorship contracts are based on viewership, so increasing number of viewers means more revenue. There are 5 Ways by which IPL teams are earning revenue. 
. 
The revenue of all IPL teams are classified into the following: 
1. Media rights
2. Sponsorship
3.Ticket sales
4. Stall rental
5. Prize money 

Write a program to get all the revenues based on a category mentioned above and total amount earned. Prompt the user to know whether they want to continue to add revenue or not and finally generate a report to display top earning categories and total amount earned as shown in the sample input and output. 

Since the categories are stored in sorted order so we use TreeSet<Revenue> to store all the Revenue object. The template for the Revenue class contains the method compareTo() to perform the comparation between two revenue objects and return an integer value.  By default the iterator in treeset class returns the values in ascending order and for this requirment we can use descendingIterator() method to get the values in decending order. For more information on TreeSet refer to the Java API document. 

Create a main class " Main.java" 
Create Revenue class with below attributes, 
revenueCategory - String 
amount - Integer 
Include a constructor for Revenue class with arguments revenueCategory and amount 
Include appropiate getter and setter for the revenue class. 

Input and Output Format: 
Refer sample input and output for formatting specifications. 
Display the report Category and Amount seperated by following statement 
  "System.out.println(String.format("%-15s%-15s","Category", "Amount"));" 


[All text in bold corresponds to input and the rest corresponds to output]
Sample Input/Output : 
Enter revenue category 
Sponsorship 
Enter revenue amount 
60000 
Do you want to continue(yes/no): 
yes 
Enter revenue category 
Ticket sales 
Enter revenue amount 
45000 
Do you want to continue(yes/no): 
yes 
Enter revenue category 
Stall rental 
Enter revenue amount 
23000 
Do you want to continue(yes/no): 
no 
Top spending categories 
Category    Amount 
Sponsorship 60000 
Ticket sales 45000 
Stall rental  23000 
Total amount earned: 128000 



Problem Statement:
Given:
public static void before() {
    Set set = new TreeSet();
    set.add(“2”);
    set.add(3);
    set.add(“1”);
    Iterator it = set.iterator();
    while (it.hasNext())
         System.out.print(it.next() + “  ”);
}

Which of the following statements are true?
A.     The before() method will print 1  2.
B.     The before() method will print 1  2   3.
C.     The before() method will print three numbers, but the order cannot be determined.
D.    The before() method will not compile.
E.     The before() method will throw an exception at runtime.

Problem Statement:
Given:
TreeSet map = new TreeSet();
map.add(“one”);
map.add(“two”);
map.add(“three”);
map.add(“four”);
map.add(“one”);
Iterator it = map.iterator();
while (it.hasNext()) {
     System.out.print(it.next() + “ “ );
}

What is the result?
A.     Compilation fails.
B.     one    two     three  four
C.     four   three   two    one
D.    four   one     three   two
E.     one    two    three   four  one
F.      one    four    three   two  one
G.    An exception is thrown at runtime.
H.    The print order is not guaranteed.


Problem Statement:
Given:
import java.util.*;
class CollectionTypes {
        public static void main(String[ ]  args) {
        // insert code here
        x.add(“one”);
        x.add(“two”);
        x.add(“TWO”);
        System.out.println(x.poll());
    }
}

Which inserted at // insert code here, will compile? (Choose all that apply.)
a)  List<String> x = new LinkedList<String>();
b)  TreeSet<String> x = new TreeSet<String>();
c)  HashSet<String> x = new HashSet<String>();
d)  Queue<String> x = new PriorityQueue<String>();
e)  ArrayList<String> x = new ArrayList<String>();
f)  LinkedList<String> x = new LinkedList<String>();

Problem Statement:
Given a method declared as:
public static <E extends Number> List<? super E> process(List<E> nums)

A programmer wants to use this method like the following:
// INSERT DECLARATIONS HERE
output = process(input);

Which pairs of declarations could be placed at // INSERT DECLARATIONS HERE to allow the code to compile? (Choose all that apply.)
a)       ArrayList<Integer> input = null;
ArrayList<Integer> output = null;
b)  ArrayList<Integer> input = null;
List<Integer> output = null;
c)  ArrayList<Integer> input = null;
List<Number> output = null;
d)  List<Number> input = null;
ArrayList<Integer> output = null;
e)  List<Number> input = null;
List<Number> output = null;
f)  List<Integer> input = null;
List<Integer> output = null;
g)       None of the earlier.


Problem Statement:
Which collection class(es) allows you to grow or shrink its size and provides indexed access to its elements, but whose methods are not synchronized? (Choose all that apply.)
A. java.util.HahSet
B. java.util.LinkedHashSet
C. java.util.List
D. java.util.ArrayList
E. java.util.Vector
F. java.util.PriorityQueue

