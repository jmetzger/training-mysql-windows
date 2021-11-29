# Slow Query Log

## Walkthrough

```
mysql> show variables like '%slow%';
+-----------------------------+-------------------------------------+
| Variable_name               | Value                               |
+-----------------------------+-------------------------------------+
| log_slow_admin_statements   | OFF                                 |
| log_slow_extra              | OFF                                 |
| log_slow_replica_statements | OFF                                 |
| log_slow_slave_statements   | OFF                                 |
| slow_launch_time            | 2                                   |
| slow_query_log              | OFF                                 |
| slow_query_log_file         | /var/lib/mysql-data/mysql2-slow.log |
+-----------------------------+-------------------------------------+
7 rows in set (0.01 sec)

mysql> show variables like '%long%';
+----------------------------------------------------------+-----------+
| Variable_name                                            | Value     |
+----------------------------------------------------------+-----------+
| long_query_time                                          | 10.000000 |
| performance_schema_events_stages_history_long_size       | 10000     |
| performance_schema_events_statements_history_long_size   | 10000     |
| performance_schema_events_transactions_history_long_size | 10000     |
| performance_schema_events_waits_history_long_size        | 10000     |
+----------------------------------------------------------+-----------+
5 rows in set (0.00 sec)

mysql> set slow_query_log = on;
ERROR 1229 (HY000): Variable 'slow_query_log' is a GLOBAL variable and should be set with SET GLOBAL
mysql> set global slow_query_log = on;
Query OK, 0 rows affected (0.00 sec)

mysql> set global long_query_time = 0.000001;
Query OK, 0 rows affected (0.00 sec)

mysql> show session variables like 'long_query_time';
+-----------------+-----------+
| Variable_name   | Value     |
+-----------------+-----------+
| long_query_time | 10.000000 |
+-----------------+-----------+
1 row in set (0.00 sec)

mysql> show global variables like 'long_query_time';
+-----------------+----------+
| Variable_name   | Value    |
+-----------------+----------+
| long_query_time | 0.000001 |
+-----------------+----------+
1 row in set (0.01 sec)

mysql> quit
Bye
root@mysql2:/etc/mysql/mysql.conf.d# mysql
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 8.0.27-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show session variables like 'long_query_time';
+-----------------+----------+
| Variable_name   | Value    |
+-----------------+----------+
| long_query_time | 0.000001 |
+-----------------+----------+
1 row in set (0.00 sec)
```
