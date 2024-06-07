
*Date : 05.17.2024*

Create the table WORLDCITY with the following data.
 
City	Country	Continent	Latitude	NorthSouth	Longitude	EastWest
Athens	Greece	Europe	37.59	N	23.44	E
Atlanta	United States	North America	33.45	N	84.23	W
Dallas	United States	North America	32.47	N	96.47	W
Nashville	United States	North America	36.09	N	86.46	W
Victoria	Canada	North America	48.25	N	123.21	W
Peterborough	Canada	North America	44.18	N	79.18	W
Vancouver	Canada	North America	49.18	N	123.04	W
Toledo	United States	North America	41.39	N	83.82	W
Warsaw	Poland	Europe	52.15	N	21.00	E
Lima	Peru	South America	12.03	S	77.03	W
Rio De Janeiro	Brazil	South America	22.43	S	43.13	W
Santiago	Chile	South America	33.27	S	70.40	W
Bogota	Colombia	South America	04.36	N	74.05	W
Buenos Aires	Argentina	South America	34.36	S	58.28	W
Quito	Ecuador	South America	00.13	S	78.30	W
Caracas	Venezuela	South America	10.30	N	66.56	W
Madras	India	Asia	28.36	N	77.12	E
Bombay	India	Asia	18.58	N	72.50	E
Manchester	England	Europe	51.30	N	0.0	null
Moscow	Russia	Europe	55.45	N	37.35	E
Paris	France	Europe	48.52	N	2.20	E
Shenyang	China	Asia	41.48	N	123.27	E
Cairo	Egypt	Africa	30.03	N	31.15	E
Tripoli	Lybia	Africa	32.54	N	13.11	E
Beijing	China	Asia	39.56	N	116.24	E
Rome	Italy	Europe	41.54	N	12.29	E
Tokyo	Japan	Asia	35.42	N	139.46	E
Sydney	Australia	Australia	33.52	S	151.13	E
Sparta	Greece	Europe	37.05	N	22.27	E
Madrid	Spain	Europe	40.24	N	3.41	W
 
Complete the following exercise:
1.	For all the different countries contained in the WORLDCITY table, display their names and the continent in which they are located. Make sure that no country name is duplicated.
1.	Write an SQL query to display the list of the city and country for all the cities that begin with letter R.
2.	Write an SQL query to display the list of the city and country for all the cities that end with letter A.
3.	Write an SQL query to display the list of the city and country for all the cities that begin with letter M and have exactly six letters in them.
4.	Write an SQL query to display the list of the city and country for all the cities that contain an A as the second letter. 
 
Complete the following exercise:
a)	Create a following tables

CUSTOMER Table Schema:
COLUMN NAME	DESCRIPTION	DATATYPE	SIZE	CONSTRAINTS
CUSTID	Customer Id	Number		Primary Key
FNAME	First Name	Character	30	
LNAME	Last Name	Character	30	
ADDRESS	Customer Address 	Character	50	
PHONENO	Phone	Number		Not Null
CITY	City	Character	20	
COUNTRY	Country	Character	20	
DATEFIRSTPURCHASED	Date of the first purchase by the customer	Date		
SUPPLIERID	Supplier Information	Number		Foreign Key 

Data for CUSTOMER table:
CUSTID	FNAME	LNAME	ADDRESS	PHONENO	CITY	COUNTRY	DATEFIRSTPURCHASED	SUPPLIERID
1001	Das	Jeyaseelan	119, park Avenue, II street,	9841093428	Coimbatore	India	10-jan-2004	1
2001	Gopi	Govindraj	241, I floor, Kamaraj street, Madippakkam	9444124590	Chennai	India	25-mar-2005	4
1201	Dilip	Kishore	43, II Avenue, Anna Nagar	9997234534	Bangalore	India	20-aug-2004	2
1300	Aanand	Chowdhury	42/1 sector 1, II Street	9841054348	Bangalore	India	15-may-2005	2
1220	Chandra	Nagarajan	83, lal bagh	98410672356	Bangalore	India	12-feb-2006	4
1221	Abhishek	Kumar	13,kishori park,	94447623901	Chennai	India	15-may-2004	1
1320	Nikhil	Pandit	218, alwaanya street	94448923091	Salem	India	21-apr-2006	3
1222	Meenu	Monica	C11, church road	98410563421	Trichy	India	30-aug-2004	1
1225	Pavan	Kumar	128/A, North Mada Street	99934782103	maduari	India	18-aug-2004	4



