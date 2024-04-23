
*Date : 04.18.2024*

Handson

1. IPL Merchandise is an alternative form of revenue and brings substantial income.

Another merchandise company called “Fundas” has come up with a native flair offering customized mugs, team badges, helmets, etc. The company has decided to print a special code on the merchandises. The special code contains the captions of the IPL teams along with the jersey number of the celebrity players of the corresponding team on the merchandises. The code to be printed is considered valid for printing only if their:
--> first word is one of the team's caption [RCB, MI, CSK, SRH, KXIP, DD, KKR, RPSG and GL]
--> second word is the jersey number
Write a program that reads a string S corresponding to the team name and jersey number and validates if the name is eligible to be printed on the stocks.
Include a class UserMainCode with a static method called  validateTeam  which accepts a string and its return type is bool. In this method display the details as given in sample input and output.
Create a Class Main which would be used to accept  two Strings and call the static method called  validateTeam present in UserMainCode.
Input Format:
First line of the input is a string S, that corresponds to the team name and jersey number.

Output Format:
Output should display “Valid” if the team name and jersey number is valid for printing. Otherwise print “Invalid”.

Sample Input 1 :
CSK 7
Sample Output 1 :
Valid

Sample Input 2 :
RCB1 18
Sample Output 2 :
Invalid

2. In Cricket it is so common that the players are often called by their last names. Few cricketers have their origins from the same regions of the country which is why they have common last names. Sandeep is now entrusted with yet another task that is to check for the last names of players.

Given two player's names P1 and P2, Sandeep has to write a program to find if the last name of the two given players are the same. Help him do this using String Builder  method.
Include a class UserMainCode with a static method called display which accepts two strings and its return type is void. In this method display the details as given in sample input and output.

Create a Class Main which would be used to accepts two  Strings and call the static method called display present in UserMainCode.
Input Format:
First line of the input is a string P1, that corresponds to the first player's name.
Second line of the input is a string P2, that corresponds to the second player's name.

Output Format:
Output should print in a single line “Yes” if the last names of the players are the same. Otherwise print “No”.

Sample input
Mohit Sharma
Rohit Sharma

Sample output
Yes


Sample input
Mohit Sharma
Virat Kohli

Sample output
No

3. Write a program to read a string and find whether it is a valid string or not.
Validation Rules :
1. It accepts the player name as a string and is appended with the player's skill.
2.It ends with a symbol ,the symbol is '*' if the player is a raider and it is '#' if the player is a defender.
3.Player's first name,last name and skill should start with upper case letters

Include a class UserMainCode with a static method validatePlayer  which accepts a string. In this method check whether the given player name is valid as per the validation rules mentioned above. The return type is Boolean.


Create a Class Main which would be used to accept the string and call the static method present in UserMainCode.

Input and Output Format:
Input consists of a string.
Output consists of a string “Valid” or “Invalid”.
Refer sample output for formatting specifications.

Sample Input 1:
Anup Kumar-Raider*
Sample Output 1:
Valid

Sample Input 2:
Surender Nada-Defender#
Sample Output 2:
Valid

Sample Input 3:
Rohit Rana-Defender*
Sample Output 3:
Invalid

4. Write a program to read a string and find whether it is a valid string or not.
Validation Rules :
1. It accepts the player name as a string ,player name length should be between 4 to 20.

2..It starts with four digit number representing the player's debutant year.

3.It ends with single digit number representing the number of IPL season played by the player.

Include a class UserMainCode with a static method validatePlayer which accepts a string. In this method check whether the given player name is valid as per the validation rules mentioned above. The return type is Boolean.



Create a Class Main which would be used to accept the string and call the static method present in UserMainCode.

Input and Output Format:
Input consists of a string.

Output consists of a string “Valid” or “Invalid”.
Refer sample output for formatting specifications.

Sample Input 1:

2013Mohit Sharma3

Sample Output 1:

Valid

Sample Input 2:

200Mohammad Kaif

Sample Output 2:

Invalid

5. T20 IPL board get the number of player names and finds the players having the string “Sharma” in their name. Write a program to get the player names in an array and use Contains method to get the players whose name has the string "Sharma". 

Input and Output Format: 
Refer sample input and output for formatting specifications. 

Sample Input/Output 1: 
Enter number of players 
5 
Enter player names 
Rohit Sharma
Adam Smith
Ishant Sharma
Mohit Sharma
Jaspirit Bumrah 
Rohit Sharma 
Ishant Sharma 
Mohit Sharma
