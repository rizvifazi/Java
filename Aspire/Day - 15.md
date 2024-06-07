
*Date : 05.20.2024*

## Subqueries
- select query inside another select query
- used to retrieve data based on unknown condition
- Inner query will be executed first and based on the output, the outer query will be executed
- 2 types
1. **Single row subquery** - inner query returns a single row, then it is evaluated with outer query using `=,!=,<,>,<=,>=`
2. **Multi row subquery** - inner query returns a multiple rows, then it is evaluated with outer query using `any,all,exists,not exists, in, not in`

```mysql
mysql> create table emp(eid int primary key,efirstname varchar(20),elastname varchar(20),ecity varchar(30));
Query OK, 0 rows affected (0.06 sec)

mysql> insert into emp values(1,'Ram','Kumar','Chennai');
Query OK, 1 row affected (0.01 sec)

mysql> insert into emp values(2,'Sam','Kumar','Pune');
Query OK, 1 row affected (0.01 sec)

mysql> insert into emp values(3,'Saj','Kumar','Mumbai');
Query OK, 1 row affected (0.01 sec)

mysql> insert into emp values(4,'Raj','Kumar','Delhi');
Query OK, 1 row affected (0.01 sec)

mysql> insert into emp values(5,'John','Smith','Bangalore');
Query OK, 1 row affected (0.01 sec)

mysql> insert into emp values(6,'Tim','Harry','Hyderabad');
Query OK, 1 row affected (0.01 sec)

mysql> create table dept(did int primary key,dname varchar(20),empid int,dsal float,constraint dept_fk foreign key(empid) references emp(eid));
Query OK, 0 rows affected (0.07 sec)

mysql> insert into dept values(1000,'HR',1,5000);
Query OK, 1 row affected (0.01 sec)

mysql> insert into dept values(1001,'Sales',2,10000);
Query OK, 1 row affected (0.01 sec)

mysql> insert into dept values(1002,'IT',3,5000);
Query OK, 1 row affected (0.01 sec)

mysql> insert into dept values(1003,'Admin',4,10000);
Query OK, 1 row affected (0.01 sec)

mysql> insert into dept values(1004,'HR',5,12000);
Query OK, 1 row affected (0.01 sec)

mysql> insert into dept values(1005,'IT',6,15000);
Query OK, 1 row affected (0.01 sec)

mysql> select * from emp;
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   1 | Ram        | Kumar     | Chennai   |
|   2 | Sam        | Kumar     | Pune      |
|   3 | Saj        | Kumar     | Mumbai    |
|   4 | Raj        | Kumar     | Delhi     |
|   5 | John       | Smith     | Bangalore |
|   6 | Tim        | Harry     | Hyderabad |
+-----+------------+-----------+-----------+
6 rows in set (0.01 sec)

mysql> select * from dept;
+------+-------+-------+-------+
| did  | dname | empid | dsal  |
+------+-------+-------+-------+
| 1000 | HR    |     1 |  5000 |
| 1001 | Sales |     2 | 10000 |
| 1002 | IT    |     3 |  5000 |
| 1003 | Admin |     4 | 10000 |
| 1004 | HR    |     5 | 12000 |
| 1005 | IT    |     6 | 15000 |
+------+-------+-------+-------+
6 rows in set (0.00 sec)

mysql> select * from emp where eid=(select empid from dept where dsal=12000);
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   5 | John       | Smith     | Bangalore |
+-----+------------+-----------+-----------+
1 row in set (0.01 sec)

mysql> select * from emp where eid in(select empid from dept where dsal>10000);
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   5 | John       | Smith     | Bangalore |
|   6 | Tim        | Harry     | Hyderabad |
+-----+------------+-----------+-----------+
2 rows in set (0.01 sec)

mysql> select * from emp where eid =(select empid from dept where dsal>10000); 
ERROR 1242 (21000): Subquery returns more than 1 row  -- Important
mysql> select * from emp where eid > any(select empid from dept where dsal<10000); -- Should satisfy any of the value condition
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   2 | Sam        | Kumar     | Pune      |
|   3 | Saj        | Kumar     | Mumbai    |
|   4 | Raj        | Kumar     | Delhi     |
|   5 | John       | Smith     | Bangalore |
|   6 | Tim        | Harry     | Hyderabad |
+-----+------------+-----------+-----------+
5 rows in set (0.00 sec)

mysql> select * from emp where eid > all(select empid from dept where dsal<10000); -- Should satisfy all of the condition.
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   4 | Raj        | Kumar     | Delhi     |
|   5 | John       | Smith     | Bangalore |
|   6 | Tim        | Harry     | Hyderabad |
+-----+------------+-----------+-----------+
3 rows in set (0.00 sec)

mysql> select * from emp where eid = all(select empid from dept where dsal<10000);
Empty set (0.00 sec)

mysql> select * from emp where exists(select * from dept where dsal=5000); -- If the query exists, ie- returns a value then execute other select query.
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   1 | Ram        | Kumar     | Chennai   |
|   2 | Sam        | Kumar     | Pune      |
|   3 | Saj        | Kumar     | Mumbai    |
|   4 | Raj        | Kumar     | Delhi     |
|   5 | John       | Smith     | Bangalore |
|   6 | Tim        | Harry     | Hyderabad |
+-----+------------+-----------+-----------+
6 rows in set (0.00 sec)

mysql> select * from emp where not exists(select * from dept where dsal=5000);
Empty set (0.00 sec)
```

## Joins
- At the time of displaying we can join multiple tables and get the relevant data

### Types
1. **Equi join**
      - We join the table based on some **equality condition**

