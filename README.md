# Address-Book-System-SQL
## UC1 - Create database address_book_service
```
create database address_book_service;
```
### Show database 
```
show databases;
```
### Go to the database created and select current database
```
use address_book_service;
select database();
```
## UC2 - Create address_book_table with various attributes

```
create table if not exists address_book_table(
     firstname varchar(30) not null default '',
     lastname varchar(30) not null default '',
     address varchar(50) not null default '',
     city varchar(30) not null default '',
     phoneNumber int unsigned not null unique,
     email varchar(50) not null default '',
     primary key (phoneNumber)
     );
```
### Show tables in the database
```
show tables;
```
### Show details of table
```
desc address_book_table;
```

