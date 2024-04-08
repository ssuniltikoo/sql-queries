# sql-queries

#### SQL BASIC 
 ###### _keys_
```sql
Candiate keys vs primary keys
         
    ID | FIRST_NAME | LAST_NAME | EMAIL_ID | PHONE
         
    Candiate Keys : ID OR EMAIL_ID OR PHONE
    From List of above candiate keys any one can qualify for primary key
    Primary key is one of the candiate keys having special role of being the key 
    based on which data will be sorted in table
    *** However PHONE and EMAIL_ID should not be created as primary key as they can change in future for person
    while ID will always be the same, e.g EMP_ID or STudent_id.
   

```
> RULE OF THUMB  CHOOSE ONLY THAT COLUMN IN TABLE FOR PRIMARY KEY WHOSE VALUE NEVER CHANGES. Also multimple columns can be used 
> for primary key e.g PRIMARY key(emp_id, email), so data will be sorted first based on id and then email

#### _List of constraints for colums in table_

- UNIQUE
- NOT NULL
- default
- AUTO_increment
- primary key
- foreign key

```sql

create database scaler;

use scaler;

create table IF NOT EXISTS students 
(
	id int auto_increment,
    firstname varchar(50) not null,
    lastname varchar(50) not null,
    email varchar(50) not null unique,
    dateofbirth date not null ,
    enrollmentDate timestamp not null,
    psp decimal(5, 2) default 0,
    batchId int default 1,
    isActive boolean not null default false,
    primary key(id)
);

DROP TABLE students;
INSERT INTO students values('test','testing', 'test@test.com', '2001-01-28' , now(), 82.23, 1, 1);

--- INSERT INTO students("amit","anand", "amaitanand@test.com","01-01-2001",date,"12.23","1","1");

INSERT INTO students(firstname,lastname,email,dateofbirth,enrollmentDate,psp,batchId,isActive)  values('amit','sharma', 'amaitsharma@test.com', '2001-10-19' , now(), 12.23, 1, 1);

SELECT * from students;


INSERT INTO students(firstname,lastname,email,dateofbirth,enrollmentDate,psp,batchId,isActive)  values('amit','sharma', 'amaitsharma@test.com', '2001-10-19' , now(), 12.23, 1, 1);
INSERT INTO students(firstname,lastname,email,dateofbirth,enrollmentDate,psp,batchId,isActive)  values('babu','sharma', 'babutsharma@test.com', '1999-10-19' , now(), 22.23, 2, 1);

INSERT INTO students(firstname,lastname,email,dateofbirth,enrollmentDate,psp,batchId,isActive)  values('babu','verma', 'babuverma@test.com', '2012-10-19' , now(),29.23, null, 1);

INSERT INTO students(firstname,lastname,email,dateofbirth,enrollmentDate,psp,batchId,isActive)  values('abhi','sharma', 'abhisharma@test.com', '1998-10-19' , now(), 12.23, 3, 1);



```

###### _FOREIGN KEY_
> Foreign key is used to link one table to another. Foreign keys should be uniques that is the only constraint and any column
> can be selected to be foreign key and not necessary needs to be primary key of other table.
> Foreign key helps to handle data integrity for update queries and data orphaning for delete queries 
> Foreign key constraint  allows to handle this by
 - Throwing error
 - set values to null
 - delete all corresponding rows of other tables



-  ON DELETE
   -    cascade 
   -    set null
   -    No Action == restrict (don't allow delete)
   -    SET Default
- ON UPDATE
  - cascade 
   - set null
   - No Action
   - SET Default



```sql


-- create batch table

Create table IF NOT EXISTS BATCH(
	id int primary key Auto_increment,
    batch_name varchar(100) not null unique,
    start_date date not null,
    end_date date not null
) ;

INSERT INTO batch(batch_name, start_date, end_date) values('MAY_23', '2023-01-12', '2024-03-16');
INSERT INTO batch(batch_name, start_date, end_date) values('MAY_22', '2022-05-12', '2023-03-16');
INSERT INTO batch(batch_name, start_date, end_date) values('jan_23', '2023-01-12', '2024-03-16');
INSERT INTO batch(batch_name, start_date, end_date) values('sep_22', '2023-09-12', '2024-12-16');

select * from batch;
commit;
-- ALter table to update foreign key
ALTER TABLE students
ADD FOREIGN key(batchId)
REFERENCES batch(id);

select s.firstname, s.lastname , b.batch_name
from students s
join batch b
on s.batchid = b.id; 


```