```mysql
mysql> create table dept1(deptid int primary key,dname varchar(20));
Query OK, 0 rows affected (0.06 sec)

mysql> insert into dept1 values(10,'Sales');
Query OK, 1 row affected (0.01 sec)

mysql> insert into dept1 values(20,'Admin');
Query OK, 1 row affected (0.01 sec)

mysql> insert into dept1 values(30,'HR');
Query OK, 1 row affected (0.01 sec)

mysql> insert into dept1 values(40,'IT');
Query OK, 1 row affected (0.01 sec)

mysql> create table empl1(empid int primary key,ename varchar(20),deptid int,foreign key(deptid) references dept1(deptid));
Query OK, 0 rows affected (0.06 sec)

mysql> insert into empl1 values(1,'Pat',10);
Query OK, 1 row affected (0.01 sec)

mysql> insert into empl1 values(2,'Sat',20);
Query OK, 1 row affected (0.01 sec)

mysql> insert into empl1 values(3,'Pack',10);
Query OK, 1 row affected (0.01 sec)

mysql> insert into empl1(empid,ename) values(4,'Mack');
Query OK, 1 row affected (0.01 sec)

mysql> select * from dept1;
+--------+-------+
| deptid | dname |
+--------+-------+
|     10 | Sales |
|     20 | Admin |
|     30 | HR    |
|     40 | IT    |
+--------+-------+
4 rows in set (0.00 sec)

mysql> select * from empl1;
+-------+-------+--------+
| empid | ename | deptid |
+-------+-------+--------+
|     1 | Pat   |     10 |
|     2 | Sat   |     20 |
|     3 | Pack  |     10 |
|     4 | Mack  |   NULL |
+-------+-------+--------+
4 rows in set (0.00 sec)

mysql> select e.ename,d.dname from empl1 e,dept1 d where e.deptid=d.deptid; -- equi join equality condition
+-------+-------+
| ename | dname |
+-------+-------+
| Pat   | Sales |
| Sat   | Admin |
| Pack  | Sales |
+-------+-------+
3 rows in set (0.00 sec)

mysql> show tables;
+---------------------+
| Tables_in_javabatch |
+---------------------+
| books               |
| customer            |
| customer1           |
| customer2           |
| customer3           |
| dept                |
| dept1               |
| emp                 |
| empl1               |
| programmer          |
+---------------------+
10 rows in set (0.00 sec)

mysql> select * from dept;
+------+-------+-------+-------+
| did  | dname | empid | dsal  |
+------+-------+-------+-------+
| 1000 | HR    |     1 |  5000 |
| 1001 | Sales |     2 | 10000 |
| 1002 | IT    |     3 |  5000 |
| 1003 | Admin |     4 | 10000 |
| 1004 | HR    |     5 | 12000 |
| 1005 | IT    |     6 | 15000 |
+------+-------+-------+-------+
6 rows in set (0.00 sec)

mysql> select * from emp;
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   1 | Ram        | Kumar     | Chennai   |
|   2 | Sam        | Kumar     | Pune      |
|   3 | Saj        | Kumar     | Mumbai    |
|   4 | Raj        | Kumar     | Delhi     |
|   5 | John       | Smith     | Bangalore |
|   6 | Tim        | Harry     | Hyderabad |
+-----+------------+-----------+-----------+
6 rows in set (0.00 sec)

mysql> select e.efirstname,e.ecity,d.dname,d.dsal from emp e, dept d where e.eid=d.empid; -- equi join equality condition, common column.
+------------+-----------+-------+-------+
| efirstname | ecity     | dname | dsal  |
+------------+-----------+-------+-------+
| Ram        | Chennai   | HR    |  5000 |
| Sam        | Pune      | Sales | 10000 |
| Saj        | Mumbai    | IT    |  5000 |
| Raj        | Delhi     | Admin | 10000 |
| John       | Bangalore | HR    | 12000 |
| Tim        | Hyderabad | IT    | 15000 |
+------------+-----------+-------+-------+
6 rows in set (0.00 sec)
```

2. Inner join
      - similar to **equi join** but we have to use `on` clause

```mysql
mysql> select e.ename,d.dname from empl1 e,dept1 d where e.deptid=d.deptid; -- compare equi join
mysql> select e.ename,d.dname from empl1 e inner join dept1 d on e.deptid=d.deptid;
+-------+-------+
| ename | dname |
+-------+-------+
| Pat   | Sales |
| Sat   | Admin |
| Pack  | Sales |
+-------+-------+
3 rows in set (0.00 sec)

mysql> select e.efirstname,e.ecity,d.dname,d.dsal from emp e, dept d where e.eid=d.empid; -- compare equi join
mysql> select e.efirstname,e.ecity,d.dname,d.dsal from emp e inner join dept d on e.eid=d.empid;
+------------+-----------+-------+-------+
| efirstname | ecity     | dname | dsal  |
+------------+-----------+-------+-------+
| Ram        | Chennai   | HR    |  5000 |
| Sam        | Pune      | Sales | 10000 |
| Saj        | Mumbai    | IT    |  5000 |
| Raj        | Delhi     | Admin | 10000 |
| John       | Bangalore | HR    | 12000 |
| Tim        | Hyderabad | IT    | 15000 |
+------------+-----------+-------+-------+
6 rows in set (0.00 sec)
```

3. **Natural join**
      - create an implicit join clause based on common columns in a table, this must exist to join naturally.

