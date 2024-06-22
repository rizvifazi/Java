
*Date : 06.21.2024*

# Mockito framework 
- open source testing framework to create mock objects
- Every appl we create 3 tier architecture (ie) controller, service and repository. If we write test case for controller, first it will hits the controller, then service, then repository, then database. But it is not a good practice to hit db at time of testing 
- If we want to mock repository data, whatever the request comes from controller,it forwards to the service prg and instead of forwarding to actuall repo prg and then to db, we create mock object of repo 

## 1. Create java maven project with junit 5 and mockito dependency
```xml
<dependencies>
            <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>5.5.2</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.mockito</groupId>
            <artifactId>mockito-junit-jupiter</artifactId>
            <version>3.2.4</version>
            <scope>test</scope>
        </dependency> 
    </dependencies>
```

## 2. Create model class
```java
public class Book {
              private String bookId;
              private String title;
              private int price;
              private LocalDate publishedDate;
        //getter, setter, constructor
}
```

## 3. Create repo interface
```java
public interface BookRepository {
              Book findBookByBookId(String bookId);
              void save(Book book);
}
```

## 4. Create service program
```java
public class BookService {
              
              private BookRepository bookRepository;
              
              public BookService(BookRepository bookRepository) {
                             this.bookRepository = bookRepository;
              }
              
              public int calculateTotalCost(List<String> bookIds) {
                             int total = 0;
                             for(String bookId : bookIds){
                                           Book book = bookRepository.findBookByBookId(bookId);
                                           total = total + book.getPrice();
                             }
                             return total;
              }
              
              public void addBook(Book book) {
                             bookRepository.save(book);
              }
              
              
}
```

`@RunWith(MockitoJunitRunner.class)` - Junit 4 will support mockito based annotation

`@ExtendWith(MockitoExtension.class)` - Junit 5 will support mockito based annotation

Service <-> Repository <-> Database

`@InjectMocks` - It tells which class is under test - program that is communicate with external dependency or class annotated with `@Mock`

`@Mock` - create a mock implementation for the class you need 

## 1. Stubbing of methods
   - One of the primary benefit of mockito is ability to return a provided response for a specific method is called on mock dependency, so we need to tell mockito what to return as response of that method
   - The process of writing how a given mock method should behave or return 

2 ways
1. using mockito static method called `when()`+`thenReturn()` - "when" any specific method is called on mock object, "thenReturn" some preconfigured value
2. using mockito static method called `doReturn()`+`when()` - "doReturn" some preconfigured value "when" specific method is called on mock object 
3. test void methods using `doNothing()`+`when()`

```java
@ExtendWith(MockitoExtension.class)
public class BookServiceTest {

              @InjectMocks
              BookService bookService;
              @Mock
              BookRepository bookRepo;
              
              @Test
              public void testCalculateTotalCost() {
                             List<String> bookIds=new ArrayList<>();
                             bookIds.add("1234");
                             bookIds.add("1235");
                             
                             Book b1=new Book("1234","Mockito",500,LocalDate.now());
                             Book b2=new Book("1235","Junit",400,LocalDate.now());
                             
                             //when+thenReturn
                            /*when(bookRepo.findBookByBookId("1234")).thenReturn(b1);
                            when(bookRepo.findBookByBookId("1235")).thenReturn(b2);*/
                             
                             //doReturn+when
                            doReturn(b1).when(bookRepo).findBookByBookId("1234");
                            doReturn(b2).when(bookRepo).findBookByBookId("1235");
                             
                             int totalCost=bookService.calculateTotalCost(bookIds);
                             assertEquals(900,totalCost);
              }
              
              @Test
              public void testAddBook() {
                             Book b1=new Book("1234","Mockito",500,LocalDate.now());
                             doNothing().when(bookRepo).save(b1);
                             bookService.addBook(b1);
              }
}
```

## 2. Exception handling in Mockito
  - To handle exception in Mockito which covers negative scenarios

1. If we test exception for non void method then we can use `when()`+`thenThrow()`
2. If we test exception for void method then we use `doThrow()`+`when()`

