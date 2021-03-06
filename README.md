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
## UC8 - Retrieve data sorted alphabetically on name for a given city
```
select * from address_book_table
     where city='Hazaribagh' order by firstname;
```
## UC9 - Add type and name for each address book
### Add familyLog as type and name as family for some contacts
```
 update address_book_table
     set TYPE='familyLog' , NAME='family'
     where firstname='Devnandan' or firstname='Dev';
```
### Add friendsLog as type and name as friends for some contacts
```
 update address_book_table
     set TYPE='friendsLog' , NAME='friends'
     where firstname='Mohan';
```
### Add professionLog as type and name as profession for some contacts
``` 
update address_book_table
     set TYPE='professionLog' , NAME='profession'
     where firstname='Suraj';
```
### Check the updates in table
```
 select * from address_book_table;
```
## UC10 - Find number of contacts by its type
```
 select count(*) as FAMILY_COUNT from address_book_table
     where type='familyLog';
```
## UC11 - Add persons to both family and friends
### Adding person to family
```
 insert into address_book_table
    values ('Nirmal', 'Kumar', 'Bihar', 'Patna', 958477, 'nirmal@gmail.com', 'family', 'familyLog');
```
### Adding person to friends
```
 insert into address_book_table
    values ('Bibhuti', 'Rajan', 'Bihar', 'Chatra', 945687, 'bibhuti@gmail.com', 'friends', 'friendsLog');
```
### Checking the update in table
```
 select * from address_book_table;
```
## UC12 - Creating ER diagram
### Creating Contact table
```
 create table Contact
    -> (
    -> firstName varchar(50) not null,
    -> lastName varchar(50) not null,
    -> Address varchar(150) not null,
    -> city varchar(50) not null,
    -> PhoneNumber int unsigned not null,
    -> Email varchar(50) not null primary key
    -> Address_Book_Name varchar(50) not null foreign key references address_book(Address_Book_Name)
    -> );
```
### Creating table address_book_dict
```
 create table address_book_dict
    -> (
    -> Address_Book_Name varchar(50) not null primary key,
    -> Type varchar(50) not null
    -> );
```
## UC13 - 
### Inserting data into contact table
```
  insert into Contact values
     ('Dev', 'Kumar', 'Jharkhand', 'Hazaribagh', 7870752948, 'devk@gmail.com', 'Personal');
     ('Nandan', 'raj', 'Bihar', 'Patna', 8265478955, 'nandank@gmail.com', 'Casual'),
     ('Mohana', 'kavya', 'T.S.', 'HYD', 9784595425, 'mohana@gmail.com', 'Professional'),
     ('Sai', 'Deeksha', 'T.S', 'HYD',  78459745645, 'deeksha@gmail.com', 'Professional'),
     ('Saurabh', 'Harale', 'A.P', 'HYD', 7845123690, 'saurabh@gmail.com', 'Casual'),
     ('Manoj', 'Kumar', 'Jharkhand', 'Ranchi', 987456320, 'manoj@gmail.com', 'Personal');
```
### Insert data into address_book_dict
```
insert into address_book_dict values
('Professional' , 'peers'),
('Personal', 'family'),
('Casual', 'friends);
```
### Retrieving Contacts for given city or state
```
select * from Contact left join address_book_dict using (Address_Book_Name) where city = 'HYD';
 select * from Contact left join address_book_dict using (Address_Book_Name) where Address = 'T.S';
```
### Understanding the size of address book by City and State
```
SELECT city,COUNT(*) as COUNT FROM contact left join address_book_dict using (Address_Book_Name) GROUP BY city;
SELECT Address,COUNT(*) as COUNT FROM contact left join address_book_dict using (Address_Book_Name) GROUP BY Address;
```
### Retrieve entries sorted alphabetically by Person’s name for a given city and state
```
select * from Contact left join address_book_dict using (Address_Book_Name) order by city asc;
select * from Contact left join address_book_dict using (Address_Book_Name) order by Address asc;
```
### Ability to get number of contact persons(count by its type)
```
SELECT type, COUNT(*) as COUNT FROM address_book_dict right join Contact using (Address_Book_Name) GROUP BY type;
```