```mysql
mysql> select * from empl1 natural join dept1;
+--------+-------+-------+-------+
| deptid | empid | ename | dname |
+--------+-------+-------+-------+
|     10 |     1 | Pat   | Sales |
|     20 |     2 | Sat   | Admin |
|     10 |     3 | Pack  | Sales |
+--------+-------+-------+-------+
3 rows in set (0.00 sec)

mysql> select * from emp natural join dept;  -- Produces incorrect results if common column does not exist.
+-----+------------+-----------+-----------+------+-------+-------+-------+
| eid | efirstname | elastname | ecity     | did  | dname | empid | dsal  |
+-----+------------+-----------+-----------+------+-------+-------+-------+
|   6 | Tim        | Harry     | Hyderabad | 1000 | HR    |     1 |  5000 |
|   5 | John       | Smith     | Bangalore | 1000 | HR    |     1 |  5000 |
|   4 | Raj        | Kumar     | Delhi     | 1000 | HR    |     1 |  5000 |
|   3 | Saj        | Kumar     | Mumbai    | 1000 | HR    |     1 |  5000 |
|   2 | Sam        | Kumar     | Pune      | 1000 | HR    |     1 |  5000 |
|   1 | Ram        | Kumar     | Chennai   | 1000 | HR    |     1 |  5000 |
|   6 | Tim        | Harry     | Hyderabad | 1001 | Sales |     2 | 10000 |
|   5 | John       | Smith     | Bangalore | 1001 | Sales |     2 | 10000 |
|   4 | Raj        | Kumar     | Delhi     | 1001 | Sales |     2 | 10000 |
|   3 | Saj        | Kumar     | Mumbai    | 1001 | Sales |     2 | 10000 |
|   2 | Sam        | Kumar     | Pune      | 1001 | Sales |     2 | 10000 |
|   1 | Ram        | Kumar     | Chennai   | 1001 | Sales |     2 | 10000 |
|   6 | Tim        | Harry     | Hyderabad | 1002 | IT    |     3 |  5000 |
|   5 | John       | Smith     | Bangalore | 1002 | IT    |     3 |  5000 |
|   4 | Raj        | Kumar     | Delhi     | 1002 | IT    |     3 |  5000 |
|   3 | Saj        | Kumar     | Mumbai    | 1002 | IT    |     3 |  5000 |
|   2 | Sam        | Kumar     | Pune      | 1002 | IT    |     3 |  5000 |
|   1 | Ram        | Kumar     | Chennai   | 1002 | IT    |     3 |  5000 |
|   6 | Tim        | Harry     | Hyderabad | 1003 | Admin |     4 | 10000 |
|   5 | John       | Smith     | Bangalore | 1003 | Admin |     4 | 10000 |
|   4 | Raj        | Kumar     | Delhi     | 1003 | Admin |     4 | 10000 |
|   3 | Saj        | Kumar     | Mumbai    | 1003 | Admin |     4 | 10000 |
|   2 | Sam        | Kumar     | Pune      | 1003 | Admin |     4 | 10000 |
|   1 | Ram        | Kumar     | Chennai   | 1003 | Admin |     4 | 10000 |
|   6 | Tim        | Harry     | Hyderabad | 1004 | HR    |     5 | 12000 |
|   5 | John       | Smith     | Bangalore | 1004 | HR    |     5 | 12000 |
|   4 | Raj        | Kumar     | Delhi     | 1004 | HR    |     5 | 12000 |
|   3 | Saj        | Kumar     | Mumbai    | 1004 | HR    |     5 | 12000 |
|   2 | Sam        | Kumar     | Pune      | 1004 | HR    |     5 | 12000 |
|   1 | Ram        | Kumar     | Chennai   | 1004 | HR    |     5 | 12000 |
|   6 | Tim        | Harry     | Hyderabad | 1005 | IT    |     6 | 15000 |
|   5 | John       | Smith     | Bangalore | 1005 | IT    |     6 | 15000 |
|   4 | Raj        | Kumar     | Delhi     | 1005 | IT    |     6 | 15000 |
|   3 | Saj        | Kumar     | Mumbai    | 1005 | IT    |     6 | 15000 |
|   2 | Sam        | Kumar     | Pune      | 1005 | IT    |     6 | 15000 |
|   1 | Ram        | Kumar     | Chennai   | 1005 | IT    |     6 | 15000 |
+-----+------------+-----------+-----------+------+-------+-------+-------+
36 rows in set (0.00 sec)

mysql> select * from dept natural join emp; -- Produces incorrect results if common column does not exist.
+------+-------+-------+-------+-----+------------+-----------+-----------+
| did  | dname | empid | dsal  | eid | efirstname | elastname | ecity     |
+------+-------+-------+-------+-----+------------+-----------+-----------+
| 1005 | IT    |     6 | 15000 |   1 | Ram        | Kumar     | Chennai   |
| 1004 | HR    |     5 | 12000 |   1 | Ram        | Kumar     | Chennai   |
| 1003 | Admin |     4 | 10000 |   1 | Ram        | Kumar     | Chennai   |
| 1002 | IT    |     3 |  5000 |   1 | Ram        | Kumar     | Chennai   |
| 1001 | Sales |     2 | 10000 |   1 | Ram        | Kumar     | Chennai   |
| 1000 | HR    |     1 |  5000 |   1 | Ram        | Kumar     | Chennai   |
| 1005 | IT    |     6 | 15000 |   2 | Sam        | Kumar     | Pune      |
| 1004 | HR    |     5 | 12000 |   2 | Sam        | Kumar     | Pune      |
| 1003 | Admin |     4 | 10000 |   2 | Sam        | Kumar     | Pune      |
| 1002 | IT    |     3 |  5000 |   2 | Sam        | Kumar     | Pune      |
| 1001 | Sales |     2 | 10000 |   2 | Sam        | Kumar     | Pune      |
| 1000 | HR    |     1 |  5000 |   2 | Sam        | Kumar     | Pune      |
| 1005 | IT    |     6 | 15000 |   3 | Saj        | Kumar     | Mumbai    |
| 1004 | HR    |     5 | 12000 |   3 | Saj        | Kumar     | Mumbai    |
| 1003 | Admin |     4 | 10000 |   3 | Saj        | Kumar     | Mumbai    |
| 1002 | IT    |     3 |  5000 |   3 | Saj        | Kumar     | Mumbai    |
| 1001 | Sales |     2 | 10000 |   3 | Saj        | Kumar     | Mumbai    |
| 1000 | HR    |     1 |  5000 |   3 | Saj        | Kumar     | Mumbai    |
| 1005 | IT    |     6 | 15000 |   4 | Raj        | Kumar     | Delhi     |
| 1004 | HR    |     5 | 12000 |   4 | Raj        | Kumar     | Delhi     |
| 1003 | Admin |     4 | 10000 |   4 | Raj        | Kumar     | Delhi     |
| 1002 | IT    |     3 |  5000 |   4 | Raj        | Kumar     | Delhi     |
| 1001 | Sales |     2 | 10000 |   4 | Raj        | Kumar     | Delhi     |
| 1000 | HR    |     1 |  5000 |   4 | Raj        | Kumar     | Delhi     |
| 1005 | IT    |     6 | 15000 |   5 | John       | Smith     | Bangalore |
| 1004 | HR    |     5 | 12000 |   5 | John       | Smith     | Bangalore |
| 1003 | Admin |     4 | 10000 |   5 | John       | Smith     | Bangalore |
| 1002 | IT    |     3 |  5000 |   5 | John       | Smith     | Bangalore |
| 1001 | Sales |     2 | 10000 |   5 | John       | Smith     | Bangalore |
| 1000 | HR    |     1 |  5000 |   5 | John       | Smith     | Bangalore |
| 1005 | IT    |     6 | 15000 |   6 | Tim        | Harry     | Hyderabad |
| 1004 | HR    |     5 | 12000 |   6 | Tim        | Harry     | Hyderabad |
| 1003 | Admin |     4 | 10000 |   6 | Tim        | Harry     | Hyderabad |
| 1002 | IT    |     3 |  5000 |   6 | Tim        | Harry     | Hyderabad |
| 1001 | Sales |     2 | 10000 |   6 | Tim        | Harry     | Hyderabad |
| 1000 | HR    |     1 |  5000 |   6 | Tim        | Harry     | Hyderabad |
+------+-------+-------+-------+-----+------------+-----------+-----------+
36 rows in set (0.00 sec)

-- Rename column and try again

mysql> desc emp;
+------------+-------------+------+-----+---------+-------+
| Field      | Type        | Null | Key | Default | Extra |
+------------+-------------+------+-----+---------+-------+
| eid        | int         | NO   | PRI | NULL    |       |
| efirstname | varchar(20) | YES  |     | NULL    |       |
| elastname  | varchar(20) | YES  |     | NULL    |       |
| ecity      | varchar(30) | YES  |     | NULL    |       |
+------------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)

mysql> desc dept;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| did   | int         | NO   | PRI | NULL    |       |
| dname | varchar(20) | YES  |     | NULL    |       |
| empid | int         | YES  | MUL | NULL    |       |
| dsal  | float       | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)

mysql> alter table dept rename column empid to eid;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc dept;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| did   | int         | NO   | PRI | NULL    |       |
| dname | varchar(20) | YES  |     | NULL    |       |
| eid   | int         | YES  | MUL | NULL    |       |
| dsal  | float       | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)

mysql> select * from emp natural join dept; -- Joins on the the basis of common column.
+-----+------------+-----------+-----------+------+-------+-------+
| eid | efirstname | elastname | ecity     | did  | dname | dsal  |
+-----+------------+-----------+-----------+------+-------+-------+
|   1 | Ram        | Kumar     | Chennai   | 1000 | HR    |  5000 |
|   2 | Sam        | Kumar     | Pune      | 1001 | Sales | 10000 |
|   3 | Saj        | Kumar     | Mumbai    | 1002 | IT    |  5000 |
|   4 | Raj        | Kumar     | Delhi     | 1003 | Admin | 10000 |
|   5 | John       | Smith     | Bangalore | 1004 | HR    | 12000 |
|   6 | Tim        | Harry     | Hyderabad | 1005 | IT    | 15000 |
+-----+------------+-----------+-----------+------+-------+-------+
6 rows in set (0.00 sec)

mysql> select * from dept natural join emp; 
+------+------+-------+-------+------------+-----------+-----------+
| eid  | did  | dname | dsal  | efirstname | elastname | ecity     |
+------+------+-------+-------+------------+-----------+-----------+
|    1 | 1000 | HR    |  5000 | Ram        | Kumar     | Chennai   |
|    2 | 1001 | Sales | 10000 | Sam        | Kumar     | Pune      |
|    3 | 1002 | IT    |  5000 | Saj        | Kumar     | Mumbai    |
|    4 | 1003 | Admin | 10000 | Raj        | Kumar     | Delhi     |
|    5 | 1004 | HR    | 12000 | John       | Smith     | Bangalore |
|    6 | 1005 | IT    | 15000 | Tim        | Harry     | Hyderabad |
+------+------+-------+-------+------------+-----------+-----------+
6 rows in set (0.00 sec)

```

