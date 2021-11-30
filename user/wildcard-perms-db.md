# Wildcard Permission for databases

## Why ? 

  * Allow a user to connect to all databases starting with prod_
  * Also those, that are present yet .


## Walktrough 

```
# as root 
mysql> create user schulung@localhost identified by 'my_super_secret_pass';
mysql> -- give permission to all databases starting with prod_
mysql> grant all on `prod\_%`.* to schulung@localhost 
mysql> create schema prod_db1; create schema prod_db2;
mysql> use prod_db1; create table data (id int); 
mysql> use prod_db2; create table data (id int);

# as user schulung@localhost
# connect and find out if you cann access db's 
# mysql -uschulung -p 





