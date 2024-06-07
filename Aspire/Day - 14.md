
*Date : 05.17.2024*


# SQL Statements
1. DDL
2. DML
3. DQL - Data Query Language

## DQL - Data Query Language
### 1. select - used to fetch the data from table
```mysql
>select * from suppliers; -- select all rows and columns from table

>select supid, supname from suppliers; -- select all rows but only specific column

>select * from suppliers where supid>10; -- select all columns but only specific rows

>select supid,supname from suppliers where supid>10;  -- select specific rows as well as specific columns

>select orders.orderid,suppliers.supname from orders,suppliers where orders.supid=suppliers.supid; -- select data from multiple tables

>select o.orderid,s.supname from orders o,suppliers s where o.supid=s.supid;
- create an alias for the table to select data from multiple tables

>select distinct city from customers;  - To avoid duplicates values  //REMEMBER

>select * from suppliers where city='Chennai' and type='PC Manufacture';

>select * from suppliers where city='Chennai' or type='PC Manufacture';
```

IS NULL, IS NOT NULL
```mysql
>select * from emp where dept is null;
>select * from emp where dept is not null;
```

LIKE, NOT LIKE - Pattern matching operator
    - used to fetch the data based on some pattern - applied **only for varchar**
    - 2 wild card characters
           **% - everything(anything)**
           **_ - single value**
```mysql
>select * from suppliers where supname like 'R%'; - select all suppliers whose name should start with R

>select * from suppliers where supname like '%the%';  //weather, feather,father

>select * from suppliers where supname not like 'S%';
>select * from suppliers where supname like 'Sm_th';
>select * from orders where orderid like '1000_';
```

supname
Hello%
HelloHo
HelloBye
Hello%
```mysql
>select * from suppliers where supname like 'Hello%'; - select all 4 rows
```

If we want to include %,_ at time of pattern matching then we have to use escape sequences
```mysql
>select * from suppliers where supname like 'Hello!%' ESCAPE '!'; - select 2 rows
```

Gana
Girl
Giri
G%
```mysql
>select * from suppliers where supname like 'G%'; - select all 4 rows

>select * from suppliers where supname like 'G&%' ESCAPE '&'; - select 1 row
```

Hello
Hello\%%
Hi\%
```mysql
>select * from suppliers where supname like 'H%'; - select all 3 rows

>select * from suppliers where supname like 'H%!%' ESCAPE '!'; - select 2 rows

>select * from suppliers where supname like 'H\%'; 
```

IN, NOT IN - **used instead of multiple OR operator**
```mysql
>select * from suppliers where supname='HP' or supname='HCL' or supname='TCS';

>select * from suppliers where supname in('HP','HCL','TCS');

>select * from orders where orderid not in(1000,1003,1005,1007);
```

BETWEEN, NOT BETWEEN - **Range operator** - includes the ranges 1000 and 2000.
```mysql
>select * from suppliers where supid between 1000 and 2000;

>select * from suppliers where supid>=1000 and supid<=2000;
```

Set operator - UNION, UNION ALL, INTERSECT, MINUS
```mysql
>select supid from supplier
     union
select supid from orders;
     -- select both supid from supplier and orders table, if there is any duplication it will be considered only once

>select supid from supplier
     union all
select supid from orders;
     -- select both supid from supplier and orders table, and print everything with duplication 

>select supid from supplier
     intersect
select supid from orders;
     -- select only common supid from supplier and orders table

>select supid from supplier
     minus
select supid from orders;
     -- remove supid from supplier table that is present in order table

```


## SQL Functions
### 1. Numeric functions - apply these function to numbers

a. abs(n) - return absolute value
```mysql
>select abs(5);  5
>select abs(-5); 5
```

b. ceil(n) - largest number >= n
```mysql
>select ceil(9.5);  10
>select ceil(-9.5); -9
```

c. floor(n) - nearest number <= n
```mysql
>select floor(9.5); 9
>select floor(-9.5); -10
```

d. mod(m,n) - mod(7,2) - 1
e. power(m,n) - power(3,2) - 9
f. sqrt(n)
g. exp(n)
h. log(n)
i. sin(n)
j. cos(n)
k. tan(n)
l. round(n) - round to nearest decimal values

```mysql
>select round(125.07); 125 
>select round(125.67); 126
>select round(125.67,1); 125.7
>select round(125.11,1); 125.1
>select round(125.67,2); 125.67
>select round(125.678,2); 125.68
```

Important
```mysql
>select round(125.67,-1); 130          120   125   130
    -- -1 represents 10's, if the value is greater than mid value it returns higher value otherwise it returns lower value 
>select round(221.67,-1); 220     220  225  230  
>select round(221.67,-2); 200     200  250  300
    -- -2 represents 100's, if the value is greater than mid value it returns higher value otherwise it returns lower value 
>select round(673.24,-2); 700    600   650  700
>select round(3673.12,-3); 4000  3000  3500  4000
    -- -3 represents 1000's, if the value is greater than mid value it returns higher value otherwise it returns lower value 

>select round(salary,-1) from empl;
```