4. Outer join
      - used to display both matched and unmatched data - 3 types

1. Left Outer Join
      - **all rows from left table** + only matched rows from right table

```mysql
mysql> select e.ename, d.dname from empl1 e left join dept1 d on e.deptid=d.deptid;
+-------+-------+
| ename | dname |
+-------+-------+
| Pat   | Sales |
| Sat   | Admin |
| Pack  | Sales |
| Mack  | NULL  |
+-------+-------+
4 rows in set (0.00 sec)

mysql> select * from emp;
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   1 | Ram        | Kumar     | Chennai   |
|   2 | Sam        | Kumar     | Pune      |
|   3 | Saj        | Kumar     | Mumbai    |
|   4 | Raj        | Kumar     | Delhi     |
|   5 | John       | Smith     | Bangalore |
|   6 | Tim        | Harry     | Hyderabad |
|   7 | Tom        | Hardy     | Colombo   |
+-----+------------+-----------+-----------+
7 rows in set (0.00 sec)

mysql> select * from dept;
+------+-------+------+-------+
| did  | dname | eid  | dsal  |
+------+-------+------+-------+
| 1000 | HR    |    1 |  5000 |
| 1001 | Sales |    2 | 10000 |
| 1002 | IT    |    3 |  5000 |
| 1003 | Admin |    4 | 10000 |
| 1004 | HR    |    5 | 12000 |
| 1005 | IT    |    6 | 15000 |
| 1006 | SE    | NULL | 30000 |
+------+-------+------+-------+
7 rows in set (0.00 sec)

mysql> select e.efirstname,e.ecity, d.dname, d.dsal from emp e left join dept d on e.eid=d.eid;
+------------+-----------+-------+-------+
| efirstname | ecity     | dname | dsal  |
+------------+-----------+-------+-------+
| Ram        | Chennai   | HR    |  5000 |
| Sam        | Pune      | Sales | 10000 |
| Saj        | Mumbai    | IT    |  5000 |
| Raj        | Delhi     | Admin | 10000 |
| John       | Bangalore | HR    | 12000 |
| Tim        | Hyderabad | IT    | 15000 |
| Tom        | Colombo   | NULL  |  NULL |
+------------+-----------+-------+-------+
7 rows in set (0.00 sec)
```

2. Right outer join
       - **all rows from right table** + only matched rows from left table

```mysql
mysql> select e.ename, d.dname from empl1 e right join dept1 d on e.deptid=d.deptid;
+-------+-------+
| ename | dname |
+-------+-------+
| Pat   | Sales |
| Pack  | Sales |
| Sat   | Admin |
| NULL  | HR    |
| NULL  | IT    |
+-------+-------+
5 rows in set (0.00 sec)

mysql> select e.efirstname,e.ecity, d.dname, d.dsal from emp e right join dept d on e.eid=d.eid;
+------------+-----------+-------+-------+
| efirstname | ecity     | dname | dsal  |
+------------+-----------+-------+-------+
| Ram        | Chennai   | HR    |  5000 |
| Sam        | Pune      | Sales | 10000 |
| Saj        | Mumbai    | IT    |  5000 |
| Raj        | Delhi     | Admin | 10000 |
| John       | Bangalore | HR    | 12000 |
| Tim        | Hyderabad | IT    | 15000 |
| NULL       | NULL      | SE    | 30000 |
+------------+-----------+-------+-------+
7 rows in set (0.00 sec)
```

3. Full outer join
      - return matched and unmatched data from both the table
      - In mysql, **we dont have full outer join**, we use union of left join and right join

