
*Date : 05.14.2024*

Complete the following assignment:

a)	Create the table PROGRAMMER with the given information using SQL CREATE TABLE command:

| Attribute Name | Description/Data Type/Constraint                                        |
| -------------- | ----------------------------------------------------------------------- |
| EmpNo          | Employee's unique ID. Max. 5 characters, numeric.                       |
| ProjId         | Project in which programmer participates. Max. 5 characters, varchar.   |
| LastName       | Surname of employee. Max. 30 characters. Required.                      |
| FirstName      | Employee's first name. Max. 30 characters.                              |
| HireDate       | Date on which employee was hired. Date data type.                       |
| Language       | Programming language used by programmer. Max. 15 characters.            |
| TaskNo         | Number of the task associated with the project. Numeric, max. 2 digits. |
| Privilege      | Type of privilege given to programmer. Max. 25 characters.              |


```mysql
Enter password: **************
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.3.0 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| javabatch          |
| mysql              |
| performance_schema |
| sakila             |
| sys                |
| world              |
+--------------------+
7 rows in set (0.01 sec)

mysql> use javabatch;
Database changed
mysql> show tables;
+---------------------+
| Tables_in_javabatch |
+---------------------+
| customer            |
| customer1           |
| customer2           |
| customer3           |
+---------------------+
4 rows in set (0.00 sec)

mysql> CREATE TABLE PROGRAMMER(
    -> EmpNo int(5),
    -> LastName varchar(30) NOT NULL,
    -> FirstName varchar(30),
    -> HireDate date,
    -> ProjId varchar(5),
    -> Language varchar(15),
    -> TaskNo int(2),
    -> Privilege varchar(25),
    -> constraint pg_pk PRIMARY KEY(EmpNo));
Query OK, 0 rows affected, 2 warnings (0.04 sec)

mysql> desc PROGRAMMER;
+-----------+-------------+------+-----+---------+-------+
| Field     | Type        | Null | Key | Default | Extra |
+-----------+-------------+------+-----+---------+-------+
| EmpNo     | int         | NO   | PRI | NULL    |       |
| LastName  | varchar(30) | NO   |     | NULL    |       |
| FirstName | varchar(30) | YES  |     | NULL    |       |
| HireDate  | date        | YES  |     | NULL    |       |
| ProjId    | varchar(5)  | YES  |     | NULL    |       |
| Language  | varchar(15) | YES  |     | NULL    |       |
| TaskNo    | int         | YES  |     | NULL    |       |
| Privilege | varchar(25) | YES  |     | NULL    |       |
+-----------+-------------+------+-----+---------+-------+
8 rows in set (0.00 sec)
```

b)	Insert the following data into the PROGRAMMER table:

| EmpNo | LastName  | FirstName | HireDate   | ProjId | Language | TaskNo | Privilege    |
| ----- | --------- | --------- | ---------- | ------ | -------- | ------ | ------------ |
| 201   | Gupta     | Saurav    | 1995-01-01 | NPR    | VB       | 52     | Secret       |
| 390   | Ghosh     | Pinky     | 1993-05-01 | KCW    | Java     | 11     | Top Secret   |
| 789   | Agarwal   | Praveen   | 1998-08-31 | Rnc    | VB       | 11     | Secret       |
| 134   | Chaudhury | Supriyo   | 1995-07-15 | TIPPS  | C++      | 52     | Secret       |
| 896   | Jha       | Ranjit    | 1997-06-15 | KCW    | Java     | 10     | Top Secret   |
| 345   | John      | Peter     | 1999-11-15 | TIPPS  | Java     | 52     |              |
| 563   | Anderson  | Andy      | 1994-08-15 | NITTS  | C++      | 89     | confidential |