### 1. Create model class
```java
public class Book {
              private String bookId;
              private String title;
              private int price;
              private LocalDate publishedDate;
}
```

### 2. Create repo interface
```java
public interface BookRepository {
              List<Book> findAllBooks() throws SQLException;
              void save(Book book) throws SQLException;
}
```

### 3. Create service class
```java
public class BookService {
              
              private BookRepository bookRepository;
              
              public BookService(BookRepository bookRepository) {
                             this.bookRepository = bookRepository;
              }
              
              public int getTotalPriceOfBooks() {
                             List<Book> books = null;
                             try {
                                           books = bookRepository.findAllBooks();
                             } catch (SQLException e) {
                                           // log exception
                                           throw new DatabaseReadException("Unable to read from database due to - " + e.getMessage());
                             }
                             int totalPrice = 0;
                             for(Book book : books){
                                           totalPrice = totalPrice + book.getPrice();
                             }
                             return totalPrice;
              }
              
              public void addBook(Book book){
                             try {
                                           bookRepository.save(book);
                             } catch (SQLException e) {
                                           // log exception
                                           throw new DatabaseWriteException("Unable to write in database due to - " + e.getMessage());
                             }
              }
}
```

### 4. Create DatabaseReadException
```java
public class DatabaseReadException extends RuntimeException {
              public DatabaseReadException(String message) {
                             super(message);
              }
}
```

### 5. Create DatabaseWriteException
```java
public class DatabaseWriteException extends RuntimeException {
              public DatabaseWriteException(String message) {
                             super(message);
              }
}
```

### 6. Create test
```java
@ExtendWith(MockitoExtension.class)
public class BookServiceTest {

              @InjectMocks
              BookService bookService;
              @Mock
              BookRepository bookRepo;
              
              @Test  //non void method
              public void testGetTotalPriceOfBooks() throws SQLException {
                        //when(bookRepo.findAllBooks()).thenThrow(SQLException.class);
                             
                             when(bookRepo.findAllBooks()).thenThrow(new SQLException("Database is not found"));
                             
                          //given(bookRepo.findAllBooks()).willThrow(SQLException.class);
                             
                             //assertThrows(DatabaseReadException.class,()->bookService.getTotalPriceOfBooks());
              }
              
              @Test  //void method
              public void testAddBook() throws SQLException {
                             Book b1=new Book("1234","Mockito",500,LocalDate.now());
                             
                            //doThrow(SQLException.class).when(bookRepo).save(b1);
                             
                             doThrow(new SQLException("Database is not found")).when(bookRepo).save(b1);
                             bookService.addBook(b1);
                             //assertThrows(DatabaseWriteException.class,()->bookService.addBook(b1));
              }
}
```

## 3. Behavior verification
   - one of important feature of mockito is that when mock object is created it remembers all operations performed on it using `verify()`

### 1. Create model class
```java
public class Book {
              private String bookId;
              private String title;
              private int price;
              private LocalDate publishedDate;
}

public class BookRequest {
              private String title;
              private int price;
              private LocalDate publishedDate;
}
```

### 2. Create repo interface
```java
public interface BookRepository {
              void save(Book book);
              Book findBookById(String bookId);
}
```

