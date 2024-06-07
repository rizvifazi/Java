
*Date : 06.03.2024*



1.	Create JPA Relationship for the following diagram
![[jpa.png]]
 

JPA Relationship
     - used to establish the relationship between entities

1. One to One
      - one user has only one vehicle
      - In User class, we will be creating an object for Vehicle class

User table                                    Vehicle table
user_id(pk)  user_name  vehicle_id(fk)         vehicle_id(pk)   vehicle_name

a. Configure db info and hibernate properties in persistence.xml

b. Create Vehicle entity class 

@Entity
@Table(name="veh100")
public class Vehicle {
  @Id
  @GeneratedValue(strategy=GenerationType.AUTO)
  @Column(name="vehicle_id")
  private Integer id;
  @Column(name="vehicle_name")
  private String name;

  //getter,setter, constructor
}

c. Create User entity class

@Entity
@Table(name="user100")
public class User {
  @Id
  @GeneratedValue(strategy=GenerationType.AUTO)
  @Column(name="user_id")
  private Integer id;
  @Column(name="user_name")
  private String name;
  
  @OneToOne
  @JoinColumn(name="vehicle_id")
  private Vehicle vehicle;   //one user has only one vehicle

  //getter,setter, constructor
}

d. Configure entity class in xml file

<class>com.pack.User</class>
      <class>com.pack.Vehicle</class>

e. Create Main class

Cascading operation
    - used in mapping concept, if we perform any operation on one entity class it should be automatically affect the another entity class - 4 types
1. CascadeType.PERSIST
2. CascadeType.UPDATE
3. CascadeType.REMOVE
4. CascadeType.ALL

public class Main1 {

              public static void main(String[] args) {
                             EntityManagerFactory emf=Persistence.createEntityManagerFactory("student-info");
                             EntityManager em=emf.createEntityManager();
                             EntityTransaction et=em.getTransaction();
                             et.begin();
                             
                             Vehicle v1=new Vehicle();
                             v1.setName("Benz");
                             Vehicle v2=new Vehicle();
                             v2.setName("BMW");
                             
                             User u1=new User();
                             u1.setName("Ram");
                             u1.setVehicle(v1);
                             User u2=new User();
                             u2.setName("Sam");
                             u2.setVehicle(v2);
                             
                             //em.persist(v1);
                             //em.persist(v2);
                             em.persist(u1);
                             em.persist(u2);
                             
                             et.commit();
                             System.out.println("Success");
                             em.close();
                             emf.close();
              }

}

mysql> select * from veh100;
+------------+--------------+
| vehicle_id | vehicle_name |
+------------+--------------+
|         10 | Benz         |
|         12 | BMW          |
+------------+--------------+
2 rows in set (0.01 sec)

mysql> select * from user100;
+---------+-----------+------------+
| user_id | user_name | vehicle_id |
+---------+-----------+------------+
|       9 | Ram       |         10 |
|      11 | Sam       |         12 |
+---------+-----------+------------+
2 rows in set (0.00 sec)

2. One to many 
      - one user has many vehicle, in this case it creates a separate table which contain PK from both table

User table                                    Vehicle table
user_id(pk)  user_name                vehicle_id(pk)   vehicle_name

user_vehicle table
user_id   vehicle_id

a. Create Vehicle1 entity class

@Entity
@Table(name="veh101")
public class Vehicle1 {
  @Id
  @GeneratedValue(strategy=GenerationType.AUTO)
  @Column(name="vehicle_id")
  private Integer id;
  @Column(name="vehicle_name")
  private String name;
  
  //getter,setter, constructor
}

b. Create User1 entity class

@Entity
@Table(name="user101")
public class User1 {
  @Id
  @GeneratedValue(strategy=GenerationType.AUTO)
  @Column(name="user_id")
  private Integer id;
  @Column(name="user_name")
  private String name;
  
  @OneToMany(targetEntity = Vehicle1.class, cascade=CascadeType.ALL)
  //@OneToMany(cascade = CascadeType.ALL)
  //@JoinTable(name="user_vehicle",joinColumns=@JoinColumn(name="user_id")
         //  ,inverseJoinColumns=@JoinColumn(name="vehicle_id"))
  private List<Vehicle1> vehicle1=new ArrayList<>();

//getter,setter, constructor
}

C. Configure entity class in xml file

<class>com.pack.User1</class>
      <class>com.pack.Vehicle1</class>

e. Create Main class

public class Main1 {

