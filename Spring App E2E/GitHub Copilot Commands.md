

@workspace /new

Prompt 1:
![[Pasted image 20241102234837.png]]


```
@workspace /new Create Capstone project structure for ABC NetBanking Portal involving Pure JavaScript and HTML5/CSS3 for frontend. The frontend to interact with backend https://localhost:443/abcnetbankingportal URI. Springboot 2.5 version as backend and the services as UserService for registration, LoginService for authentication, ManageAccountService for View Balance and manage beneficiaries, FundTransferService for fund transfer between own account and third party account, TransactionsService for deposits and withdrawals, StatementService for all transactions and current balance, NotificationService for all transactions as sms and email. Database as MySQL with schema SQL with some realistic data insertion. Using JWT-based authentication for API service and https encryption for communication. Maven project type. Java8. package com.abc.netbanking.
```


Prompt 2:
![[Pasted image 20241102234959.png]]

```
@workspace /new Create project Structure for ABC netbanking online portal - front end UI with javascript, Html5 and css3 for styling and F and backend services using Spring boot 3.0.5, Database to be used is H2. It should have following modules: User registration, User login, Account management, Fund Transfer, Transaction history and statements. Use Ajax for asynchronous API calls with backend service layer to interact with backend http://localhost:9090/NetBankingABC/url. it should have following services: Userservice, loginservice, Authservice,fundtransferservice, Accountservice,configservice. DB - H2 with schema sql with realistic data insertion. Maven project type. Java 11. package com.abc.netbanking.
```


## Combined

```
@workspace /new Create Capstone project structure for ABC NetBanking Portal with: * Front-end: Vanilla Javascript for UI with HTML5/CSS3 * Back-end: Spring Boot 3.3.5 (Java 17)* Database: H2 with schema and minimum 10 sample data * Modules : UserLogin, UserRegister, ResetPassword, UserProfile, UserSecurity, Notifications, AccountOverview, RecentTransactions, Beneficiaries, MakePayment, TransactionHistory, GenerateReport, ContactUs, FAQ, FeedbackForm, AppInfo  * Services: UserService, LoginService (w/ PasswordResetService), AuthService, AccountService, TransactionService, TransactionHistory and Statement Service AccountService, ConfigService, NotificationService, ReportGenerationService,  BeneficiaryService * Communication: REST API with JWT-based authentication and HTTPS encryption * Base Endpoint : http://localhost:9090/NetBankingABC/**resourceurl** * Testing: JUnit for unit tests * Build Automation: Maven with build tasks for compilation and packaging * Version Control: Git initialized Package: com.abc.netbanking **Optional:** * Include Ajax for asynchronous communication
```




## Authentication Authorization Fundamentals for Spring



A SecurityConfig class w/ password encoding mechanics. Include the authorization refactoring

Security Config `@Configuration` with `@EnableWebSecurity`.
`@EnableWebSecurity` is a meta-annotation that includes the removed `@Configuration`, still allowing for bean creation methods within the annotated class; but it also includes the `@EnableGlobalAuthentication` annotation that enables a great deal more security autoconfiguration to be done by Spring Boot for the application.