m. truncate(n,value)

```mysql
>select truncate(125.56);  error  -- Very Imp, compulsory should have 2 arguments
>select truncate(123.13,1); 123.1
>select truncate(123.67,1); 123.6
>select truncate(123.678,2); 123.67
>select truncate(123.67,-1); 120
   -- -1 represents 10's, if the value is greater or lesser than mid value it always return only lower value 
>select truncate(999.99,-2);  900
```

### 2. Character function - apply on varchar

1. ascii(n) - return ascii value of left most char
```mysql
>select ascii('a');  97
>select ascii('Bad'); 66 -- ascii(B)
```

2. char_length(char)
   character_length(char)
   length(char)
      - used to length of the string

```mysql
>select char_length('hello'); 5
>select character_length('hello'); 5
>select length('hello'); 5
```

3. `concat()/**space operator**` - concatenate two or more string

```mysql
>select concat('The answer is','24');  The answer is 24
>select concat('The answer is','10+10');  The answer is 10+10
>select concat('The answer is',10+10);  The answer is 20
>select 'The answer is' '24' ;  The answer is 24 -- Space operator
>select concat('The answer is',null);  null
```

4. `concat_ws(joing term, terms to join)` - concatenate two or more expr and adds a separator between each concatened expr

```mysql
>select concat_ws('+','a','b','c'); a+b+c
>select concat_ws('xyz','a','b','c'); axyzbxyzc
>select concat_ws(null,'a','b','c');  null

> select concat_ws('ded','bed','ged'); 
+------------------------------+
| concat_ws('ded','bed','ged') |
+------------------------------+
| beddedged                    |
+------------------------------+
1 row in set (0.00 sec)
```

5. `field(value,list)` - return position of a value in list of values

```mysql
>select field('b','a','b','c','d','e');  2
>select field('15','10','20','15','30'); 3
>select field('c','a','b');  0 -- since the value not in list
>select field(null,'a','b'); null
```

6. `find_in_set(value, comma seperated string)` - return the position of a value in a comma **separated string**

```mysql
>select find_in_set('b','a,b,c,d,e');  2
>select find_in_set('2','3,1,2,3,4'); 3
```

7. `format(vlaue, decimals) `- **used to format number with comma and rounding to nearest decimal value**

```mysql
>select format('123457.67889',2); 1,23,457.68
```

8. `instr()` - return location of substring in a string

```mysql
>select instr('hello','h');  1
>select instr('hello','e');  2
>select instr('hello','a'); 0
>select instr('hello','l'); 3
```

9. lower()
   lcase()
     - convert string to lowercase

10. left() - extract leftmost char of string

```mysql
>select left('hello',1); h
>select left('hello',4); hell
>select left('hello',10); hello
```

11. right() - extract rightmost char of string

```mysql
>select right('hello',1); o
>select right('hello',4); ello
>select right('hello',10); hello
```

12. locate() - return location of **first occurence of substring** in a string

```mysql
>select locate('h','hello'); 1
>select locate('l','hello'); 3
>select locate('l','hello',3);  4  -- after 3rd position, first occurence of l
>select locate('l','heelo',3); 4
>select locate('e','technology internet'); 2
>select locate('e','technology internet',3); 15
>select locate('a','technology internet',3); 0
```

13. lpad(char1,n,char2) - char1 is left padded with char2 of length n

```mysql
>select lpad('world',10,'hello'); helloworld
>select lpad('world',11,'hello');  hellohworld
>select lpad('world',12,'hello');  helloheworld
>select lpad('world',9,'hello');  hellworld
>select lpad('world',4,'hello');  worl
```

14. rpad(char1,n,char2) - char1 is right padded with char2 of length n

```mysql
>select rpad('world',10,'hello'); worldhello
>select rpad('world',11,'hello'); worldhelloh
>select rpad('world',12,'hello');  worldhellohe
>select rpad('world',9,'hello');  worldhell
>select rpad('world',4,'hello');  worl
```

15. ltrim() - remove all spaces on left side

```mysql
>select ltrim(' HELLO '); HELLO_
>select ltrim(' HELLO WORLD '); HELLO WORLD_
```

16. rtrim() - remove all spaces on right side

```mysql
>select rtrim(' HELLO '); _HELLO
>select rtrim(' HELLO WORLD '); _HELLO WORLD
```

17. trim() - trim both leading and trailing space

