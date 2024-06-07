
*Date : 05.14.2024*

## File processing system
- we store all data inside the files 

Drawbacks
1. Data redundancy - duplication of data 
2. Data isolation - same data is scattered across multiple system
3. Only particular format of data can be stored inside the file
4. No security
5. No backup and recovery of data 
6. Integrity constraints are buried inside programming language 
7. Only single user can access the file

## Database system
- set of logically related data - database 
- set of programs to access those data - DBMS/RDBMS 

| DBMS                                                                                           | RDBMS                                                                                                       |
| ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| 1. No relationship between tables we have only primary key                                     | 1. We can relate two tables using foreign key                                                               |
| 2. Data is stored in flat file inside the system                                               | 2. Data is stored inside the tables                                                                         |
| 3. Only single user can access the data at a time                    <br>eg: MS Access, Foxpro | 3. Multiple user can access the data at a time<br>eg: Oracle, mysql, sql server, db2, sybase, postgress sql |


## Data models
 - semantic representation of data and their relationship

1. Hierarchical model
2. Network model
3. ER model - Entity Relationship diagram
4. Relational model - represent the data in the form of table
      Table will contains rows(records/tuples) and columns(attributes/fields)
5. Semi structured model - represent data in xml files

## DBMS/RDBMS 
   - set of programs to access those data - 2 types
1. SQL - Structured Query Language
2. PLSQL - Procedural Language and Structured Query Language

# SQL
   - It is a English like syntax to process the data in database

## Types of `keys` in SQL

1. Super key - any combination of columns that uniquely fetch the value from database 

Consider we have Employee table 
empid, ename, address, salary, dept


*REFER*
ename, address, dept - super key (3 columns can uniquely fetch the record)
empid, salary - candidate key(minimal of super key)
empid - primary key - any one of candidate key is selected as primary key
salary - alternate key


## Integrity constraints in SQL - 5 types

1. Entity integrity constraint
      - Entity means table - constraints that are applied directly on the table 
      - 2 types
	1. `Primary key` - no duplication, no null values
	2. `Unique key` - no duplication, one null value will be allowed 

2. Domain integrity constraint
      - Domain is permitted value for the column
      - constraint that is applied to value of the column
      - 2 types
	  1. `NOT NULL` 
	  2. `CHECK` - In a banking app record, applying a `CHECK` stating each account must have minimum of 500/- balance.

3. Referential Integrity constraint
     - we can refer one table with another table using foreign key
     - One tables PK(`Primary Key`) only will be acting as FK(`Foreing Key`) in another table, so first we have to create PK table then only we have to create FK table
     - Foreign key contains duplicate values and also null values
     - FK column should contain only the value that are present in PK column
     - Whenever there is one to many, many to one, many to many
     - First we have to delete PK table then we have to delete FK table

e.g. :  one person places many orders - one to many

Person
```
perid(pk)	pname	ordername
 1		A	Coffee
 2		B	Tea
 3		C	Juice
 4		D	Biscuits
 5		E	Cola
 1		A	Cakes
```

The above table is *incorrect* as the `perid(pk)` contains duplicate values, so above is invalid. SO consider the below.

Person
```
perid(pk)  pname  
 1          A       
 2          B       
 3          C      
 4          D       
 5          E      
```


Orders
```
orderid(pk)    ordername     perid(FK)
  100           Coffee         1
  101           Tea            2
  102           Juice          3
  103           Biscuits       4
  104           Sandwich       5 (6 is invalid as it does not exist in the PK column)
  106           Cakes          1
  107           Burger         -(null is allowed for FK)
```

4. Default constraint
       - By default if we didn't provide any value for the column, irrespective of the datatype always it will contain null value
       - But we don't want to have null value, instead we want to provide some default value, then we use `default` constraint

5. NULL constraint


## Composite primary key
 - If table contains *more than one column as primary key* where its combination should be unique

```cmd
A(PK)     B(PK)       C
1          1          1   11
2          1              21 - Combination should be uniqe
1          4          3   14 
1          2          4   12
```

Note
1. By default if we didn't provide any value for the column, irrespective of the datatype always it will contain `null` value
2. SQL is a case sensitive - tablename, columnname are *not case sensitive*, but the values stored inside the tables are *case sensitive*
   'ram'!='RAM'

## SQL datatypes
1. Numeric datatype - store any numbers `+ve` or `-ve` 

   - `numeric(p,q)`  p=total width, q=precision after decimal point
	   `numeric(5,2`) - 123.45
   - `numeric(p)` - `numeric(5)` - 12345
   - `int/integer`
   - `tinyint` -128 to 127
   - `smallint` -32768 to 32767
   - `mediumint` -8388608  to 8388607
   - `bigint` -9223372036854775808 to 9223372036854775807 - Phone numbers
   - `dec(p,q)/decimal(p,q)/fixed(p,q)`
   - `float`
   - `double`

2. Character datatype 
   - `char(n)` - fixed length of char
             char(10) - 'Ram'
   - `varchar(n) `- variable length of char , good
             varchar(10) - 'Ram'