```mysql
mysql> INSERT INTO PROGRAMMER values(201,'Gupta','Saurav',1995-01-01,'NPR','VB',52,'Secret');
ERROR 1292 (22007): Incorrect date value: '1993' for column 'HireDate' at row 1
mysql> INSERT INTO PROGRAMMER values(201,'Gupta','Saurav',19950101,'NPR','VB
',52,'Secret');
Query OK, 1 row affected (0.01 sec)

mysql> select * from programmer;
+-------+----------+-----------+------------+--------+----------+--------+-----------+
| EmpNo | LastName | FirstName | HireDate   | ProjId | Language | TaskNo | Privilege |
+-------+----------+-----------+------------+--------+----------+--------+-----------+
|   201 | Gupta    | Saurav    | 1995-01-01 | NPR    | VB       |     52 | Secret    |
+-------+----------+-----------+------------+--------+----------+--------+-----------+
1 row in set (0.00 sec)
       INSERT INTO PROGRAMMER values(390,'Ghosh','Pinky',19930105,'KCW','Java',11,'Top Secret');
mysql>
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO PROGRAMMER values(789,'Agarwal','Praveen',19980831,'Rnc','VB',11,'Secret');
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO PROGRAMMER values(134,'Chaudhury','Supriyo',19950715,'TIPPS','C++',52,'Secret
');
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO PROGRAMMER values
    -> 134,'Chaudhury','Supriyo',19950715,'TIPPS','C++',52,'Secret
    '> ^C
mysql> INSERT INTO PROGRAMMER values
    -> (896,'Jha','Ranjit',19970615,'KCW','Java',10,'Top Secret'),
    -> (345,'John','Peter',19991115,'TIPPS','Java',52,''),
    -> (563,'Anderson','Andy',19940815,'NITTS','C++',89,'confidential');
Query OK, 3 rows affected (0.01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from PROGRAMMER;
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
| EmpNo | LastName  | FirstName | HireDate   | ProjId | Language | TaskNo | Privilege    |
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
|   134 | Chaudhury | Supriyo   | 1995-07-15 | TIPPS  | C++      |     52 | Secret       |
|   201 | Gupta     | Saurav    | 1995-01-01 | NPR    | VB       |     52 | Secret       |
|   345 | John      | Peter     | 1999-11-15 | TIPPS  | Java     |     52 |              |
|   390 | Ghosh     | Pinky     | 1993-01-05 | KCW    | Java     |     11 | Top Secret   |
|   563 | Anderson  | Andy      | 1994-08-15 | NITTS  | C++      |     89 | confidential |
|   789 | Agarwal   | Praveen   | 1998-08-31 | Rnc    | VB       |     11 | Secret       |
|   896 | Jha       | Ranjit    | 1997-06-15 | KCW    | Java     |     10 | Top Secret   |
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
7 rows in set (0.00 sec)

```

 
c)	Create a table WEATHER with following data:

| City       | State       | High | Low |
| ---------- | ----------- | ---- | --- |
| Calcutta   | West Bengal | 105  | 90  |
| Trivandrum | Kerala      | 101  | 92  |
| Mumbai     | Maharashtra | 88   | 69  |
| Bangalore  | Karnataka   | 77   | 60  |
| New Delhi  |             | 80   | 72  |

```mysql
mysql> CREATE TABLE WEATHER(City varchar(30),State varchar(20),High int(3),Low int(3),constraint primary key(City));
Query OK, 0 rows affected, 2 warnings (0.02 sec)

mysql> desc WEATHER;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| City  | varchar(30) | NO   | PRI | NULL    |       |
| State | varchar(20) | YES  |     | NULL    |       |
| High  | int         | YES  |     | NULL    |       |
| Low   | int         | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)

mysql> INSERT INTO WEATHER VALUES
    -> ('Calcutta','West Bengal',105,90),
    -> ('Trivandrum','Kerala',101,92),
    -> ('Mumbai','Maharashtra',88,69),
    -> ('Bangalore','Karnataka',77,60),
    -> ('New Delhi','',80,72);
Query OK, 5 rows affected (0.01 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+
| City       | State       | High | Low  |
+------------+-------------+------+------+
| Bangalore  | Karnataka   |   77 |   60 |
| Calcutta   | West Bengal |  105 |   90 |
| Mumbai     | Maharashtra |   88 |   69 |
| New Delhi  |             |   80 |   72 |
| Trivandrum | Kerala      |  101 |   92 |
+------------+-------------+------+------+
5 rows in set (0.00 sec)
```

d)	Create a table BOOKS with the following data