```mysql
>select trim(leading from ' hello '); hello_
>select trim(trailing from ' hello '); _hello
>select trim(both from ' hello '); hello
>select trim(leading '0' from '000123000'); 123000
>select trim(trailing '1' from '111hello111'); 111hello
>select trim(both '0' from '000123000'); 123
```

18. ucase()
    upper()
      - convert string to uppercase

19. mid() - used to extract substring from string
```mysql
>select mid('technology',5,2); no
>select mid('technology',1,4); tech
>select mid('technology',-7,4); hnol  -- minus means start from behind
>select mid('technology',-3,3); ogy
```

20. substr() - used to extract substring from string, can be used instead of mid
```mysql
>select substr('technology',5); nology -- see
>select substr('technology.com',1,4); tech
>select substr('technology.com',-3,3); com
>select substr('technology.com' from 1 for 4); tech
```

21. substring() - used to extract substring from string
```mysql
>select substring('technology',5); nology  -- see
>select substring('technology.com',1,4); tech
>select substring('technology.com',-3,3); com
>select substring('technology.com' from 1 for 4); tech
```

22. `substring_index('string','delimiter','for') `- return substring from string before number of occurence of delimiter

```mysql
>select substring_index('www.technology.com','.',1);  www
>select substring_index('www.technology.com','.',2);  www.technology
>select substring_index('www.technology.com','.',-1); com
```

23. strcmp() - compare two strings

```mysql
>select strcmp('hello','hello'); 0
>select strcmp('car','hello'); -1
>select strcmp('hello','car');  1
```

24. space() - return string with specified number of space
```mysql
>select space(3); '   '
```

24. reverse() - reverse the string
```mysql
>select reverse('hello'); olleh
```

25. replace() - replace the string
```mysql
>select replace('abc abc','a','B');  Bbc Bbc
```

### 3. Date function 

### 4. Aggregate/Group function
- used to group the values
- It will **ignore null** values at time of grouping
- `sum(), avg(), count(), min(), max(), stddev(), median(), mode()`
- For **date** datatype we can apply only `max(), min(), count()`

Employee table
empid(int)  name(varchar)  gender(varchar)  salary(double)  dob(date) - we have totally 50 rows

What we provide in the select list that will be coming as column name
```mysql
>select count(*) from employee;
count(*)
-----
  50
   
>select count(gender) from employee;
count(gender)
------------
50

>select count(distinct gender) from employee; 
count(distinct gender) 
--------------------------
  3
```

Create alias for the column
```mysql
>select count(*) as "Number of Employees" from employee; -- " " are required for ALias with spaces
Number of Employees
--------------------
50

>select count(*)  "Number of Employees" from employee; -- without as quote
Number of Employees
--------------------
50   

>select count(*) 'NumberofEmployees' from employee;  -- '' without spaces
NumberofEmployees
--------------------
50

>select sum(salary) as "Total Salary" from employee;
>select max(dob) from employee;
>select min(dob) from employee;
>select avg(salary) from employee;
```

#### Order by
order by clause
    - used for sorting purpose only at time of displaying
    - It should be always present in the **last of select stmt**
	`select - from - where - group by - having - order by`
    - By **default sorted in ascending order**
    - column index represent the column index from select list and not from table
    - If we sort based on multiple columns, then by default it will sorted **only on first column**, in the first column if there is **any duplication** for those state column alone, it will be sorted **based on second column city in desc order**

```mysql
>select supplier_city,supplier_state from supplier where supplier_name='IBM' order by supplier_city;  -- by default asc order

>select supplier_city,supplier_state from supplier where supplier_name='IBM' order by supplier_city asc; -- explicit asc order

>select supplier_city,supplier_state from supplier where supplier_name='IBM' order by supplier_city desc; -- explicit desc order
```

Supplier table
supid   supname   supplier_city  supplier_name  address

```mysql
>select supplier_city,supplier_state from supplier where supplier_name='IBM' order by 2;  -- column index, represent column index from select list and not from table
```

Supplier
supplier_city   supplier_state
Chennai          Tamilnadu
Allepey          Kerela
Coimbatore       Tamilnadu
Mumbai           Maharastra
Pune             Maharastra

```mysql
>select supplier_city,supplier_state from supplier where supplier_name='IBM' order by supplier_state asc,supplier_city desc;
```

supplier_state    supplier_city
Kerela            Allepey
Maharastra        Pune
Maharastra        Mumbai
Tamilnadu         Coimbatore
Tamilnadu         Chennai

#### Group by
group by clause
    - used to group the values in a table based on some aggregate function

Employee table
empid     ename     dept      salary
1           A        HR       4000
2           B        IT       5000
3           C        HR       6000
4           D        Sales    5000
5           E        IT       5000
6           F        HR       4000
7           G        Sales    4000

We want to calculate total sum of salary
```mysql
>select sum(salary) from employee;
```