3. Date datatype
       - `date` - only `date(yyyy-MM-dd)` - Only format
       - `datetime` - store both date and time `(yyyy-MM-dd hh:mm:ss)`
       - `Timestamp` - both date and time `(yyyyMMddhhmmss)`

4. LOB datatype - Large Object datatype
   - `BLOB`(Binary Large Object) - used to store images, audio or video file
   - `CLOB`(Character Large Object)- used to store very long string , description, remarks in Student table. JSON will be stored separately as a .JSON file.

## SQL Operators

1. `+,-,*,/,>,<,>=,<=`
2. ALL
3. ANY
4. AND
5. OR
6. IN, NOT IN
7. LIKE, NOT LIKE - Pattern matching operator
8. BETWEEN, NOT BETWEEN
9. IS NULL, IS NOT NULL
10. EXISTS, NOT EXISTS
11. UNION, UNION ALL, INTERSECT, MINUS - Set operator

```MySQL
mysql> show databases;    -- to view all databases

mysql> create database javabatch;  -- create new database 
Query OK, 1 row affected (0.02 sec)

mysql> use javabatch;   - use our database called javabatch
Database changed

mysql> show tables;   -- to view all tables in db
Empty set (0.01 sec)

mysql>drop database db1;   --to delete the db
```



# SQL statement

## 1. DDL statement - Data Definition Language - 4 stmt
                - `create, alter, drop, truncate`


### a. **create** - used to create a new table

```MySQL
mysql> create table customer(id int,name varchar(20),age int);
Query OK, 0 rows affected (0.08 sec)

mysql> desc customer;   -- to view structure of the table
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| id    | int         | YES  |     | NULL    |       |
| name  | varchar(20) | YES  |     | NULL    |       |
| age   | int         | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

-- Its always a good practice to create table with atleast 1 PK
-- By default the values will have NULL constraint, we can define otherwise(NOT NULL, default)

mysql> create table customer1(id int primary key,name varchar(20) NOT NULL, age int default 20);
Query OK, 0 rows affected (0.06 sec)

-- There is an issue with the above method that you need to be 100% sure about the primary key, in future if you change your mind you need to drop the whole column. Data will also be lost.
-- So it is better to define the PK in the below method so only the primary key contrain can be droped using alter statement.

mysql> create table customer2(id int,name varchar(20) NOT NULL, age int default 20, constraint cust_pk primary key(id));
Query OK, 0 rows affected (0.06 sec)

-- Its difficult to maintain the id data manually, there's a chance of arising duplicates, so it is a best practice to make it AUTO_INCREMENT.
-- We can define AUTO_INCREMENT=50; so the id will start at a particular value and increment by 1.
-- Only int can be AUTO_INCREMENTED, ay other random id generation logic need to be handled by JAVA logic.


mysql> create table customer3(id int AUTO_INCREMENT,name varchar(20) NOT NULL, age int default 20, constraint cust_pk1 primary key(id));
Query OK, 0 rows affected (0.07 sec)
-- contrinat name should be unique

mysql> alter table customer3 AUTO_INCREMENT=50;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

-- Create composite primary key
mysql> create table customer4(sno int,id int ,name varchar(20) NOT NULL, age int, constraint cust_pk2 primary key(sno,id));
Query OK, 0 rows affected (0.06 sec) 

-- Create FK
mysql> create table department(deptid int primary key,dname varchar(20));
Query OK, 0 rows affected (0.06 sec)

mysql> create table emp(empid int primary key,ename varchar(20),salary double, did int,foreign key(did) references department(deptid));
Query OK, 0 rows affected (0.07 sec)

-- The below method is safe and future proof.
mysql> create table emp1(empid int,ename varchar(20),salary double, did int,constraint emp_pk primary key(empid),constraint emp_fk foreign key(did) references department(deptid));
Query OK, 0 rows affected (0.07 sec)

-- Create Unique key, since it can accept a null value
mysql> create table empl(sapid int primary key, projectid int unique, name varchar(20));
Query OK, 0 rows affected (0.06 sec)

-- Create a check constraint
mysql> create table account(accid int primary key,name varchar(20),balance int, constraint acc_chk check(balance>500));
Query OK, 0 rows affected (0.06 sec)

-- create table from another table where we copy both data and structure 
mysql> create table customer5 as select * from customer4;
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> create table customer6 as select id,name from customer4;
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

-- copy only structure from one table and create another table, should provide some wrong condition. eg:1=4
mysql> create table customer7 as select * from customer4 where 1=4;
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

### b. **alter** - to alter table properties and values

1. To rename table name

```mysql
mysql> alter table customer7 rename to cust7;
Query OK, 0 rows affected (0.03 sec)
```

2. To rename column name in table
```mysql
mysql> alter table cust7 rename column age to custage;
Query OK, 0 rows affected (0.02 sec)
```

3. To add new column to existing table
```mysql
mysql> alter table cust7 add address varchar(20);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table cust7 add city varchar(20),add state varchar(20);
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc cust7;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| sno     | int         | NO   |     | NULL    |       |
| id      | int         | NO   |     | NULL    |       |
| name    | varchar(20) | NO   |     | NULL    |       |
| custage | int         | YES  |     | NULL    |       |
| address | varchar(20) | YES  |     | NULL    |       |
| city    | varchar(20) | YES  |     | NULL    |       |
| state   | varchar(20) | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
7 rows in set (0.00 sec)