```mysql
mysql> select e.ename, d.dname from empl1 e left join dept1 d on e.deptid=d.deptid
    ->   union
    -> select e.ename, d.dname from empl1 e right join dept1 d on d.deptid=e.deptid;
+-------+-------+
| ename | dname |
+-------+-------+
| Pat   | Sales |
| Sat   | Admin |
| Pack  | Sales |
| Mack  | NULL  |
| NULL  | HR    |
| NULL  | IT    |
+-------+-------+
6 rows in set (0.00 sec)


mysql> select e.efirstname,e.ecity, d.dname, d.dsal from emp e left join dept d on e.eid=d.eid
    -> union
    -> select e.efirstname,e.ecity, d.dname, d.dsal from emp e right join dept d on e.eid=d.eid;
+------------+-----------+-------+-------+
| efirstname | ecity     | dname | dsal  |
+------------+-----------+-------+-------+
| Ram        | Chennai   | HR    |  5000 |
| Sam        | Pune      | Sales | 10000 |
| Saj        | Mumbai    | IT    |  5000 |
| Raj        | Delhi     | Admin | 10000 |
| John       | Bangalore | HR    | 12000 |
| Tim        | Hyderabad | IT    | 15000 |
| Tom        | Colombo   | NULL  |  NULL |
| NULL       | NULL      | SE    | 30000 |
+------------+-----------+-------+-------+
8 rows in set (0.00 sec)
```

5. Cross join
      - cartesian product of two tables
```mysql
>select * from empl1,dept1;
    or
>select * from empl1 cross join dept1;

mysql> select * from empl1 cross join dept1;
+-------+-------+--------+--------+-------+
| empid | ename | deptid | deptid | dname |
+-------+-------+--------+--------+-------+
|     1 | Pat   |     10 |     10 | Sales |
|     2 | Sat   |     20 |     10 | Sales |
|     3 | Pack  |     10 |     10 | Sales |
|     4 | Mack  |   NULL |     10 | Sales |
|     1 | Pat   |     10 |     20 | Admin |
|     2 | Sat   |     20 |     20 | Admin |
|     3 | Pack  |     10 |     20 | Admin |
|     4 | Mack  |   NULL |     20 | Admin |
|     1 | Pat   |     10 |     30 | HR    |
|     2 | Sat   |     20 |     30 | HR    |
|     3 | Pack  |     10 |     30 | HR    |
|     4 | Mack  |   NULL |     30 | HR    |
|     1 | Pat   |     10 |     40 | IT    |
|     2 | Sat   |     20 |     40 | IT    |
|     3 | Pack  |     10 |     40 | IT    |
|     4 | Mack  |   NULL |     40 | IT    |
+-------+-------+--------+--------+-------+
16 rows in set (0.00 sec)

mysql> select * from emp cross join dept;
+-----+------------+-----------+-----------+------+-------+------+-------+
| eid | efirstname | elastname | ecity     | did  | dname | eid  | dsal  |
+-----+------------+-----------+-----------+------+-------+------+-------+
|   7 | Tom        | Hardy     | Colombo   | 1000 | HR    |    1 |  5000 |
|   6 | Tim        | Harry     | Hyderabad | 1000 | HR    |    1 |  5000 |
|   5 | John       | Smith     | Bangalore | 1000 | HR    |    1 |  5000 |
|   4 | Raj        | Kumar     | Delhi     | 1000 | HR    |    1 |  5000 |
|   3 | Saj        | Kumar     | Mumbai    | 1000 | HR    |    1 |  5000 |
|   2 | Sam        | Kumar     | Pune      | 1000 | HR    |    1 |  5000 |
|   1 | Ram        | Kumar     | Chennai   | 1000 | HR    |    1 |  5000 |
|   7 | Tom        | Hardy     | Colombo   | 1001 | Sales |    2 | 10000 |
|   6 | Tim        | Harry     | Hyderabad | 1001 | Sales |    2 | 10000 |
|   5 | John       | Smith     | Bangalore | 1001 | Sales |    2 | 10000 |
|   4 | Raj        | Kumar     | Delhi     | 1001 | Sales |    2 | 10000 |
|   3 | Saj        | Kumar     | Mumbai    | 1001 | Sales |    2 | 10000 |
|   2 | Sam        | Kumar     | Pune      | 1001 | Sales |    2 | 10000 |
|   1 | Ram        | Kumar     | Chennai   | 1001 | Sales |    2 | 10000 |
|   7 | Tom        | Hardy     | Colombo   | 1002 | IT    |    3 |  5000 |
|   6 | Tim        | Harry     | Hyderabad | 1002 | IT    |    3 |  5000 |
|   5 | John       | Smith     | Bangalore | 1002 | IT    |    3 |  5000 |
|   4 | Raj        | Kumar     | Delhi     | 1002 | IT    |    3 |  5000 |
|   3 | Saj        | Kumar     | Mumbai    | 1002 | IT    |    3 |  5000 |
|   2 | Sam        | Kumar     | Pune      | 1002 | IT    |    3 |  5000 |
|   1 | Ram        | Kumar     | Chennai   | 1002 | IT    |    3 |  5000 |
|   7 | Tom        | Hardy     | Colombo   | 1003 | Admin |    4 | 10000 |
|   6 | Tim        | Harry     | Hyderabad | 1003 | Admin |    4 | 10000 |
|   5 | John       | Smith     | Bangalore | 1003 | Admin |    4 | 10000 |
|   4 | Raj        | Kumar     | Delhi     | 1003 | Admin |    4 | 10000 |
|   3 | Saj        | Kumar     | Mumbai    | 1003 | Admin |    4 | 10000 |
|   2 | Sam        | Kumar     | Pune      | 1003 | Admin |    4 | 10000 |
|   1 | Ram        | Kumar     | Chennai   | 1003 | Admin |    4 | 10000 |
|   7 | Tom        | Hardy     | Colombo   | 1004 | HR    |    5 | 12000 |
|   6 | Tim        | Harry     | Hyderabad | 1004 | HR    |    5 | 12000 |
|   5 | John       | Smith     | Bangalore | 1004 | HR    |    5 | 12000 |
|   4 | Raj        | Kumar     | Delhi     | 1004 | HR    |    5 | 12000 |
|   3 | Saj        | Kumar     | Mumbai    | 1004 | HR    |    5 | 12000 |
|   2 | Sam        | Kumar     | Pune      | 1004 | HR    |    5 | 12000 |
|   1 | Ram        | Kumar     | Chennai   | 1004 | HR    |    5 | 12000 |
|   7 | Tom        | Hardy     | Colombo   | 1005 | IT    |    6 | 15000 |
|   6 | Tim        | Harry     | Hyderabad | 1005 | IT    |    6 | 15000 |
|   5 | John       | Smith     | Bangalore | 1005 | IT    |    6 | 15000 |
|   4 | Raj        | Kumar     | Delhi     | 1005 | IT    |    6 | 15000 |
|   3 | Saj        | Kumar     | Mumbai    | 1005 | IT    |    6 | 15000 |
|   2 | Sam        | Kumar     | Pune      | 1005 | IT    |    6 | 15000 |
|   1 | Ram        | Kumar     | Chennai   | 1005 | IT    |    6 | 15000 |
|   7 | Tom        | Hardy     | Colombo   | 1006 | SE    | NULL | 30000 |
|   6 | Tim        | Harry     | Hyderabad | 1006 | SE    | NULL | 30000 |
|   5 | John       | Smith     | Bangalore | 1006 | SE    | NULL | 30000 |
|   4 | Raj        | Kumar     | Delhi     | 1006 | SE    | NULL | 30000 |
|   3 | Saj        | Kumar     | Mumbai    | 1006 | SE    | NULL | 30000 |
|   2 | Sam        | Kumar     | Pune      | 1006 | SE    | NULL | 30000 |
|   1 | Ram        | Kumar     | Chennai   | 1006 | SE    | NULL | 30000 |
+-----+------------+-----------+-----------+------+-------+------+-------+
49 rows in set (0.00 sec)

```

