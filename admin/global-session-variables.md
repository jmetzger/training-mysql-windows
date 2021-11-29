# Globale/Persistente und Session Variablen 

## Find out with show and @@ 

```
mysql> show session variables like 'PERFORMANCE%schema';
+--------------------+-------+
| Variable_name      | Value |
+--------------------+-------+
| performance_schema | ON    |
+--------------------+-------+
1 row in set (0.00 sec)

mysql> select @@performance_schema;
+----------------------+
| @@performance_schema |
+----------------------+
|                    1 |
+----------------------+
1 row in set (0.00 sec)

mysql> select @@SESSION.performance_schema;
ERROR 1238 (HY000): Variable 'performance_schema' is a GLOBAL variable
mysql> select @@performance_schema;
+----------------------+
| @@performance_schema |
+----------------------+
|                    1 |
+----------------------+
1 row in set (0.00 sec)

mysql> select @@GLOBAL.long_query_time;
+--------------------------+
| @@GLOBAL.long_query_time |
+--------------------------+
|                10.000000 |
+--------------------------+
1 row in set (0.00 sec)

mysql> select @@SESSION.long_query_time;
+---------------------------+
| @@SESSION.long_query_time |
+---------------------------+
|                 10.000000 |
+---------------------------+
1 row in set (0.00 sec)

mysql> set SESSION long_query_time=0.000001
    -> ;
Query OK, 0 rows affected (0.00 sec)

mysql> select @@SESSION.long_query_time;
+---------------------------+
| @@SESSION.long_query_time |
+---------------------------+
|                  0.000001 |
+---------------------------+
1 row in set (0.00 sec)

mysql> select @@GLOBAL.long_query_time;
+--------------------------+
| @@GLOBAL.long_query_time |
+--------------------------+
|                10.000000 |
+--------------------------+
1 row in set (0.00 sec)

mysql> 


```

## SET PERSISTENT 

```
# Set variable to be use also after restart of mysql-server 
SET PERSIST long_query_time = 0.000001

# will we in 
C:\ProgramData\MySQL\MySQL Server 8.0\Data\mysql-auto.cnf 
# <- as json 
# loaded after my.ini 
```

## Get GLOBAL/SESSION variable directly from performance_schema (starting from MySQL 8) 

```
use performance_schema 
select * from global_variables;
select * from session_variables 

# or Alternative is (without use):
use sakila;
select * from performance_schema.global_variables
select * from performance_schema.session_variables

```