| BookId | Title | TopicId | PublisherName            | PlaceOfPublication | Price | PurchaseDate | ShelfNo |
| ------ | ----- | ------- | ------------------------ | ------------------ | ----- | ------------ | ------- |
| 8293   | DBMS  | DB1     | Prentice Hall            | Mumbai             | 255   | 1995-01-01   | S11     |
| 5645   | DBMS  | DB1     | Pearson Education        | Mumbai             | 655   | 1993-01-05   | S12     |
| 6565   | C     | C1      | TMH                      | Mumbai             | 840   | 1998-08-31   | S66     |
| 6567   | C++   | Cplus1  | ABC Publishers           | Delhi              | 300   | 1995-07-15   | S77     |
| 4576   | JAVA  | JAVA1   | Guru Govind Publications | Delhi              | 500   | 1997-06-15   | S87     |
| 3433   | OOPS  | OOPS1   | Dave Publishers          | Pune               | 600   | 1999-11-15   | S56     |
| 4655   | SAD   | SAD1    | Sajan Publications       | Cochin             | 700   | 1994-08-15   | S76     |

```mysql
mysql> CREATE TABLE BOOKS(BookId int(4),Title varchar(10),TopicId varchar(10),PublisherName varchar(50),PlaceofPublication varchar(20),Price decimal(5,2),Pu
rchaseDate date,ShelfNo varchar(5));
Query OK, 0 rows affected, 1 warning (0.03 sec)

mysql> desc BOOKS;
+--------------------+--------------+------+-----+---------+-------+
| Field              | Type         | Null | Key | Default | Extra |
+--------------------+--------------+------+-----+---------+-------+
| BookId             | int          | YES  |     | NULL    |       |
| Title              | varchar(10)  | YES  |     | NULL    |       |
| TopicId            | varchar(10)  | YES  |     | NULL    |       |
| PublisherName      | varchar(50)  | YES  |     | NULL    |       |
| PlaceofPublication | varchar(20)  | YES  |     | NULL    |       |
| Price              | decimal(5,2) | YES  |     | NULL    |       |
| PurchaseDate       | date         | YES  |     | NULL    |       |
| ShelfNo            | varchar(5)   | YES  |     | NULL    |       |
+--------------------+--------------+------+-----+---------+-------+
8 rows in set (0.00 sec)

mysql> ALTER TABLE BOOKS add constraint bk_pk PRIMARY KEY(BookId);
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc BOOKS;
+--------------------+--------------+------+-----+---------+-------+
| Field              | Type         | Null | Key | Default | Extra |
+--------------------+--------------+------+-----+---------+-------+
| BookId             | int          | NO   | PRI | NULL    |       |
| Title              | varchar(10)  | YES  |     | NULL    |       |
| TopicId            | varchar(10)  | YES  |     | NULL    |       |
| PublisherName      | varchar(50)  | YES  |     | NULL    |       |
| PlaceofPublication | varchar(20)  | YES  |     | NULL    |       |
| Price              | decimal(5,2) | YES  |     | NULL    |       |
| PurchaseDate       | date         | YES  |     | NULL    |       |
| ShelfNo            | varchar(5)   | YES  |     | NULL    |       |
+--------------------+--------------+------+-----+---------+-------+
8 rows in set (0.00 sec)

mysql> INSERT INTO BOOKS VALUES
    -> (8293,'DBMS','DB1','Prentice Hall', 'Mumbai', 255,19950101,'S11'),
    -> ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '' at line 2
mysql> INSERT INTO BOOKS VALUES(8293,'DBMS','DB1','Prentice Hall', 'Mumbai', 255,19950101,'S11');
Query OK, 1 row affected (0.01 sec)

mysql> select * from BOOKS;
+--------+-------+---------+---------------+--------------------+--------+--------------+---------+
| BookId | Title | TopicId | PublisherName | PlaceofPublication | Price  | PurchaseDate | ShelfNo |
+--------+-------+---------+---------------+--------------------+--------+--------------+---------+
|   8293 | DBMS  | DB1     | Prentice Hall | Mumbai             | 255.00 | 1995-01-01   | S11     |
+--------+-------+---------+---------------+--------------------+--------+--------------+---------+
1 row in set (0.00 sec)

mysql> INSERT INTO BOOKS VALUES(8293,'DBMS','DB1','Prentice Hall', 'Mumbai', 255,19950101,'S11')
    -> ^C
mysql> INSERT INTO BOOKS VALUES
    -> (5645,'DBMS','DB1','Pearson Education', 'Mumbai', 655,19930105,'S12'),
    -> (6565,'C','C1','TMH', 'Mumbai', 840,19980831,'S66'),
    -> (6567,'C++','Cplus1','ABC Publishers', 'Delhi', 300,19950715,'S77'),
    -> (4576,'JAVA','JAVA1','Guru Govind Publications', 'Delhi', 500,19970615,'S87'),
    -> (3433,'OOPS','OOPS1','Dave Publishers', 'Pune', 600,19991115,'S56'),
    -> (4655,'SAD','SAD1','Sajan Publications', 'Cochin', 700,19940815,'S76');
Query OK, 6 rows affected (0.01 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> select * from BOOKS;
+--------+-------+---------+--------------------------+--------------------+--------+--------------+---------+
| BookId | Title | TopicId | PublisherName            | PlaceofPublication | Price  | PurchaseDate | ShelfNo |
+--------+-------+---------+--------------------------+--------------------+--------+--------------+---------+
|   3433 | OOPS  | OOPS1   | Dave Publishers          | Pune               | 600.00 | 1999-11-15   | S56     |
|   4576 | JAVA  | JAVA1   | Guru Govind Publications | Delhi              | 500.00 | 1997-06-15   | S87     |
|   4655 | SAD   | SAD1    | Sajan Publications       | Cochin             | 700.00 | 1994-08-15   | S76     |
|   5645 | DBMS  | DB1     | Pearson Education        | Mumbai             | 655.00 | 1993-01-05   | S12     |
|   6565 | C     | C1      | TMH                      | Mumbai             | 840.00 | 1998-08-31   | S66     |
|   6567 | C++   | Cplus1  | ABC Publishers           | Delhi              | 300.00 | 1995-07-15   | S77     |
|   8293 | DBMS  | DB1     | Prentice Hall            | Mumbai             | 255.00 | 1995-01-01   | S11     |
+--------+-------+---------+--------------------------+--------------------+--------+--------------+---------+
7 rows in set (0.00 sec)

```