              public static void main(String[] args) {
                             EntityManagerFactory emf=Persistence.createEntityManagerFactory("student-info");
                             EntityManager em=emf.createEntityManager();
                             EntityTransaction et=em.getTransaction();
                             et.begin();
                             
                             Vehicle1 v1=new Vehicle1();
                             v1.setName("Benz");
                             Vehicle1 v2=new Vehicle1();
                             v2.setName("BMW");
                             
                             List<Vehicle1> l1=new ArrayList<>();
                             l1.add(v1);
                             l1.add(v2);
                             
                             User1 u1=new User1();
                             u1.setName("Ram");
                             u1.setVehicle1(l1);
                             
                             em.persist(u1);
                             
                             et.commit();
                             System.out.println("Success");
                             em.close();
                             emf.close();
              }

}


mysql> select * from veh101;
+------------+--------------+
| vehicle_id | vehicle_name |
+------------+--------------+
|         14 | Benz         |
|         15 | BMW          |
+------------+--------------+
2 rows in set (0.01 sec)

mysql> select * from user101;
+---------+-----------+
| user_id | user_name |
+---------+-----------+
|      13 | Ram       |
+---------+-----------+
1 row in set (0.01 sec)

mysql> select * from user101_veh101;
+---------------+---------------------+
| User1_user_id | vehicle1_vehicle_id |
+---------------+---------------------+
|            13 |                  14 |
|            13 |                  15 |
+---------------+---------------------+
2 rows in set (0.01 sec)

3. Many to one
      - Many vehicle belongs to one user

4. Many to Many
      - Many user will have many vehicles


@Entity
@Table(name="veh102")
public class Vehicle2 {
  @Id
  @GeneratedValue(strategy=GenerationType.AUTO)
  @Column(name="vehicle_id")
  private Integer id;
  @Column(name="vehicle_name")
  private String name;
  
  @ManyToMany(targetEntity=User2.class)
  private List<User2> user=new ArrayList<>();
  

}


@Entity
@Table(name="user102")
public class User2 {
  @Id
  @GeneratedValue(strategy=GenerationType.AUTO)
  @Column(name="user_id")
  private Integer id;
  @Column(name="user_name")
  private String name;

  @ManyToMany(targetEntity=Vehicle2.class, cascade=CascadeType.ALL)
  private List<Vehicle2> vehicle=new ArrayList<>();
}

public class Main1 {

              public static void main(String[] args) {
                             EntityManagerFactory emf=Persistence.createEntityManagerFactory("student-info");
                             EntityManager em=emf.createEntityManager();
                             EntityTransaction et=em.getTransaction();
                             et.begin();
                             
                             Vehicle2 v1=new Vehicle2();
                             v1.setName("Benz");
                             Vehicle2 v2=new Vehicle2();
                             v2.setName("BMW");
                             
                             List<Vehicle2> l1=new ArrayList<>();
                             l1.add(v1);
                             l1.add(v2);
                             List<Vehicle2> l2=new ArrayList<>();
                             l2.add(v1);
                             l2.add(v2);
                             
                             User2 u1=new User2();
                             u1.setName("Ram");
                             u1.setVehicle(l1);
                             User2 u2=new User2();
                             u2.setName("Sam");
                             u2.setVehicle(l2);
                             
                             em.persist(u1);
                             em.persist(u2);
                             
                             et.commit();
                             System.out.println("Success");
                             em.close();
                             emf.close();
              }

}

mysql> select * from veh102;
+------------+--------------+
| vehicle_id | vehicle_name |
+------------+--------------+
|         17 | Benz         |
|         18 | BMW          |
+------------+--------------+
2 rows in set (0.00 sec)

mysql> select * from user102;
+---------+-----------+
| user_id | user_name |
+---------+-----------+
|      16 | Ram       |
|      19 | Sam       |
+---------+-----------+
2 rows in set (0.01 sec)

mysql> select * from user102_veh102;
+---------------+--------------------+
| User2_user_id | vehicle_vehicle_id |
+---------------+--------------------+
|            16 |                 17 |
|            16 |                 18 |
|            19 |                 17 |
|            19 |                 18 |
+---------------+--------------------+
4 rows in set (0.01 sec)


JPA Inheritance
    - entity class also can be inherited - 3 types

1. Single table/Table per class inheritance
      - For all entity class it will create only a single table 

@DiscriminatorColumn - used to differentiate the type of employee
@DiscriminatorValue - used to provide value for the column we generated

@Entity
@Table(name="emp100")
@Inheritance(strategy=InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name="empType",discriminatorType = DiscriminatorType.STRING)
@DiscriminatorValue(value="employee")
public class Employee {
   @Id
   private Integer id;
   private String name;
}

@Entity
@DiscriminatorValue(value="reg_employee")
public class RegularEmployee extends Employee{
    private Double salary;
    private Double bonus;
}