7. Self join - join on same table
```mysql
-- like matrix multiplication
mysql> select a.efirstname as firstname1, b.efirstname as firstname2,a.ecity from emp a, emp b where a.eid<>b.eid;
+------------+------------+-----------+
| firstname1 | firstname2 | ecity     |
+------------+------------+-----------+
| Tom        | Ram        | Colombo   |
| Tim        | Ram        | Hyderabad |
| John       | Ram        | Bangalore |
| Raj        | Ram        | Delhi     |
| Saj        | Ram        | Mumbai    |
| Sam        | Ram        | Pune      |
| Tom        | Sam        | Colombo   |
| Tim        | Sam        | Hyderabad |
| John       | Sam        | Bangalore |
| Raj        | Sam        | Delhi     |
| Saj        | Sam        | Mumbai    |
| Ram        | Sam        | Chennai   |
| Tom        | Saj        | Colombo   |
| Tim        | Saj        | Hyderabad |
| John       | Saj        | Bangalore |
| Raj        | Saj        | Delhi     |
| Sam        | Saj        | Pune      |
| Ram        | Saj        | Chennai   |
| Tom        | Raj        | Colombo   |
| Tim        | Raj        | Hyderabad |
| John       | Raj        | Bangalore |
| Saj        | Raj        | Mumbai    |
| Sam        | Raj        | Pune      |
| Ram        | Raj        | Chennai   |
| Tom        | John       | Colombo   |
| Tim        | John       | Hyderabad |
| Raj        | John       | Delhi     |
| Saj        | John       | Mumbai    |
| Sam        | John       | Pune      |
| Ram        | John       | Chennai   |
| Tom        | Tim        | Colombo   |
| John       | Tim        | Bangalore |
| Raj        | Tim        | Delhi     |
| Saj        | Tim        | Mumbai    |
| Sam        | Tim        | Pune      |
| Ram        | Tim        | Chennai   |
| Tim        | Tom        | Hyderabad |
| John       | Tom        | Bangalore |
| Raj        | Tom        | Delhi     |
| Saj        | Tom        | Mumbai    |
| Sam        | Tom        | Pune      |
| Ram        | Tom        | Chennai   |
+------------+------------+-----------+
42 rows in set (0.00 sec)
```



**Schema object** - anything that is stored inside the database (ie) tables, view, procedure, functions


## Views
- It is a schema object 
- It is a virtual table because it **doesn't have its own data**, it will be containing data of another table which is called **as base table**
- Used to execute any **complex queries**, hide the implementation from client, can retrieve data using view name.

### 2 types
1. Simple view
2. Compound view

#### Syntax:
`CREATE [OR REPLACE] view viewname as SELECT stmt;`

```mysql
mysql> create view v1 as select e.ename,d.dname from empl1 e,dept1 d where e.deptid=d.deptid;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from v1;
+-------+-------+
| ename | dname |
+-------+-------+
| Pat   | Sales |
| Sat   | Admin |
| Pack  | Sales |
+-------+-------+
3 rows in set (0.00 sec)

mysql> show tables;
+---------------------+
| Tables_in_javabatch |
+---------------------+
| cust1               |
| cust7               |
| cust8               |
| customer            |
| customer3           |
| customer4           |
| customer5           |
| customer6           |
| department          |
| dept                |
| dept1               |
| emp                 |
| emp1                |
| empl                |
| empl1               |
| v1                  |
+---------------------+
16 rows in set (0.03 sec)

mysql> show full tables;
+---------------------+------------+
| Tables_in_javabatch | Table_type |
+---------------------+------------+
| dept                | BASE TABLE |
| dept1               | BASE TABLE |
| emp                 | BASE TABLE |
| emp1                | BASE TABLE |
| empl                | BASE TABLE |
| empl1               | BASE TABLE |
| v1                  | VIEW       |
+---------------------+------------+
16 rows in set (0.00 sec)

mysql> drop table empl1;
Query OK, 0 rows affected (0.04 sec)

mysql> select * from v1;
ERROR 1356 (HY000): View 'javabatch.v1' references invalid table(s) or column(s) or function(s) or definer/invoker of view lack rights to use them
mysql> drop view v1;
Query OK, 0 rows affected (0.01 sec)

mysql> show full tables;
+---------------------+------------+
| Tables_in_javabatch | Table_type |
+---------------------+------------+
| dept                | BASE TABLE |
| dept1               | BASE TABLE |
| emp                 | BASE TABLE |
| emp1                | BASE TABLE |
| empl                | BASE TABLE |
+---------------------+------------+
14 rows in set (0.00 sec)


mysql> create view v1 as select e.efirstname,e.ecity, d.dname, d.dsal from emp e left join dept d on e.eid=d.eid;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from v1;
+------------+-----------+-------+-------+
| efirstname | ecity     | dname | dsal  |
+------------+-----------+-------+-------+
| Ram        | Chennai   | HR    |  5000 |
| Sam        | Pune      | Sales | 10000 |
| Saj        | Mumbai    | IT    |  5000 |
| Raj        | Delhi     | Admin | 10000 |
| John       | Bangalore | HR    | 12000 |
| Tim        | Hyderabad | IT    | 15000 |
| Tom        | Colombo   | NULL  |  NULL |
+------------+-----------+-------+-------+
7 rows in set (0.00 sec)

mysql> show full tables;
+---------------------+------------+
| Tables_in_javabatch | Table_type |
+---------------------+------------+
| books               | BASE TABLE |
| customer            | BASE TABLE |
| customer1           | BASE TABLE |
| customer2           | BASE TABLE |
| customer3           | BASE TABLE |
| dept                | BASE TABLE |
| dept1               | BASE TABLE |
| emp                 | BASE TABLE |
| empl1               | BASE TABLE |
| programmer          | BASE TABLE |
| result              | BASE TABLE |
| v1                  | VIEW       |
+---------------------+------------+
12 rows in set (0.00 sec)

mysql> select * from v1 where dsal=10000; -- Running queries on the view.
+------------+-------+-------+-------+
| efirstname | ecity | dname | dsal  |
+------------+-------+-------+-------+
| Sam        | Pune  | Sales | 10000 |
| Raj        | Delhi | Admin | 10000 |
+------------+-------+-------+-------+
2 rows in set (0.00 sec)

mysql> desc v1;
+------------+-------------+------+-----+---------+-------+
| Field      | Type        | Null | Key | Default | Extra |
+------------+-------------+------+-----+---------+-------+
| efirstname | varchar(20) | YES  |     | NULL    |       |
| ecity      | varchar(30) | YES  |     | NULL    |       |
| dname      | varchar(20) | YES  |     | NULL    |       |
| dsal       | float       | YES  |     | NULL    |       |
+------------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)


mysql> insert into v1 values('Ram','Tokyo','QA',23000);                       -- Cannot modify view
ERROR 1471 (HY000): The target table v1 of the INSERT is not insertable-into

```