Note:
	The primary keys and other keys could be assumed if not mentioned.
	When inserting values try using all the 3 different ways to insert data into the table

e)	Write SQL queries to:
i.	Saurav Gupta is assigned a different project with id NITTS and he would work with C++ now. Update this change in the PROGRAMMER table.

```mysql
UPDATE PROGRAMMER set ProjId='NITTS', Language='C++' WHERE EmpNo=201;
```

```mysql
mysql> SELECT * FROM PROGRAMMER;
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
| EmpNo | LastName  | FirstName | HireDate   | ProjId | Language | TaskNo | Privilege    |
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
|   134 | Chaudhury | Supriyo   | 1995-07-15 | TIPPS  | C++      |     52 | Secret       |
|   201 | Gupta     | Saurav    | 1995-01-01 | NPR    | VB       |     52 | Secret       |
|   345 | John      | Peter     | 1999-11-15 | TIPPS  | Java     |     52 |              |
|   390 | Ghosh     | Pinky     | 1993-01-05 | KCW    | Java     |     11 | Top Secret   |
|   563 | Anderson  | Andy      | 1994-08-15 | NITTS  | C++      |     89 | confidential |
|   789 | Agarwal   | Praveen   | 1998-08-31 | Rnc    | VB       |     11 | Secret       |
|   896 | Jha       | Ranjit    | 1997-06-15 | KCW    | Java     |     10 | Top Secret   |
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
7 rows in set (0.00 sec)

mysql> UPDATE PROGRAMMER set ProjId='NITTS', Language='C++' WHERE EmpNo=201;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM PROGRAMMER;
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
| EmpNo | LastName  | FirstName | HireDate   | ProjId | Language | TaskNo | Privilege    |
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
|   134 | Chaudhury | Supriyo   | 1995-07-15 | TIPPS  | C++      |     52 | Secret       |
|   201 | Gupta     | Saurav    | 1995-01-01 | NITTS  | C++      |     52 | Secret       |
|   345 | John      | Peter     | 1999-11-15 | TIPPS  | Java     |     52 |              |
|   390 | Ghosh     | Pinky     | 1993-01-05 | KCW    | Java     |     11 | Top Secret   |
|   563 | Anderson  | Andy      | 1994-08-15 | NITTS  | C++      |     89 | confidential |
|   789 | Agarwal   | Praveen   | 1998-08-31 | Rnc    | VB       |     11 | Secret       |
|   896 | Jha       | Ranjit    | 1997-06-15 | KCW    | Java     |     10 | Top Secret   |
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
7 rows in set (0.00 sec)
```


i.	The books on DBMS are shifted to shelf with number S10. Please update this detail in BOOKS table.

```mysql
UPDATE BOOKS set ShelfNo='S10' WHERE Title='DBMS';
```