SUPPLIER Table Schema:
COLUMN NAME	DESCRIPTION	DATATYPE	SIZE	CONSTRAINTS
SUPPLIERID	Supplier Id	Number		Primary Key
SNAME	Supplier Name	Character	30	
SCITY	Supplier City	Character	30	
SPHONE	Supplier Phone	Number		Not Null
EMAIL	Email id of Supplier	Character	50	Unique



Data for SUPPLIER table:
SUPPLIERID	SNAME	SCITY	SPHONE	EMAIL
1	Dilip	Chennai	8999900000	dilip@abc.co.in

2	Tarun	Madurai	8999911111	tarun@xyz.com

3	Naresh	Coimbatore	8999922222	g.naresh@xyzl.com

4	Ganesan	Trichy	8999933333	Ganesan_83@ijk.com


 
ORDERS Table Schema:
COLUMN NAME	DESCRIPTION	DATATYPE	SIZE	CONSTRAINTS
ORDERID	Order Number	Number		Primary Key
ORDERDATE	Date of Order	Date		
CUSTID	Customer Identity	Number		
QUANTITY	Quantity Ordered	Number		Check (Quantity >0)
ITEMID	Item Code	Number		Foreign Key

Data for ORDERS Table:
ORDERID	ORDERDATE	CUSTID	QUANTITY	ITEMID
1	12-jan-2004	1001	30	25
2	6-may-2005	1202	38	24
3	16-dec-2006	1220	10	22
4	21-may-2004	1233	12	21

ITEMS Table Schema:
COLUMN NAME	DESCRIPTION	DATATYPE	SIZE	CONSTRAINTS
ITEMID	Item Code	Number		Primary Key
ITEMNAME	Item Name	Character	35	Not Null
SUPPLIERID	Supplier Code	Number		Foreign Key
MINQTY	Minimum Qty that can be ordered	Number		Not Null
MAXQTY	Maximum Qty that can be ordered	Number		Not Null
Price	Price per unit	Number(5,2)		

Data for ITEMS Table:
ITEMID	ITEMNAME	SUPPLIERID	MINQTY	MAXQTY	Price
20	Pears Soap	4	7	20	30.00
21	V.V.D. Coconut oil 200 ml	2	8	15	79.00
22	Ponds powder 400g	3	6	25	106.00
23	Reynolds pen- blue	1	10	30	15.00
24	Reynolds pen- black	1	10	30	16.00
25	Mysore sandal soap	4	7	25	25.00
26	Fair & lovely cream- 50g	3	5	15	55.00
27	Rexono deo spary	2	5	20	100.00
28	Dove soap	4	7	15	85.00


b)	Write SQL queries to
i.	Display all customers from Chennai.
ii.	Display the details of all customers who purchased from the supplier 2.
iii.	Display CUSTID, FNAME, LNAME of all customers whose purchase date is after January 2005.
iv.	Display the details of all suppliers who are from location Coimbatore.
v.	Display the details of all suppliers whose name stars with G.
vi.	Display the details of all customers, who do not have the alphabet e in their LNAME.
vii.	Display the details of the entire customer whose first date of purchase is in 2006 and arrange it in descending order.
viii.	Display the details of all the orders where the quantity is less than 35.
ix.	Display the details of the items supplied by supplier 4.
x.	Display the details of all items where SUPPLIERID is 3 and the MINQTY is greater than 7 order by ITEMID.
