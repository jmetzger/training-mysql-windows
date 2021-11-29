# Creating a trigger without super privileges 

## Warum ist es so ? 

  * Trigger können nicht auf DETERMINISTIC gesetzt werden. 
  * Wenn ein Trigger nicht-deterministisch ist, kann es zu Problemen kommen
  * In diesem Fall kann es beim BINLOG_FORMAT=STATEMENT zu Problemen beim Slave kommen

## Test auf MySQL 8.0.27 BINLOG_FORMAT = ROW 

```
# User training@localhost mit folgenden Rechten 
show grants;
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Grants for training@localhost                                                                                                                                                                                                        |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `training`@`localhost`                                                                                                                                                                                         |
| GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, REFERENCES, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE, EVENT, TRIGGER ON `sakila`.* TO `training`@`localhost` |
+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
2 rows in set (0.01 sec)

# Test - Case 
use sakila;

# aus bug-report 
mysql> CREATE TABLE t1 ( a int );
Query OK, 0 rows affected (0.02 sec)

mysql> CREATE TRIGGER g1 BEFORE INSERT ON t1 FOR EACH ROW SET new.a=new.a+1;
ERROR 1419 (HY000): You do not have the SUPER privilege and binary logging is enabled (you *might* want to use the less safe log_bin_trust_function_creators variable)
```

## (Dirty-)Fix 

```
# Either set it in the config or as SUPER-privileges user:
/etc/mysql/mysql.conf.d/mysqld.cnf 
log-bin-trust-function-creators = 1 
systemctl restart mysql

# now login as unprivileged (NON SUPERUSER PERMS) and try again
# on localhost
mysql -utraining -p 
use sakila
mysql> CREATE TABLE if not exists t1 ( a int );
Query OK, 0 rows affected, 1 warning (0.00 sec)

mysql> DROP TRIGGER IF EXISTS g1;
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> CREATE TRIGGER g1 BEFORE INSERT ON t1 FOR EACH ROW SET new.a=new.a+1;
Query OK, 0 rows affected (0.00 sec)
```

## Refs:

  * https://bugs.mysql.com/bug.php?id=39489
