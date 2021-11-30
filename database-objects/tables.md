# Tables 

## Show tables 

```
# within mysql>
# so on the command-line enter:
# mysql (as root) 
USE sakila 
SHOW TABLES 

-- or --

select * from information_schema.TABLES 
```

### Create table 

```
-- only if you want to create table in a completely new database 
create schema training; 
USE training
CREATE TABLE people (id INT NOT NULL AUTO_INCREMENT, name VARCHAR(20), PRIMARY KEY(id)); 
```

### Find out the structure of the table 

```
# you have to connect to db first with 
# mysql 
# within mysql>
DESCRIBE people 
SHOW CREATE TABLE people 
-- or : if you want to know more --
SELECT * from INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME='people' AND TABLE_SCHEMA='training' \G
```

### Show indexes 

```
SHOW INDEX FROM actor 
SHOW INDEXES FROM ACTOR 
```

### Change table (Add field)  

```
--- We want to add a field before name 
--- IMPORTANT: BEFORE does not exist 
ALTER TABLE people ADD first_name VARCHAR(10) AFTER id;

ALTER TABLE schulungen ADD seats TINYINT unsigned DEFAULT 1, ADD price DECIMAL(6,2);
ALTER TABLE schulungen ADD (room TINYINT unsigned DEFAULT 1,  discount DECIMAL(6,2));

```

### Modify a field in table (Change property) 

```
ALTER TABLE people
	MODIFY COLUMN first_name VARCHAR(20);
```

### Drop a field from the table 

```
ALTER TABLE people ADD middle_name VARCHAR(25) BEFORE name; 
DESCRIBE people;
ALTER TABLE people DROP COLUMN middle_name;
```  

```
# More Examples
-- 
ALTER TABLE actor ADD in_rente BOOLEAN default true 
INSERT INTO actor (first_name,last_name,in_rente) values ('Jochen','Metzger',false)
-- Wieder loswerden 
ALTER TABLE actor DROP in_rente;
# add and drop in once command 
ALTER TABLE actor ADD in_rente2 BOOLEAN default true, DROP in_rente;
```

### Deleting table data (truncate) 

```
USE sakila
-- Create table based on other table 
CREATE TABLE actorcopy as SELECT * FROM actor;
-- Fields ? 
SELECT * FROM actorcopy; 
-- Empty it 
TRUNCATE TABLE actorcopy; 
-- Emptry ?
SELECT COUNT(*) FROM actorcopy; 
```

### Delete table data (with delete) 

#### Explanation 

  * Do not use delete when you want to use data of complete table
    * truncate is quicker in this case.
  * DELETE FROM ... WHERE ... does a SELECT first 
  
#### Example 

```
USE sakila
CREATE TABLE actorbackup AS SELECT * FROM actor;
SELECT COUNT(*) FROM actorbackup; 
DELETE FROM actorbackup WHERE actor_id > 100; 
SELECT COUNT(*) FROM actorbackup; 
```

### Delete complete table 

```
USE sakila
DROP TABLE actorbackup;
```

