
*Date : 04.22.2024*

Handson

1. Exception 2(ArrayIndexOutOfBoundsException And NegativeArraySizeException)

Write a program to get the number of overs and the runs scored in each over. Get the over number from the user and display number of runs scored in that over. Let 
•            number of overs be the array size
•            over number be the index of the array+1
•            runs be the array elements

This program may generate 
1. NegativeArraySize Exception when the number of overs is negative
2. ArrayIndexOutOfRange Exception when the over number that is searched is beyond the specified over numbers. 

Use exception handling mechanisms to handle these exceptions.Use a single catch block. In the catch block, print the class name of the exception thrown.
Input and Output Format:
Refer sample input and output for formatting specifications.
All text in bold corresponds to input and the rest corresponds to output.

Sample  Input/Output 1:
Enter the number of overs
3
Enter the number of runs for each over
8
15
12
Enter the over number 
2
Runs scored in this over : 15

Sample  Input/Output 2:
Enter the number of overs
3
Enter the number of runs for each over
8
15
12
Enter the over number 
4
java.lang.ArrayIndexOutOfBoundsException

Sample  Input/Output 3:
Enter the number of overs
-1
Enter the number of runs for each over
java.lang.NegativeArraySizeException


2.Custom Exceptions [Age]

Write a program to get the name and age of the player from the user and  display it. 
player name is a string 
player age is an integer value 
Note : The player is eligible to participate in IPL when their age is 19 and above 
  
This program may generate   
1. InvalidAgeRange Custom Exception when the player's age is below 19 
 Use exception handling mechanisms to handle these exceptions 

Create a class called CustomException which extends Exception and it includes constructor to initialize the message. 
 
 Use appropriate exception handling mechanisms to handle these exceptions  
 
Input and Output Format:
Refer sample input and output for formatting specifications.
All text in bold corresponds to input and the rest corresponds to output.

Sample  Input/Output 1:
Enter the player name
Albie Morkel
Enter the player age
35
Player name : Albie Morkel
Player age : 35

Sample  Input/Output 2:
Enter the player name
Ishan Kishan
Enter the player age
16
CustomException: InvalidAgeRangeException


3. TeamNameNotFound Exception

Write a program to get the two team names i.e expected Runner and Winner team of IPL season 4 and display it.
Team name is a string

Note : The team name given below are only eligible to take part in IPL season 4
Chennai Super Kings
Deccan Chargers
Delhi Daredevils
Kings XI Punjab
Kolkata Knight Riders
Mumbai Indians
Rajasthan Royals
Royal Challengers Bangalore
This program may generate TeamNameNotFound Custom Exception when the expected team entered is not present in the above eligible teams list for IPL season 4.
Use exception handling mechanisms to handle these exceptions

Input and Output Format:
Refer sample input and output for formatting specifications.
All text in bold corresponds to input and the rest corresponds to output.
Sample Input and Output 1:
Enter the expected winner team of IPL Season 4
Chennai Super Kings
Enter the expected runner Team of IPL Season 4
Mumbai Indians
Expected IPL Season 4 winner: Chennai Super Kings
Expected IPL Season 4 runner: Mumbai Indians

Sample Input and Output 1:
Enter the expected winner team of IPL Season 4
Pune Warriors
TeamNameNotFoundException: Entered team is not a part of IPL Season 4