### 3. Create service 
```java
public class BookService {
              
              private BookRepository bookRepository;
              
              public BookService(BookRepository bookRepository) {
                             this.bookRepository = bookRepository;
              }
              
              public void addBook(Book book) {
                             if(book.getPrice() <= 500){
                                           return;
                             }
                             bookRepository.save(book);
              }
              
              public void addBook(BookRequest bookRequest) {
                             if(bookRequest.getPrice() <= 500){
                                           return;
                             }
                             Book book = new Book();
                             book.setTitle(bookRequest.getTitle());
                             book.setPrice(bookRequest.getPrice());
                            book.setPublishedDate(bookRequest.getPublishedDate());
                             bookRepository.save(book);
              }
              
              public void updatePrice(String bookId, int updatedPrice){
                             if(bookId==null) {
                                           return;
                             }
                             Book book = bookRepository.findBookById(bookId);
                             book.setPrice(updatedPrice);
                             bookRepository.save(book);
              }
}


@ExtendWith(MockitoExtension.class)
public class BookServiceTest {
              
              @InjectMocks
              BookService bookService;
              @Mock
              BookRepository bookRepo;
              
              @Test //To verify whether mock object is invoked or not
              public void testAddBook() {
                             Book b1=new Book("1234","Mockito",600,LocalDate.now());
                             bookService.addBook(b1);
                             verify(bookRepo).save(b1);
              }

              @Test //To verify number of invocations of mock method, if book price <= 500 then it wont invoke bookRepo
              public void testAddBook1() {
                             Book b1=new Book("1234","Mockito",500,LocalDate.now());
                             bookService.addBook(b1);
                             verify(bookRepo,times(0)).save(b1);
              }
              
              @Test 
              public void testAddBook2() {
                             Book b1=new Book("1234","Mockito",600,LocalDate.now());
                             Book b2=new Book("1235","Junit",700,LocalDate.now());
                             bookService.addBook(b1);
                             bookService.addBook(b2);
                             //verify(bookRepo,times(2)).save(b1);
                             //verify(bookRepo,atLeast(4)).save(b1);
                             verify(bookRepo,atMost(4)).save(b1);
                             verify(bookRepo,atMostOnce()).save(b1);
                             verify(bookRepo,atLeastOnce()).save(b1);
              }
              
              @Test //To verify number of invocations of mock method, if book price <= 500 then it wont invoke bookRepo
              //we checked using times(0), instead we can use never()
              public void testAddBook4() {
                             Book b1=new Book("1234","Mockito",500,LocalDate.now());
                             bookService.addBook(b1);
                             verify(bookRepo,never()).save(b1);
              }
              
              @Test
              public void testUpdatePrice() {
                             Book b1=new Book("1234","Mockito",600,LocalDate.now());
                             bookService.updatePrice("1234", 100);
                             verify(bookRepo).save(b1);
              }
              
              @Test
              public void testUpdatePrice1() {
                             Book b1=new Book(null,"Mockito",600,LocalDate.now());
                             bookService.updatePrice(null, 100);
                             verifyNoInteractions(bookRepo);
              }
              
              @Test
              public void testUpdatePrice2() {
                             Book b1=new Book("1234","Mockito",600,LocalDate.now());
                             when(bookRepo.findBookById("1234")).thenReturn(b1);
                             bookService.updatePrice("1234", 100);
                             verifyNoMoreInteractions(bookRepo);
              }
              
              @Test //To execute mock object in particular order
              public void testUpdatePrice3() {
                             Book b1=new Book("1234","Mockito",600,LocalDate.now());
                             when(bookRepo.findBookById("1234")).thenReturn(b1);
                             bookService.updatePrice("1234", 800);
                             InOrder o=Mockito.inOrder(bookRepo);
                             o.verify(bookRepo).findBookById("1234");
                             o.verify(bookRepo).save(b1);
              }
}
```


## 4. ArgumentCaptor
  - we can capture the arguments passed to mock object

### 1. Create model class
```java
public class Book {
              private String bookId;
              private String title;
              private int price;
              private LocalDate publishedDate;
}

public class BookRequest {
              private String title;
              private int price;
              private LocalDate publishedDate;
}
```

### 2. Create repo interface
```java
public interface BookRepository {
              void save(Book book);
}
```

### 3. Create service
```java
public class BookService {
              
              private BookRepository bookRepository;
              
              public BookService(BookRepository bookRepository) {
                             this.bookRepository = bookRepository;
              }

              
              public void addBook(BookRequest bookRequest) {
                             Book book = new Book();
                             book.setTitle(bookRequest.getTitle());
                             book.setPrice(bookRequest.getPrice());
                            book.setPublishedDate(bookRequest.getPublishedDate());
                             bookRepository.save(book);
              }
              
}

@ExtendWith(MockitoExtension.class)
public class BookServiceTest {

              @InjectMocks
              BookService bookService;
              @Mock
              BookRepository bookRepo;
              
              @Captor
              ArgumentCaptor<Book> bookCaptor;
              
              @Test
              public void testAddBook() {
                             BookRequest req=new BookRequest("Mockito",600,LocalDate.now());
                             bookService.addBook(req);
                             verify(bookRepo).save(bookCaptor.capture());
                             Book book=bookCaptor.getValue();
                             assertEquals("Mockito",book.getTitle());
              }
}
```