@Entity
@DiscriminatorValue(value="cont_employee")
public class ContractEmployee extends Employee{
    private Double payPerHour;
    private Integer duration;
}

<class>com.pack.Employee</class>
      <class>com.pack.RegularEmployee</class>
      <class>com.pack.ContractEmployee</class>


public class Main {
              public static void main(String[] args) {
                             EntityManagerFactory emf=Persistence.createEntityManagerFactory("student-info");
                             EntityManager em=emf.createEntityManager();
                             EntityTransaction et=em.getTransaction();
                             et.begin();
                             
                             Employee e1=new Employee();
                             e1.setId(100);
                             e1.setName("Ram");
                             
                             RegularEmployee r1=new RegularEmployee();
                             r1.setId(101);
                             r1.setName("Sam");
                             r1.setSalary(20000.0);
                             r1.setBonus(2000.0);
                             
                             ContractEmployee c1=new ContractEmployee();
                             c1.setId(102);
                             c1.setName("Saj");
                             c1.setPayPerHour(2000.2);
                             c1.setDuration(20);
                             
                             em.persist(e1);
                             em.persist(r1);
                             em.persist(c1);
                             
                             et.commit();
                             System.out.println("Success");
                             em.close();
                             emf.close();
                                                          
              }
}


mysql> select * from emp100;
+---------------+-----+------+-------+--------+----------+------------+
| empType       | id  | name | bonus | salary | duration | payPerHour |
+---------------+-----+------+-------+--------+----------+------------+
| employee      | 100 | Ram  |  NULL |   NULL |     NULL |       NULL |
| reg_employee  | 101 | Sam  |  2000 |  20000 |     NULL |       NULL |
| cont_employee | 102 | Saj  |  NULL |   NULL |       20 |     2000.2 |
+---------------+-----+------+-------+--------+----------+------------+
3 rows in set (0.01 sec)


2. Table per concrete class inheritance
       - For each entity class it creates separate table

@Entity
@Table(name="emp101")
@Inheritance(strategy=InheritanceType.TABLE_PER_CLASS)
public class Employee {
   @Id
   private Integer id;
   private String name;
}

@Entity
@Table(name="regemp101")
@AttributeOverrides({
              @AttributeOverride(name="id",column=@Column(name="id")),
  @AttributeOverride(name="name",column=@Column(name="name"))
})
public class RegularEmployee extends Employee{
    private Double salary;
    private Double bonus;
}

@Entity
@Table(name="contemp101")
@AttributeOverrides({
              @AttributeOverride(name="id",column=@Column(name="id")),
  @AttributeOverride(name="name",column=@Column(name="name"))
})
public class ContractEmployee extends Employee{
    private Double payPerHour;
    private Integer duration;
}

mysql> select * from emp101;
+-----+------+
| id  | name |
+-----+------+
| 100 | Ram  |
+-----+------+
1 row in set (0.01 sec)

mysql> select * from regemp101;
+-----+------+-------+--------+
| id  | name | bonus | salary |
+-----+------+-------+--------+
| 101 | Sam  |  2000 |  20000 |
+-----+------+-------+--------+
1 row in set (0.00 sec)

mysql> select * from contemp101;
+-----+------+----------+------------+
| id  | name | duration | payPerHour |
+-----+------+----------+------------+
| 102 | Saj  |       20 |     2000.2 |
+-----+------+----------+------------+
1 row in set (0.00 sec)

3. Joined/Table per subclass inheritance
       - used to join the table based primary key and foreign key relationship

@Entity
@Table(name="emp102")
@Inheritance(strategy=InheritanceType.JOINED)
public class Employee {
   @Id
   private Integer id;
   private String name;
}

@Entity
@Table(name="regemp102")
@PrimaryKeyJoinColumn(name="id")
public class RegularEmployee extends Employee{
    private Double salary;
    private Double bonus;
}

@Entity
@Table(name="contemp102")
@PrimaryKeyJoinColumn(name="id")
public class ContractEmployee extends Employee{
    private Double payPerHour;
    private Integer duration;
}
mysql> select * from emp102;
+-----+------+
| id  | name |
+-----+------+
| 100 | Ram  |
| 101 | Sam  |
| 102 | Saj  |
+-----+------+
3 rows in set (0.00 sec)

mysql> select * from regemp102;
+-------+--------+-----+
| bonus | salary | id  |
+-------+--------+-----+
|  2000 |  20000 | 101 |
+-------+--------+-----+
1 row in set (0.01 sec)

mysql> select * from contemp102;
+----------+------------+-----+
| duration | payPerHour | id  |
+----------+------------+-----+
|       20 |     2000.2 | 102 |
+----------+------------+-----+
1 row in set (0.01 sec)

