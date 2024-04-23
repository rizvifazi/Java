
*Date : 04.12.2024*



5. Method Overloading / Illustration(Match)
Write a program to illustrate Method Overloading.
  
Create a class named Match.
  
There are no attributes in this class.
  
Include the following methods in the Match class.
  
void displayMatchDetails(DateTime matchDate) --- In this method, display the date on which the match will be held in MM-dd-yyy format,Input date format is dd/MM/yyyy
  
void displayMatchDetails(String venue) --- In this method, venue has “stadium name,city”. display the stadium name and city seperately by using split() method.
  
void displayMatchDetails(String winnerTeam,long runs) --- In this method, display the outcome of the match – winner Team and Won by how many runs.
  
  
  
Create a Main class and in the main method test the Match class.
  
Input and Output Format:
Refer sample input and output for formatting specifications.
  
All text in bold corresponds to input and the rest corresponds to output.
  
Sample Input and Output 1:
  
Menu
  
1.Match Date
  
2.Match Venue
  
3.Match Outcome
  
1
  
Enter the date of the match
  
15/09/2015
  
Match Date : 09-15-2015
Sample Input and Output 2:
Menu
1.Match Date
2.Match Venue
3.Match Outcome
**2**
Enter venue of the match
**Eden Gardens,Kolkata**
Match Venue :
Stadium : Eden Gardens
City : Kolkata
  
  
Sample Input and Output 3:
Menu
1.Match Date
2.Match Venue
3.Match Outcome
**3**
Enter the winner team of the match
**CSK**
Enter the number of runs
**12**
Match Outcome :
CSK won by 13 runs.


============


**01.**  **Inheritance 1 - Illustration**
The task is to calculate the area of the shape using a menu driven application.
Write a Java program to Implement this task.
Create a class called Shape.
Include the following protected data members / attributes:
shapeName – of type String
Include the following methods :
Create a constructor that initializes the shapeName
calculateArea –  The return type of this method is Double. This method returns 0.
Create a class called Square that extends Shape
Include the following private data members / attributes:
side – of type Integer.
Include the following methods :
Create a constructor that initializes the side. (1-argument constructor). Initialize the shapeName as "Square".
calculateArea – calculates and returns the area of the square. The return type of this method is Double.
Create a class called Rectangle that extends Shape 
Include the following private data members / attributes:
length – of type Integer.
breadth – of type Integer.
Include the following methods :
Create a constructor that initializes the length and breadth. (2-argument constructor). Initialize the shapeName as "Rectangle".
calculateArea - calculates and returns the area of the rectangle. The return type of this method is Double.
Create a class called Circle that extends Shape
Include the following private data members / attributes:
radius – of type Integer.
Include the following methods :
Create a constructor that initializes the radius. (1-argument constructor). Initialize the shapeName as "Circle".
calculateArea – calculates and returns the area of the circle. The return type of this method is Double.
Include appropriate getters and setters.
Input and Output Format:
Refer sample input and output for formatting specifications.
All text in bold corresponds to input and the rest corresponds to output.
Format the output with two decimal points
Sample Input and Output 1:
1. Rectangle
2. Square
3. Circle
Area Calculator --- Choose your shape
**1**
Enter length and breadth:
**100**
**40**
Area of Rectangle is:4000.00
Sample Input and Output 2:
1. Rectangle
2. Square
3. Circle
Area Calculator --- Choose your shape
**2**
Enter side:
**20**
Area of Square is:400.00
Sample Input and Output 3:
1. Rectangle
2. Square
3. Circle
Area Calculator --- Choose your shape
**3**
Enter Radius:
**5**
Area of Circle is:78.54
**02.**  **Abstract Class I – Shape**
[Adhere to the OOPs specifications specified here. Follow the naming conventions for getters and setters. Download the template code provided and fill in the missing code]
Create an abstract class named Shape with the following protected attributes / member variables.
String name
Include a 1-argument constructor.
Include getters and setters.
Include an abstract method named calculateArea() . This method returns a Float value.
Create a class named Circle . The class Circle is a derived class of Shape. Include the following private attributes / member variables.
Integer radius
Include a 2-argument constructor. The order of the arguments is name, radius.
Include getters and setters.
Override the abstract method calculateArea() defined in the Shape class. This method returns the area of the circle. [Take the value of pi as 3.14]
Create a class named Square . The class Square is a derived class of Shape. Include the following private attributes / member variables.
Integer side
Include a 2-argument constructor. The order of the arguments is name, side.
Include getters and setters.
Override the abstract method calculateArea() defined in the Shape class. This method returns the area of the square.
Create a class named Rectangle . The class Rectangle is a derived class of Shape. Include the following private attributes / member variables.
Integer length
Integer breadth
Include a 3-argument constructor. The order of the arguments is name, length, breadth
Include getters and setters.
Override the abstract method calculateArea() defined in the Shape class. This method returns the area of the rectangle.
Create another class called Main. In the method, create instances of the above classes and test the above classes.
Input and Output Format:
Refer sample input and output for formatting specifications.
All Float values are displayed correct to 2 decimal places.
All text in bold corresponds to input and the rest corresponds to output.
Sample Input and Output 1:
Circle
Square
Rectangle
Enter the shape name
**Circle**
Enter the radius
**25**
Area of Circle is 1962.50
Sample Input and Output 2:
Circle
Square
Rectangle
Enter the shape name
**Square**
Enter the side
**23**
Area of Square is 529.00
Sample Input and Output 3:
Circle
Square
Rectangle
Enter the shape name 
**Rectangle**
Enter the length
**45**
Enter the breadth
**60**
Area of Rectangle is 2700.00
**03.**  **Player-International Player**
Write a program to illustrate Method Overriding. 
Create a class named  Player with following protected attributes.
String name;
String country;
Create appropriate Constructor. 
create a method public void displayDetails() to display the player details. 
Create a class named  InternationalPlayer  that extends  Player class. 
which includes following private attributes
String capNumber;
Long noOfTestAppearance;
Long noOfODIAppearance;
  Create appropriate Constructor. 