## Updateable View
 - Certain views are updatable (ie) when we perform DML operation on the view it will affect the base table, but with following condition on select stmt
  1. select stmt should not contain distinct, set, aggregate function, order by, group by, having clause
  2. left join, outer join
  3. subquery in the select stmt

```mysql
mysql> create view v2 as select * from dept1;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from v2;
+--------+-------+
| deptid | dname |
+--------+-------+
|     10 | Sales |
|     20 | Admin |
|     30 | HR    |
|     40 | IT    |
+--------+-------+
4 rows in set (0.00 sec)

mysql> insert into v2 values(50,'Operations');
Query OK, 1 row affected (0.01 sec)

mysql> insert into v2 values(60,'Accounts');
Query OK, 1 row affected (0.01 sec)

mysql> select * from v2;
+--------+------------+
| deptid | dname      |
+--------+------------+
|     10 | Sales      |
|     20 | Admin      |
|     30 | HR         |
|     40 | IT         |
|     50 | Operations |
|     60 | Accounts   |
+--------+------------+
6 rows in set (0.00 sec)

mysql> create view v5 as select dname, did from dept;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from v5;
+-------+------+
| dname | did  |
+-------+------+
| HR    | 1000 |
| Sales | 1001 |
| IT    | 1002 |
| Admin | 1003 |
| HR    | 1004 |
| IT    | 1005 |
| SE    | 1006 |
+-------+------+
7 rows in set (0.00 sec)

mysql> insert into v5 values('Operations', 1007);
Query OK, 1 row affected (0.01 sec)

mysql> select * from v5;
+------------+------+
| dname      | did  |
+------------+------+
| HR         | 1000 |
| Sales      | 1001 |
| IT         | 1002 |
| Admin      | 1003 |
| HR         | 1004 |
| IT         | 1005 |
| SE         | 1006 |
| Operations | 1007 |
+------------+------+
8 rows in set (0.00 sec)

mysql> select * from dept; -- Base table updated through view
+------+------------+------+-------+
| did  | dname      | eid  | dsal  |
+------+------------+------+-------+
| 1000 | HR         |    1 |  5000 |
| 1001 | Sales      |    2 | 10000 |
| 1002 | IT         |    3 |  5000 |
| 1003 | Admin      |    4 | 10000 |
| 1004 | HR         |    5 | 12000 |
| 1005 | IT         |    6 | 15000 |
| 1006 | SE         | NULL | 30000 |
| 1007 | Operations | NULL |  NULL |
+------+------------+------+-------+
8 rows in set (0.00 sec)

mysql> create view v6 as select dname,dsal from dept;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from v6;
+------------+-------+
| dname      | dsal  |
+------------+-------+
| HR         |  5000 |
| Sales      | 10000 |
| IT         |  5000 |
| Admin      | 10000 |
| HR         | 12000 |
| IT         | 15000 |
| SE         | 30000 |
| Operations |  NULL |
+------------+-------+
8 rows in set (0.00 sec)

mysql> insert into v6 values('QA', 17000);
-- ERROR 1423 (HY000): Field of view 'javabatch.v6' underlying table doesn't have a default value
-- View missing primary key

mysql> desc v6;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| dname | varchar(20) | YES  |     | NULL    |       |
| dsal  | float       | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
2 rows in set (0.00 sec)

mysql>
```

with check options in views
    - Certain views are updatable, so at time of updating the view, we want check some condition

```mysql
mysql> create view v3 as select * from dept1 where deptid>50;
Query OK, 0 rows affected (0.01 sec)

mysql> select * from v3;
+--------+----------+
| deptid | dname    |
+--------+----------+
|     60 | Accounts |
+--------+----------+
1 row in set (0.00 sec)

mysql> update v2 set dname='Finance' where deptid=10;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update v3 set dname='Finances' where deptid=10;
Query OK, 0 rows affected (0.00 sec)
Rows matched: 0  Changed: 0  Warnings: 0

mysql> select * from v3;
+--------+----------+
| deptid | dname    |
+--------+----------+
|     60 | Accounts |
+--------+----------+
1 row in set (0.00 sec)

mysql> select * from dept1;
+--------+------------+
| deptid | dname      |
+--------+------------+
|     10 | Finance    |
|     20 | Admin      |
|     30 | HR         |
|     40 | IT         |
|     50 | Operations |
|     60 | Accounts   |
+--------+------------+
6 rows in set (0.00 sec)

mysql> create view v4 as select * from dept1 where deptid>50 with check option; -- All DML operations should satisfy check option
Query OK, 0 rows affected (0.01 sec)

mysql> insert into v4 values(70,'Marketing');
Query OK, 1 row affected (0.01 sec)

mysql> select * from v4;
+--------+-----------+
| deptid | dname     |
+--------+-----------+
|     60 | Accounts  |
|     70 | Marketing |
+--------+-----------+
2 rows in set (0.00 sec)

mysql> insert into v4 values(35,'Marketing1');
ERROR 1369 (HY000): CHECK OPTION failed 'javabatch.v4'
```