## 5. ArgumentMatchers
- used to pass some dynamic values to the arguments 
- It should be provide for all arguments, either u provide all arg as ArgumentMatchers or provide hardcoded value, but dont mix it, if we use combination then test case will be failed
- It can be used only with `when()` or with `verify()`
- Specific type of ArgumentMatchers like a`nyBoolean()`, `anyInt()`, `anyByte()`,` anyChar()`, `anyFloat()`, `anyString()`, `anyDouble()`, `anyLong()`, `anyShort()`
- Collection type ArgumentMatchers - `anyList()`, `anySet()`, `anyMap()`
- String type ArgumentMatchers -` matches(string)`, `startsWith(string)`, `endsWith(string)`, `contains(string)`

3 methods
- `any() - any object or null`
- `any(Class)`
- `anyVararg()`

### 1. Create model class
```java
public class Book {
              private String bookId;
              private String title;
              private int price;
              private LocalDate publishedDate;
              private boolean isDigital;
}
```

### 2. Create repo interface
```java
public interface BookRepository {
              void save(Book book);
              Book findBookById(String bookId);
              Book findBookByTitleAndPublishedDate(String title, LocalDate localDate);
              Book findBookByTitleAndPriceAndIsDigital(String title, int price, boolean isDigital);
              void saveAll(List<Book> books);
}
```

### 3. Create service class
```java
public class BookService {
              
              private BookRepository bookRepository;
              
              public BookService(BookRepository bookRepository) {
                             this.bookRepository = bookRepository;
              }
              
              
              public void updatePrice(String bookId, int updatedPrice){
                             Book book = bookRepository.findBookById(bookId);
                             book.setPrice(updatedPrice);
                             bookRepository.save(book);
              }
              
              public Book getBookByTitleAndPublishedDate(String title, LocalDate localDate) {
                             return bookRepository.findBookByTitleAndPublishedDate(title, localDate);
              }
              
              public Book getBookByTitleAndPriceAndIsDigital(String title, int price, boolean isDigital) {
                             return bookRepository.findBookByTitleAndPriceAndIsDigital(title, price, isDigital);
              }
              
              public void addBooks(List<Book> books) {
                             bookRepository.saveAll(books);
              }
}


@ExtendWith(MockitoExtension.class)
public class BookServiceTest {

              @InjectMocks
              BookService bookService;
              @Mock
              BookRepository bookRepo;
              
              @Test
              public void testUpdatePrice() {
                             Book b1=new Book("1234","Mockito",500,LocalDate.now());
                            //when(bookRepo.findBookById("1234")).thenReturn(b1);
                            //when(bookRepo.findBookById(anyString())).thenReturn(b1);
                           when(bookRepo.findBookById(any(String.class))).thenReturn(b1);
                             bookService.updatePrice("1234", 400);
                             verify(bookRepo).save(b1);
              }
              
              @Test
              public void testInvalidArgumentMatchers() {
                             Book b1=new Book("1234","Mockito",500,LocalDate.now());
                            //when(bookRepo.findBookByTitleAndPublishedDate("Mockito", any())).thenReturn(b1); //wrong
                             //Book b2=bookService.getBookByTitleAndPublishedDate("Mockito", any()); //wrong
                             
                         when(bookRepo.findBookByTitleAndPriceAndIsDigital(anyString(), anyInt(), anyBoolean())).thenReturn(b1);
                             Book b2=bookService.getBookByTitleAndPriceAndIsDigital("Mockito",600, false);
                             assertEquals("Mockito",b2.getTitle());
                             
                             List<Book> books=new ArrayList<>();
                             books.add(b1);
                             bookService.addBooks(books);
                             verify(bookRepo).saveAll(anyList());
              }
}
```