Override the method public void displayDetails() defined in the Player class to  display InternationalPlayer details and player details 
Create a Main class and in the main method test the above class. 
Input and Output Format: 
Refer sample input and output for formatting specifications. 
All text in bold corresponds to input and the rest corresponds to output. 
  Note: Display the text " Player Details: " inside the method DisplayDetails 
Sample Input and Output 1: 
Enter player name 
**Virat Kohli** 
Enter player country 
**India** 
Enter the Cap number 
**268** 
Enter the number of test appearnace 
**48** 
Enter the number of ODI appearnace 
**176** 
Player Details: 
Player name : Virat Kohli 
Country : India 
Cap number : 268 
Number of test appearnace : 48 
Number of ODI appearnace : 176 
**04.**   **Simple Interface**
An Interface consists of a contract of set of methods with only declaration and no implementation. Any class which implements the interface commits that all methods would be implemented. 
Here is a program to illustrate a simple interface. 
1. Create an interface IPlayerStatistics 
 Add a method with the following prototype 
--- public void displayPlayerStatistics 
2. Create class Player which implements the IPlayerStatistics Interface 
Include private data members : 
String name 
String teamName 
Integer noOfMatches 
Long totalRunsScored 
Integer noOfWicketsTaken 
Include an 5 argument constructor with following arguments:  name, teamName, noOfMatches, totalRunsScored, noOfWicketsTaken 
and implement the interface method public void displayPlayerStatistics to display the player details. 
Create a  Main class with main method to test test above classes.  
Sample Input and Output 1: 
[All text in bold corresponds to input and the rest corresponds to output.] 
Enter player name 
**Ravichandran Ashwin** 
Enter team name 
**Chennai Super Kings** 
Enter number of matches played 
**86** 
Enter total runs scored 
**185** 
Enter number of wickets taken 
**89** 
Player Details 
Player name : Ravichandran Ashwin 
Team name : Chennai Super Kings 
No of matches : 86
Total runsscored : 185 
No of wickets taken : 89
