# **Postgres Basic Commands**
- enter the command below in CMD to enter Postgres Command Line Interface
```cmd
psql -U postgres
```
```cmd
\list ## command to list all the databases
\c dbname ## switch connection a new database
\! cls ## clean and clear the CMD logs
\dt list all the tables in current database
```

# **CRUD**
## **1. Create**
```sql
CREATE TABLE accounts (
	user_id serial PRIMARY KEY,
	username VARCHAR ( 50 ) UNIQUE NOT NULL,
	password VARCHAR ( 50 ) NOT NULL,
	email VARCHAR ( 255 ) UNIQUE NOT NULL,
	created_on TIMESTAMP NOT NULL,
    last_login TIMESTAMP 
);
```
## **2. Insert**
```sql
 INSERT INTO TABLE_NAME  
 (column1,  
 column2,  
 column3, ……columnN)   
 VALUES (value1, value2, value3, ….. valueN); 

## insert new values into the table
INSERT INTO student (name,age) 
VALUES ('Alex',22),('Paul',24)

## insert default values into table
INSERT INTO student (name,age)
VALUES (DEFAULT,DEFAULT)
```
## **3. Update**
```sql
UPDATE table_name 
SET age = 25 
WHERE firstname = 'Kelvin' 
AND lastname = 'Leong'
```
## **4. Delete**
```sql
DELETE FROM table_name
WHERE [CONDITION]
```