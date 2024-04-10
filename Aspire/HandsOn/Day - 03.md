*Date : 04.08.2024*


Handson

1. Venue Details

  

[Note :

Strictly adhere to the object oriented specifications given as a part of the problem statement.

Use the same class names and member variable names.

Follow the naming conventions mentioned for getters/setters.

Create 2 separate classes in 2 separate files.]

  

Create a class named Venue with the following private member variables/attributes.

  

String name

  

String city

  

Include a 2-argument argument constructor in this class. The arguments passed to the constructor are in this order --- name, city.

Include a default, empty constructor.

  

Include appropriate getters and setters.

  

[Naming Convention:

  

getters : getName getCity...

  

setters : setName setCity...]

  

Create another class named Main and include a main method to test the above class(Print the output in Main Class).

  

Input and Output Format:

  

Refer sample input and output for formatting specifications.

  

Use list of objects to read venue details and use String.split() function to display the venue details and

  

All text in bold corresponds to the input and the rest corresponds to output.

  

Sample Input and Output :

  

Enter the number of venues

2

Enter the details of venue 1

M. Chinnasamy Stadium,Bangalore  

Enter the details of venue 2

M. A.Chidambaram Stadium,Chennai

Venue Details

Venue Name : M. Chinnasamy Stadium

City Name : Bangalore

Venue Name : M. A.Chidambaram Stadium

City Name : Chennai

  
  

2. Innings Detail

[Note :

Strictly adhere to the object-oriented specifications given as a part of the problem statement.

Use the same class names and member variable names.

Follow the naming conventions mentioned for getters/setters.

Create 2 separate classes in 2 separate files.

] 

  

Create a class named Innings with the following private member variables/attributes 

  

String battingTeam; 

Long runs; 

  

Include a 2-argument argument constructor in this class. The arguments passed to the constructor are in this order --- battingTeam, runs. 

  

Include appropriate getters and setters. 

[Naming Convention: 

getters : getBattingTeam getRuns ... 

setters : setBattingTeam, setRuns...] 

  

Override the toString() method to display the Innings details in the format shown in the output. 

[Example :   RCB -- 190] 

  

Create another class named Main and write the main method to test the above class. 

  

Input and Output Format: 

 Refer sample input and output for formatting specifications. 

Use array of objects to read innings details. It includes firstinnings and secondinnings 

All text in bold corresponds to the input and the rest corresponds to output. 

Sample Input and Output : 

Enter the number of innings 

2 

Enter the values for Innings 1 

Enter the BattingTeam 

RCB 

Enter the runs scored 

190 

Enter the values for Innings 2 

Enter the BattingTeam 

CSK 

Enter the runs scored 

195 

Innings Details 

Innings 1 

RCB -- 190 

Innings 2 

CSK -- 195 

  
  

3.Player Details

  

[Note :

Strictly adhere to the object oriented specifications given as a part of the problem statement.

Use the same class names and member variable names.

Follow the naming conventions mentioned for getters / setters.

Create 3 separate classes in 3 separate files.] 

  

Create a class named Player with the following private member variables / attributes 

  

Data Type           Variable Name

String    name

String    country

String    skill

Include appropriate getters, setters and constructors. 

  

Naming Convention : 

getters --- getName,etc... 

setters --- setName,etc... 

Include a default constructor. 

  

Include a 3-argument constructor --- the first argument corresponds to the name and the second argument corresponds to the country and the third argument corresponds to the skill. 

  

Override the toString() method to display the player details in the following format. 

String.format("%-15s %-15s %-15s",name,country,skill); 

  
  

Create a class named PlayerBO and include the following methods 

  

No         Method Name   Method Description

1            void displayPlayerDetails(Player player) In this method, display the details of  the player.

Input and Output Format: 

Refer sample input and output for formatting specifications. 

All text in bold corresponds to input and the rest corresponds to output. 

Note : The statement " Player Details" in the output is displayed in the method inside the BO class. 

Sample Input and Output : 

Enter the player name 

MS Dhoni 

Enter the country name 

India 

Enter the skill 

All Rounder 

Player Details 

MS Dhoni    India      All Rounder 

  
  

4.Delivery Details

  

[ Note :

Strictly adhere to the object oriented specifications given as a part of the problem statement.

Use the same class names and member variable names.

Follow the naming conventions mentioned for getters / setters.

Create 3 separate classes in 3 separate files.] 

  

Create a class named Delivery with the following private member variables / attributes 

  

Data Type           Variable Name

Long      over

Long      ball

String    batsman

String    bowler

String    nonStriker

Include appropriate getters, setters and constructors. 

Naming Convention : 

getters --- getOver,etc... 

setters --- setOver,etc... 

  

Include a 5-argument constructor --- the first argument corresponds to the value of over , second argument corresponds to the value of ball , third argument corresponds to the value of batsman , fourth argument corresponds to the value of bowler and the fifth argument corresponds to the value of nonStriker . 

  

Override the toString() method to display the delivery details in the following format specified in the output. 

  

Create a class named DeliveryBO and include the following methods 

No         Method Name   Method Description

1            void displayAllDeliveryDetails(Delivery[] deliveryList)       In this method, display the details of all the Deliveries.

  

Input and Output Format: 

Refer sample input and output for formatting specifications. 

All text in bold corresponds to input and the rest corresponds to output. 

Note : The statement " Delivery Details" in the output is displayed in the method inside the BO class. 

Sample Input and Output : 

Enter the number of deliveries 

2 

Enter the over 

1 

Enter the ball 

1 

Enter the batsman 

Kohli 

Enter the bowler 

DJ Bravo 

Enter the nonStriker 

Watson 

Enter the over 

1 

Enter the ball 

2 

Enter the batsman 

Kohli 

Enter the bowler 

DJ Bravo 

Enter the nonStriker 

Gayle 

Delivery Details 

Delivery -- 1 

Over: 1 

Ball : 1 

Batsman: Kohli 

Bowler: DJ Bravo 

NonStriker: Watson 

Delivery -- 2 

Over :1 

Ball : 2 

Batsman: Kohli 

Bowler: DJ Bravo 

NonStriker: Gayle