We want to calculate total sum of salary in each dept
```mysql
>select dept, sum(salary) from employee group by dept order by dept;
```

dept     sum(salary)
HR        14000
IT        10000
Sales     9000

#### having clause
- used to exclude the result from group by clause

```mysql
>select dept, sum(salary) from employee group by dept having sum(salary)>12000 order by dept;
```

dept     sum(salary)
HR        14000

## 4. TCL statement - Transaction control Language 
- Transaction is a small unit of work that is performed against the database (ie) while DML operations 
- 3 stmt

1. commit - used to commit the transaction permantely in db
2. rollback - undo all previous transaction before committing

insert;
commit;
insert;
insert;
update;
rollback;

3. savepoint - used to undo particular transaction
     
insert;
delete;
create;  - when we call DDL stmt inbetween then autocommit  will take place

```mysql
mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |   20 |
| 103 | Raj  | NULL |
+-----+------+------+
3 rows in set (0.00 sec)

mysql> START TRANSACTION;
Query OK, 0 rows affected (0.00 sec)

mysql> insert into customer values(104,'Tim',34);
Query OK, 1 row affected (0.00 sec)

mysql> update customer set age=32 where id=103;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> commit;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |   20 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
+-----+------+------+
4 rows in set (0.00 sec)

mysql> insert into customer values(105,'Jim',24);
Query OK, 1 row affected (0.01 sec)

mysql> delete from customer where id=105;
Query OK, 1 row affected (0.01 sec)

mysql> create table cust1(id int, name varchar(20));
Query OK, 0 rows affected (0.08 sec)

mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |   20 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
+-----+------+------+
4 rows in set (0.00 sec)

mysql> insert into customer values(105,'Jim',24);
Query OK, 1 row affected (0.01 sec)

mysql> insert into customer values(106,'Jam',25);
Query OK, 1 row affected (0.01 sec)

mysql> update customer set age=44 where id=106;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |   20 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
| 105 | Jim  |   24 |
| 106 | Jam  |   44 |
+-----+------+------+
6 rows in set (0.00 sec)

mysql> rollback;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |   20 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
| 105 | Jim  |   24 |
| 106 | Jam  |   44 |
+-----+------+------+
6 rows in set (0.00 sec)

mysql> START TRANSACTION;
Query OK, 0 rows affected (0.00 sec)

mysql> insert into customer values(107,'Jim',24);
Query OK, 1 row affected (0.00 sec)

mysql> delete from customer where id=106;
Query OK, 1 row affected (0.00 sec)

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |   20 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
| 105 | Jim  |   24 |
| 107 | Jim  |   24 |
+-----+------+------+
6 rows in set (0.00 sec)

mysql> rollback;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |   20 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
| 105 | Jim  |   24 |
| 106 | Jam  |   44 |
+-----+------+------+
6 rows in set (0.00 sec)

mysql> START TRANSACTION;
Query OK, 0 rows affected (0.00 sec)

mysql> savepoint initial;
Query OK, 0 rows affected (0.00 sec)

mysql> insert into customer values(108,'Tom',23);
Query OK, 1 row affected (0.00 sec)

mysql> savepoint addition;
Query OK, 0 rows affected (0.00 sec)

mysql> update customer set age=100 where id=101;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |  100 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
| 105 | Jim  |   24 |
| 106 | Jam  |   44 |
| 108 | Tom  |   23 |
+-----+------+------+
7 rows in set (0.00 sec)

mysql> savepoint updation;
Query OK, 0 rows affected (0.00 sec)

mysql> delete from customer where id=101;
Query OK, 1 row affected (0.00 sec)

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
| 105 | Jim  |   24 |
| 106 | Jam  |   44 |
| 108 | Tom  |   23 |
+-----+------+------+
6 rows in set (0.00 sec)

mysql> savepoint deletion;
Query OK, 0 rows affected (0.00 sec)

mysql> rollback to updation;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |  100 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
| 105 | Jim  |   24 |
| 106 | Jam  |   44 |
| 108 | Tom  |   23 |
+-----+------+------+
7 rows in set (0.00 sec)

mysql> rollback to addition;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from customer;
+-----+------+------+
| id  | name | age  |
+-----+------+------+
| 100 | Ram  |   23 |
| 101 | Sam  |   20 |
| 103 | Raj  |   32 |
| 104 | Tim  |   34 |
| 105 | Jim  |   24 |
| 106 | Jam  |   44 |
| 108 | Tom  |   23 |
+-----+------+------+
7 rows in set (0.00 sec)

mysql> commit;
Query OK, 0 rows affected (0.01 sec)
```

5. DCL - Data Control Language
       - Grant - grant privilege to user
       - Revoke - removing privilege from user

```mysql
>grant delete,update on employee to system;
>revoke delete,update on employee to system;
```