```mysql
mysql> SELECT * FROM BOOKS;
+--------+-------+---------+--------------------------+--------------------+--------+--------------+---------+
| BookId | Title | TopicId | PublisherName            | PlaceofPublication | Price  | PurchaseDate | ShelfNo |
+--------+-------+---------+--------------------------+--------------------+--------+--------------+---------+
|   3433 | OOPS  | OOPS1   | Dave Publishers          | Pune               | 600.00 | 1999-11-15   | S56     |
|   4576 | JAVA  | JAVA1   | Guru Govind Publications | Delhi              | 500.00 | 1997-06-15   | S87     |
|   4655 | SAD   | SAD1    | Sajan Publications       | Cochin             | 700.00 | 1994-08-15   | S76     |
|   5645 | DBMS  | DB1     | Pearson Education        | Mumbai             | 655.00 | 1993-01-05   | S12     |
|   6565 | C     | C1      | TMH                      | Mumbai             | 840.00 | 1998-08-31   | S66     |
|   6567 | C++   | Cplus1  | ABC Publishers           | Delhi              | 300.00 | 1995-07-15   | S77     |
|   8293 | DBMS  | DB1     | Prentice Hall            | Mumbai             | 255.00 | 1995-01-01   | S11     |
+--------+-------+---------+--------------------------+--------------------+--------+--------------+---------+
7 rows in set (0.00 sec)

mysql> UPDATE BOOKS set ShelfNo='S10' WHERE Title='DBMS';
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> SELECT * FROM BOOKS;
+--------+-------+---------+--------------------------+--------------------+--------+--------------+---------+
| BookId | Title | TopicId | PublisherName            | PlaceofPublication | Price  | PurchaseDate | ShelfNo |
+--------+-------+---------+--------------------------+--------------------+--------+--------------+---------+
|   3433 | OOPS  | OOPS1   | Dave Publishers          | Pune               | 600.00 | 1999-11-15   | S56     |
|   4576 | JAVA  | JAVA1   | Guru Govind Publications | Delhi              | 500.00 | 1997-06-15   | S87     |
|   4655 | SAD   | SAD1    | Sajan Publications       | Cochin             | 700.00 | 1994-08-15   | S76     |
|   5645 | DBMS  | DB1     | Pearson Education        | Mumbai             | 655.00 | 1993-01-05   | S10     |
|   6565 | C     | C1      | TMH                      | Mumbai             | 840.00 | 1998-08-31   | S66     |
|   6567 | C++   | Cplus1  | ABC Publishers           | Delhi              | 300.00 | 1995-07-15   | S77     |
|   8293 | DBMS  | DB1     | Prentice Hall            | Mumbai             | 255.00 | 1995-01-01   | S10     |
+--------+-------+---------+--------------------------+--------------------+--------+--------------+---------+
7 rows in set (0.00 sec)
```

ii.	Supriyo Chaudhury has resigned his job. Incorporate this change in the table PROGRAMMER.
```mysql
DELETE FROM PROGRAMMER WHERE FirstName='Supriyo' AND LastName='Chaudhury';
```

```mysql
mysql> SELECT * FROM PROGRAMMER;
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
| EmpNo | LastName  | FirstName | HireDate   | ProjId | Language | TaskNo | Privilege    |
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
|   134 | Chaudhury | Supriyo   | 1995-07-15 | TIPPS  | C++      |     52 | Secret       |
|   201 | Gupta     | Saurav    | 1995-01-01 | NITTS  | C++      |     52 | Secret       |
|   345 | John      | Peter     | 1999-11-15 | TIPPS  | Java     |     52 |              |
|   390 | Ghosh     | Pinky     | 1993-01-05 | KCW    | Java     |     11 | Top Secret   |
|   563 | Anderson  | Andy      | 1994-08-15 | NITTS  | C++      |     89 | confidential |
|   789 | Agarwal   | Praveen   | 1998-08-31 | Rnc    | VB       |     11 | Secret       |
|   896 | Jha       | Ranjit    | 1997-06-15 | KCW    | Java     |     10 | Top Secret   |
+-------+-----------+-----------+------------+--------+----------+--------+--------------+
7 rows in set (0.00 sec)

mysql> DELETE FROM PROGRAMMER WHERE FirstName='Supriyo' AND LastName='Chaudhury';
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM PROGRAMMER;
+-------+----------+-----------+------------+--------+----------+--------+--------------+
| EmpNo | LastName | FirstName | HireDate   | ProjId | Language | TaskNo | Privilege    |
+-------+----------+-----------+------------+--------+----------+--------+--------------+
|   201 | Gupta    | Saurav    | 1995-01-01 | NITTS  | C++      |     52 | Secret       |
|   345 | John     | Peter     | 1999-11-15 | TIPPS  | Java     |     52 |              |
|   390 | Ghosh    | Pinky     | 1993-01-05 | KCW    | Java     |     11 | Top Secret   |
|   563 | Anderson | Andy      | 1994-08-15 | NITTS  | C++      |     89 | confidential |
|   789 | Agarwal  | Praveen   | 1998-08-31 | Rnc    | VB       |     11 | Secret       |
|   896 | Jha      | Ranjit    | 1997-06-15 | KCW    | Java     |     10 | Top Secret   |
+-------+----------+-----------+------------+--------+----------+--------+--------------+
6 rows in set (0.00 sec)
```

