# Introduction

## View of Data

- A **database system** is a collection of interrelated data and a set of programs that allow users to access and modify these data
- A major **purpose** of a database system is to provide users with an abstract view of the data



### Data Models

- **Data models**: A collection of conceptual tools for describing data, data relationships, data semantics, and data constraints
- **Relational model**: All the data is stored in various **tables**



### Data abstraction

- **Data abstraction**: Hide the complexity of data structures to represent data in the database from users through several levels of data abstraction

![image-20211007230309970](C:\Users\Elian Li\AppData\Roaming\Typora\typora-user-images\image-20211007230309970.png)



### Instances and Schemas

- **Logical Schema**: the overall logical structure of the database
- **Physical schema**: the overall physical structure of the database
- **Instance**: the actual content of the database at a particular point **in time**
- **Physical Data Independence**: the ability to modify the physical schema without changing the logical schema



## Database Languages

### Data Definition Language (DDL)

- Specification notation for defining the **database schema**

```sql
create table instructor (
	ID			char(5),
    name		varchar(20),
    dept_name	varchar(20),
    salary		numeric(8,2))
```

- DDL compiler generates a set of table templates stored in a **data dictionary**
- Data dictionary contains metadata: **Database schema**, **integrity constraints** (Primary key) & **authorization**



### Data Manipulation Language (DML)

- Language for accessing and updating the data organized by the appropriate data model
- **Query Language**: The portion of a DML that involves information retrieval
- **Procedural DML**: require a user to specify what data are needed and how to get those data
- **Declarative DML**: require a user to specify what data are needed without specifying how to get those data
- SQL query language is **nonprocedural** (declarative). A query takes as input several tables (possibly only one) and always returns a single table

- SQL is **NOT** a Turing machine equivalent language



## Database Design

- **Logical Design**: Deciding on the **database schema**. Database design requires that we find a “good” collection of relation schemas
- **Physical Design**: Deciding on the physical layout of the database      



## Database Engine

- The functional components of a database system can be divided into **the** **storage manager**, **the query processor** component & **the transaction management** component



### Storage Manager

- **Storage Manager**: A program module that provides the interface between the low-level data stored in the database and the application programs and queries submitted to the system
- The storage manager is responsible to the following **tasks**:
  - Interaction with the OS file manager
  - Efficient storing, retrieving and updating of data
- The storage manager **components** include: Authorization and integrity manager, transaction manager, file manager & buffer manager
- The storage manager implements several **data structures** as part of the physical system implementation:
  - **Data files**: store the database itself
  - **Data dictionary**: stores metadata about the structure of the database, in particular the schema of the database
  - **Indices**: can provide fast access to data items. A database index provides pointers to those data items that hold a particular value



### Query Processor

- **DDL Interpreter**: interprets DDL statements and records the definitions in the **data dictionary**
- **DML Compiler**: translates DML statements in a query language into an evaluation plan consisting of low-level instructions that the query evaluation engine understands. The DML compiler performs **query optimization**; that is, it picks the lowest cost evaluation plan from among the various alternatives
- **Query Evaluation Engine**: executes low-level instructions generated by the DML compiler

![image-20211007235532877](C:\Users\Elian Li\AppData\Roaming\Typora\typora-user-images\image-20211007235532877.png)



### Transaction Management

- A transaction is a collection of operations that performs a single **logical function** in a database application
- **Transaction-management component** ensures that the database remains in a **consistent** (correct) state despite system failures (e.g., power failures and operating system crashes) and transaction failures
- **Concurrency-control manager** controls the interaction among the concurrent transactions, to ensure the **consistency** of the database



## Database Architecture

- Centralized databases

- Client-server
- Parallel databases
- Distributed databases

![image-20211008000554697](C:\Users\Elian Li\AppData\Roaming\Typora\typora-user-images\image-20211008000554697.png)



## Database Users and Administrators

- **Database Administrator (DBA)**: A person who has central control over the system

![image-20211008000615806](C:\Users\Elian Li\AppData\Roaming\Typora\typora-user-images\image-20211008000615806.png)

![image-20211008000734773](C:\Users\Elian Li\AppData\Roaming\Typora\typora-user-images\image-20211008000734773.png)
