# SELECT INTO OUTFILE 

```
# Generally, you can only write to a specific folder if secure_file_priv isset

# Step1: Check setting in global server system variables 
select @@secure_file_priv;
# or 
show variables like 'secure_file_priv';

mysql> select @@secure_file_priv;
+------------------------------------------------+
| @@secure_file_priv                             |
+------------------------------------------------+
| C:\ProgramData\MySQL\MySQL Server 8.0\Uploads\ |
+------------------------------------------------+
1 row in set (0.00 sec)

# Step 2: than use exactly that path, but either with  '/' or '\\'
# Version 1
# Take whatever suffix you want ;o) 
mysql>SELECT * from sakila.actor INTO OUTFILE 'C:\\ProgramData\\MySQL\\MySQL Server 8.0\\Uploads\\actor.txt';
# Version 2 
mysql>SELECT * from sakila.actor INTO OUTFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/actor.txt';

```