iii.	A new column to state the nature of the climate with either of the value (rainy, cloudy, sunny, snow) is to be added in the WEATHER Table.

```mysql

mysql> desc WEATHER;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| City  | varchar(30) | NO   | PRI | NULL    |       |
| State | varchar(20) | YES  |     | NULL    |       |
| High  | int         | YES  |     | NULL    |       |
| Low   | int         | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)

mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+
| City       | State       | High | Low  |
+------------+-------------+------+------+
| Bangalore  | Karnataka   |   77 |   60 |
| Calcutta   | West Bengal |  105 |   90 |
| Mumbai     | Maharashtra |   88 |   69 |
| New Delhi  |             |   80 |   72 |
| Trivandrum | Kerala      |  101 |   92 |
+------------+-------------+------+------+
5 rows in set (0.00 sec)

mysql> ALTER TABLE WEATHER ADD Nature varchar(10) after Low;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc WEATHER;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| City   | varchar(30) | NO   | PRI | NULL    |       |
| State  | varchar(20) | YES  |     | NULL    |       |
| High   | int         | YES  |     | NULL    |       |
| Low    | int         | YES  |     | NULL    |       |
| Nature | varchar(10) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+--------+
| City       | State       | High | Low  | Nature |
+------------+-------------+------+------+--------+
| Bangalore  | Karnataka   |   77 |   60 | NULL   |
| Calcutta   | West Bengal |  105 |   90 | NULL   |
| Mumbai     | Maharashtra |   88 |   69 | NULL   |
| New Delhi  |             |   80 |   72 | NULL   |
| Trivandrum | Kerala      |  101 |   92 | NULL   |
+------------+-------------+------+------+--------+
5 rows in set (0.00 sec)

mysql> ALTER TABLE WEATHER ADD CONSTRAINT nature_chk CHECK(Nature='Rainy' OR Nature='Cloudy' OR Nature='Sunny' OR Nature='Snow');
Query OK, 5 rows affected (0.07 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+--------+
| City       | State       | High | Low  | Nature |
+------------+-------------+------+------+--------+
| Bangalore  | Karnataka   |   77 |   60 | NULL   |
| Calcutta   | West Bengal |  105 |   90 | NULL   |
| Mumbai     | Maharashtra |   88 |   69 | NULL   |
| New Delhi  |             |   80 |   72 | NULL   |
| Trivandrum | Kerala      |  101 |   92 | NULL   |
+------------+-------------+------+------+--------+
5 rows in set (0.00 sec)

mysql> desc WEATHER;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| City   | varchar(30) | NO   | PRI | NULL    |       |
| State  | varchar(20) | YES  |     | NULL    |       |
| High   | int         | YES  |     | NULL    |       |
| Low    | int         | YES  |     | NULL    |       |
| Nature | varchar(10) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> INSERT INTO WEATHER VALUES('Kasi','Tamilnadu',98,43,'Foggy');
ERROR 3819 (HY000): Check constraint 'nature_chk' is violated.
mysql> INSERT INTO WEATHER VALUES('Kasi','Tamilnadu',98,43,'');
ERROR 3819 (HY000): Check constraint 'nature_chk' is violated.
mysql> INSERT INTO WEATHER VALUES('Kasi','Tamilnadu',98,43);
ERROR 1136 (21S01): Column count doesnt match value count at row 1.

mysql> INSERT INTO WEATHER(City,State,High,Low) VALUES('Kasi','Tamilnadu',98,43);
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+--------+
| City       | State       | High | Low  | Nature |
+------------+-------------+------+------+--------+
| Bangalore  | Karnataka   |   77 |   60 | NULL   |
| Calcutta   | West Bengal |  105 |   90 | NULL   |
| Kasi       | Tamilnadu   |   98 |   43 | NULL   |
| Mumbai     | Maharashtra |   88 |   69 | NULL   |
| New Delhi  |             |   80 |   72 | NULL   |
| Trivandrum | Kerala      |  101 |   92 | NULL   |
+------------+-------------+------+------+--------+
6 rows in set (0.00 sec)

mysql> INSERT INTO WEATHER VALUES('Chennai','Tamilnadu',105,67,'Sunny');
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+--------+
| City       | State       | High | Low  | Nature |
+------------+-------------+------+------+--------+
| Bangalore  | Karnataka   |   77 |   60 | NULL   |
| Calcutta   | West Bengal |  105 |   90 | NULL   |
| Chennai    | Tamilnadu   |  105 |   67 | Sunny  |
| Kasi       | Tamilnadu   |   98 |   43 | NULL   |
| Mumbai     | Maharashtra |   88 |   69 | NULL   |
| New Delhi  |             |   80 |   72 | NULL   |
| Trivandrum | Kerala      |  101 |   92 | NULL   |
+------------+-------------+------+------+--------+
7 rows in set (0.00 sec)

mysql> ALTER TABLE WEATHER MODIFY Nature varchar(10) NOT NULL;
ERROR 1138 (22004): Invalid use of NULL value
mysql> ALTER TABLE WEATHER MODIFY Nature varchar(10) UNIQUE;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+--------+
| City       | State       | High | Low  | Nature |
+------------+-------------+------+------+--------+
| Bangalore  | Karnataka   |   77 |   60 | NULL   |
| Calcutta   | West Bengal |  105 |   90 | NULL   |
| Chennai    | Tamilnadu   |  105 |   67 | Sunny  |
| Kasi       | Tamilnadu   |   98 |   43 | NULL   |
| Mumbai     | Maharashtra |   88 |   69 | NULL   |
| New Delhi  |             |   80 |   72 | NULL   |
| Trivandrum | Kerala      |  101 |   92 | NULL   |
+------------+-------------+------+------+--------+
7 rows in set (0.00 sec)

mysql> INSERT INTO WEATHER VALUES('Trichi','Tamilnadu',105,67,'Sunny');;
ERROR 1062 (23000): Duplicate entry 'Sunny' for key 'weather.Nature'
ERROR:
No query specified

mysql> INSERT INTO WEATHER VALUES('Trichi','Tamilnadu',105,67,'Sunny');
ERROR 1062 (23000): Duplicate entry 'Sunny' for key 'weather.Nature'
mysql> desc Weather;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| City   | varchar(30) | NO   | PRI | NULL    |       |
| State  | varchar(20) | YES  |     | NULL    |       |
| High   | int         | YES  |     | NULL    |       |
| Low    | int         | YES  |     | NULL    |       |
| Nature | varchar(10) | YES  | UNI | NULL    |       |
+--------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> ALTER TABLE WEATHER MODIFY Nature varchar(10) NOT UNIQUE;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'UNIQUE' at line 1
mysql> ALTER TABLE WEATHER MODIFY Nature varchar(10);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc Weather;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| City   | varchar(30) | NO   | PRI | NULL    |       |
| State  | varchar(20) | YES  |     | NULL    |       |
| High   | int         | YES  |     | NULL    |       |
| Low    | int         | YES  |     | NULL    |       |
| Nature | varchar(10) | YES  | UNI | NULL    |       |
+--------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> SHOW INDEXES FROM WEATHER;
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table   | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| weather |          0 | PRIMARY  |            1 | City        | A         |           7 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| weather |          0 | Nature   |            1 | Nature      | A         |           2 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
+---------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
2 rows in set (0.01 sec)

mysql> ALTER TABLE WEATHER DROP CONSTRINT weather.Nature;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'weather.Nature' at line 1
mysql> ALTER TABLE WEATHER DROP weather.Nature;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '.Nature' at line 1
mysql> ALTER TABLE WEATHER DROP CONSTRAINT weather.Nature;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '.Nature' at line 1
mysql> ALTER TABLE WEATHER DROP CONSTRAINT 'Nature';
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ''Nature'' at line 1
mysql> ALTER TABLE WEATHER DROP CONSTRAINT 'weather.Nature';
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ''weather.Nature'' at line 1
mysql> ALTER TABLE WEATHER DROP INDEX 'weather.Nature';
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ''weather.Nature'' at line 1
mysql> ALTER TABLE WEATHER DROP INDEX 'Nature';
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ''Nature'' at line 1
mysql> ALTER TABLE WEATHER DROP INDEX Nature;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc Weather;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| City   | varchar(30) | NO   | PRI | NULL    |       |
| State  | varchar(20) | YES  |     | NULL    |       |
| High   | int         | YES  |     | NULL    |       |
| Low    | int         | YES  |     | NULL    |       |
| Nature | varchar(10) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+--------+
| City       | State       | High | Low  | Nature |
+------------+-------------+------+------+--------+
| Bangalore  | Karnataka   |   77 |   60 | NULL   |
| Calcutta   | West Bengal |  105 |   90 | NULL   |
| Chennai    | Tamilnadu   |  105 |   67 | Sunny  |
| Kasi       | Tamilnadu   |   98 |   43 | NULL   |
| Mumbai     | Maharashtra |   88 |   69 | NULL   |
| New Delhi  |             |   80 |   72 | NULL   |
| Trivandrum | Kerala      |  101 |   92 | NULL   |
+------------+-------------+------+------+--------+
7 rows in set (0.00 sec)

mysql> INSERT INTO WEATHER VALUES('Trichi','Tamilnadu',105,67,'Sunny');
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+--------+
| City       | State       | High | Low  | Nature |
+------------+-------------+------+------+--------+
| Bangalore  | Karnataka   |   77 |   60 | NULL   |
| Calcutta   | West Bengal |  105 |   90 | NULL   |
| Chennai    | Tamilnadu   |  105 |   67 | Sunny  |
| Kasi       | Tamilnadu   |   98 |   43 | NULL   |
| Mumbai     | Maharashtra |   88 |   69 | NULL   |
| New Delhi  |             |   80 |   72 | NULL   |
| Trichi     | Tamilnadu   |  105 |   67 | Sunny  |
| Trivandrum | Kerala      |  101 |   92 | NULL   |
+------------+-------------+------+------+--------+
8 rows in set (0.00 sec)

```

