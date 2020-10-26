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
### Show the complete CREATE TABLE statement used by MySQL to create this table
```
show create table address_book_table;
```
## UC3 - Insert new contacts to address book table
### Insert a row with all the column values
```
insert into address_book_table values( 'Devnandan', 'Kumar', 'Hazaribagh', 'Barhi', 787075, 'devnandan01997@gmail.com');
insert into address_book_table values( 'Suraj', 'Kumar', 'Hazaribagh', 'Barhi', 987456, 'sraj014@gmail.com');
```
### Insert multiple rows in one command
```
insert into address_book_table values( 'Dev', 'Sahab', 'Jharkhand', 'hazaribagh', 879700, 'devsahab01997@gmail.com'),
     ('Mohan', 'Thala', 'Ranchi', 'kanta-toli', 829496, 'mohan546@gmail.com');
```
### Show all the contents of table
```
select * from address_book_table;
```
## UC4 - Ability to edit existing contacts
### Modify selected rows
```
update address_book_table set address='Jharkhand' where firstname='Devnandan' or firstname='Mohan';
```
### Modify more than one values in given contact
```
update address_book_table set address='Jharkhand', city='Hazaribagh'  where firstname='Suraj' and lastname='Kumar';
```
## UC5 - Delete the contact where it meets criteria
### delete a single record
```
delete from address_book_table where firstname='Dev' and lastname='Sahab';
```
### Show tables after deletion
```
select * from address_book_table;
```
## UC6 - Retrieve contact for given state and city
```
select * from address_book_table where city='Hazaribagh' and address='Jharkhand';
```
## UC7 - Understand size of address_book_table by city and state
```
select city as 'CITY', address as 'STATE' , count(*) as 'COUNT' from address_book_table group by city, address;
```
