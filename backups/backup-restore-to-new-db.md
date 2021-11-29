# Restore to new DB 


```
# using --databases sakila  instead does not work here 
mysqldump --events --routines sakila > /usr/src/sakila.sql
cd /usr/src

# Version 1
# echo "create schema sakilatraining" | mysql

# Version 2 - works also on Windows  
mysql -e 'create schema sakilatraining'
mysql sakilatraining < sakila.sql 
```