**---Rename view**
```mysql
mysql> rename table v4 to v5;
Query OK, 0 rows affected (0.01 sec)
```

**---Drop view**
```mysql
mysql> drop view v3;
Query OK, 0 rows affected (0.02 sec)
```

**---Alter view**
1. using create or replace
2. First we have drop the view and recreate it once again


## Index
   - It is a schema object 
   - used for faster retrieval of data if your table contains huge number of records
   - Index will be **automatically created for the table which contains primary key** and **unique key**, that type of index is called **BTree index**

#### Syntax:
`CREATE INDEX indexname on tablename(columnames,...);`

```mysql
mysql> select * from dept1;
+--------+------------+
| deptid | dname      |
+--------+------------+
|     10 | Finance    |
|     20 | Admin      |
|     30 | HR         |
|     40 | IT         |
|     50 | Operations |
|     60 | Accounts   |
|     70 | Marketing  |
+--------+------------+
7 rows in set (0.00 sec)

mysql> create index indx1 on dept1(dname);
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> show indexes from dept1;
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| dept1 |          0 | PRIMARY  |            1 | deptid      | A         |           6 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| dept1 |          1 | indx1    |            1 | dname       | A         |           7 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
2 rows in set (0.01 sec)

mysql> drop index indx1 on dept1;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> show indexes from dept1;
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| dept1 |          0 | PRIMARY  |            1 | deptid      | A         |           6 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
1 row in set (0.00 sec)
```

#### Measuring Query performance with profiles

```mysql
mysql> set profiling = 1;
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysql> select * from emp where elastname='Kumar';
+-----+------------+-----------+---------+
| eid | efirstname | elastname | ecity   |
+-----+------------+-----------+---------+
|   1 | Ram        | Kumar     | Chennai |
|   2 | Sam        | Kumar     | Pune    |
|   3 | Saj        | Kumar     | Mumbai  |
|   4 | Raj        | Kumar     | Delhi   |
+-----+------------+-----------+---------+
4 rows in set (0.00 sec)

mysql> show profiles;
+----------+------------+-------------------------------------------+
| Query_ID | Duration   | Query                                     |
+----------+------------+-------------------------------------------+
|        1 | 0.00068250 | select * from emp where elastname='Kumar' |
+----------+------------+-------------------------------------------+
1 row in set, 1 warning (0.00 sec)

mysql> select * from emp where elastname like 'Ha%';
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   6 | Tim        | Harry     | Hyderabad |
|   7 | Tom        | Hardy     | Colombo   |
+-----+------------+-----------+-----------+
2 rows in set (0.00 sec)

mysql> show profiles;
+----------+------------+----------------------------------------------+
| Query_ID | Duration   | Query                                        |
+----------+------------+----------------------------------------------+
|        1 | 0.00068250 | select * from emp where elastname='Kumar'    |
|        2 | 0.00059975 | select * from emp where elastname like 'Ha%' |
+----------+------------+----------------------------------------------+
2 rows in set, 1 warning (0.00 sec)

mysql> create index nameidx on emp(elastname);
Query OK, 0 rows affected (0.04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> show indexed from emp
    -> ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'indexed from emp' at line 1
mysql> show indexeds from emp;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'indexeds from emp' at line 1
mysql> show indexes from emp;
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| Table | Non_unique | Key_name | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment | Visible | Expression |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
| emp   |          0 | PRIMARY  |            1 | eid         | A         |           6 |     NULL |   NULL |      | BTREE      |         |               | YES     | NULL       |
| emp   |          1 | ind1     |            1 | ecity       | A         |           7 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
| emp   |          1 | nameidx  |            1 | elastname   | A         |           4 |     NULL |   NULL | YES  | BTREE      |         |               | YES     | NULL       |
+-------+------------+----------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+---------+------------+
3 rows in set (0.00 sec)

mysql> show profiles;
+----------+------------+----------------------------------------------+
| Query_ID | Duration   | Query                                        |
+----------+------------+----------------------------------------------+
|        1 | 0.00068250 | select * from emp where elastname='Kumar'    |
|        2 | 0.00059975 | select * from emp where elastname like 'Ha%' |
|        3 | 0.03521300 | create index nameidx on emp(elastname)       |
|        4 | 0.00012200 | show indexed from emp                        |
|        5 | 0.00017200 | show indexeds from emp                       |
|        6 | 0.00423550 | show indexes from emp                        |
+----------+------------+----------------------------------------------+
6 rows in set, 1 warning (0.00 sec)

mysql> select * from emp where elastname='Kumar';
+-----+------------+-----------+---------+
| eid | efirstname | elastname | ecity   |
+-----+------------+-----------+---------+
|   1 | Ram        | Kumar     | Chennai |
|   2 | Sam        | Kumar     | Pune    |
|   3 | Saj        | Kumar     | Mumbai  |
|   4 | Raj        | Kumar     | Delhi   |
+-----+------------+-----------+---------+
4 rows in set (0.00 sec)

mysql> select * from emp where elastname like 'Ha%';
+-----+------------+-----------+-----------+
| eid | efirstname | elastname | ecity     |
+-----+------------+-----------+-----------+
|   7 | Tom        | Hardy     | Colombo   |
|   6 | Tim        | Harry     | Hyderabad |
+-----+------------+-----------+-----------+
2 rows in set (0.00 sec)

mysql> show profiles;
+----------+------------+----------------------------------------------+
| Query_ID | Duration   | Query                                        |
+----------+------------+----------------------------------------------+
|        1 | 0.00068250 | select * from emp where elastname='Kumar'    |
|        2 | 0.00059975 | select * from emp where elastname like 'Ha%' |
|        3 | 0.03521300 | create index nameidx on emp(elastname)       |
|        4 | 0.00012200 | show indexed from emp                        |
|        5 | 0.00017200 | show indexeds from emp                       |
|        6 | 0.00423550 | show indexes from emp                        |
|        7 | 0.00067175 | select * from emp where elastname='Kumar'    |
|        8 | 0.00191000 | select * from emp where elastname like 'Ha%' |
+----------+------------+----------------------------------------------+
8 rows in set, 1 warning (0.00 sec)
```


> whenever you create a table at least make sure it contains a primary key, so its in 1NF, Fully Normalized will be better.