iv.	Delete the table WEATHER from database.

```mysql
mysql> SELECT * FROM WEATHER;
+------------+-------------+------+------+--------+
| City       | State       | High | Low  | Nature |
+------------+-------------+------+------+--------+
| Bangalore  | Karnataka   |   77 |   60 | NULL   |
| Calcutta   | West Bengal |  105 |   90 | NULL   |
| Chennai    | Tamilnadu   |  105 |   67 | Sunny  |
| Kasi       | Tamilnadu   |   98 |   43 | NULL   |
| Mumbai     | Maharashtra |   88 |   69 | NULL   |
| New Delhi  |             |   80 |   72 | NULL   |
| Trichi     | Tamilnadu   |  105 |   67 | Sunny  |
| Trivandrum | Kerala      |  101 |   92 | NULL   |
+------------+-------------+------+------+--------+
8 rows in set (0.00 sec)

mysql> DELETE FROM WEATHER;
Query OK, 8 rows affected (0.01 sec)

mysql> SELECT * FROM WEATHER;
Empty set (0.00 sec)

mysql> SHOW TABLES;
+---------------------+
| Tables_in_javabatch |
+---------------------+
| books               |
| customer            |
| customer1           |
| customer2           |
| customer3           |
| programmer          |
| weather             |
+---------------------+
7 rows in set (0.00 sec)

mysql> desc weather;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| City   | varchar(30) | NO   | PRI | NULL    |       |
| State  | varchar(20) | YES  |     | NULL    |       |
| High   | int         | YES  |     | NULL    |       |
| Low    | int         | YES  |     | NULL    |       |
| Nature | varchar(10) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> DROP TABLE WEATHER;
Query OK, 0 rows affected (0.02 sec)

mysql> SHOW TABLES;
+---------------------+
| Tables_in_javabatch |
+---------------------+
| books               |
| customer            |
| customer1           |
| customer2           |
| customer3           |
| programmer          |
+---------------------+
6 rows in set (0.00 sec)
```
