# Working with datababases 

## Explanations 

```
# open a connection to the mysql-server by entering
mysql
# then you will get
mysql> 
```

```
# Comments within mysql-client
# three - in a row 
---
```



## Show databases

```
mysql
mysql>
;; from here i leave out mysql> 
;; so you can easily copy & paste the lines hereafter 
show databases 

--
-- or 
--

show schemas 

--
-- or by using information_schema 
--

select * from information_schema.schemata;
```

## Use a specific database 

```
# use specific database
use sakila;



## Create database 

```
create database training
create schema training2
```