mysql> alter table cust7 add email varchar(20) after custage;
Query OK, 0 rows affected (0.12 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc cust7;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| sno     | int         | NO   |     | NULL    |       |
| id      | int         | NO   |     | NULL    |       |
| name    | varchar(20) | NO   |     | NULL    |       |
| custage | int         | YES  |     | NULL    |       |
| email   | varchar(20) | YES  |     | NULL    |       |
| address | varchar(20) | YES  |     | NULL    |       |
| city    | varchar(20) | YES  |     | NULL    |       |
| state   | varchar(20) | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
8 rows in set (0.00 sec)
```


4. Modify only datatype of existing column

```mysql
mysql> alter table cust7 modify address varchar(50) NOT NULL;
Query OK, 0 rows affected (0.09 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table cust7 modify city varchar(50) NOT NULL,modify state varchar(50) NOT NULL;
Query OK, 0 rows affected (0.08 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc cust7;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| sno     | int         | NO   |     | NULL    |       |
| id      | int         | NO   |     | NULL    |       |
| name    | varchar(20) | NO   |     | NULL    |       |
| custage | int         | YES  |     | NULL    |       |
| email   | varchar(20) | YES  |     | NULL    |       |
| address | varchar(50) | NO   |     | NULL    |       |
| city    | varchar(50) | NO   |     | NULL    |       |
| state   | varchar(50) | NO   |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
8 rows in set (0.00 sec)

```

5. To drop existing column from table 

```mysql
mysql> alter table cust7 drop column email;
Query OK, 0 rows affected (0.09 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

6. To add constraint to existing table after creating
```mysql
mysql> alter table customer add constraint c_pk primary key(id);
Query OK, 0 rows affected (0.10 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

7. To drop the constraint
```mysql
mysql> alter table customer drop primary key;
Query OK, 0 rows affected (0.11 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table emp1 drop foreign key emp_fk;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table account drop check acc_chk;
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

### c. **drop** 
  - drop the data as well as the structure of the table

```mysql
mysql> drop table account;
Query OK, 0 rows affected (0.03 sec)

mysql> drop table customer1,customer2;
Query OK, 0 rows affected (0.06 sec)

mysql> drop table if exists account;
Query OK, 0 rows affected, 1 warning (0.00 sec)
```

### d. **truncate**
  - drop the data but the structure will be present, we cannot rollback
```mysql
mysql> truncate table cust4;
```


## 2. DML - Data Manipulation Language - 3 stmts
       - insert, update, delete

### a. **insert** - used to insert new row into a table

- insert values to all columns
```mysql
mysql> insert into cust7 values(1,100,'Ram',23,'ABC Street','Chennai','Tamilnadu');
Query OK, 1 row affected (0.01 sec)

mysql> insert into cust7 values(2,101,'Sam',20,'XYZ Street','Bangalore','Karnataka');
Query OK, 1 row affected (0.01 sec)
```

- insert only to particular column
```mysql
mysql> insert into cust7(sno,id,name,address) values(3,103,'Raj','PQR Street');
Query OK, 1 row affected (0.01 sec)

mysql> select * from cust7;
+-----+-----+------+---------+------------+-----------+-----------+
| sno | id  | name | custage | address    | city      | state     |
+-----+-----+------+---------+------------+-----------+-----------+
|   1 | 100 | Ram  |      23 | ABC Street | Chennai   | Tamilnadu |
|   2 | 101 | Sam  |      20 | XYZ Street | Bangalore | Karnataka |
|   3 | 103 | Raj  |    NULL | PQR Street | NULL      | NULL      |
+-----+-----+------+---------+------------+-----------+-----------+
3 rows in set (0.00 sec)
```


- insert data from another table, make sure both table should have *same number of column and same column datatype*
```mysql
-- To copy only the structure of the table
mysql> create table cust8 as select * from cust7 where 1=2;

mysql> insert into cust8 select * from cust7;
Query OK, 3 rows affected (0.01 sec)
Records: 3  Duplicates: 0  Warnings: 0
```

- with single insert query if we want to insert multiple rows
```mysql
mysql> insert into cust8(sno, id, name, custage, address, city, state) values
    -> (4,104,'Ramu',28,'MNO Street','Cochin','Kerela'),
    -> (5,105,'Tim',27,'FTG Street','Mumbai','Maharastra');
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0
```

### b. **update** - used to update value of existing row

```mysql
mysql> update cust8 set custage=25 where id=103;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update cust8 set city='ABC',state='XYZ',custage=33 where id=103;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

### c. **delete** 
- used to delete the data but the structure will be present, **we can rollback** not like truncate.

```mysql
mysql> delete from cust8 where id=100;
Query OK, 1 row affected (0.01 sec)

mysql> delete from cust8;
Query OK, 4 rows affected (0.01 sec)
```



In MySQL the date will be always entered as `yyyy-mm-dd` or `yyyymmdd`