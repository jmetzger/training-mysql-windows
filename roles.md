# Rollen (Roles)

## Konzept 

  * Rollen 

## Walkthrough  

```
# Rolle anlegen 
mysql> CREATE ROLE sakiladb 
# Berechtigungen der Rolle zuordnen / alle Berechtigungen für sakila 
mysql> GRANT ALL ON sakila.* TO sakiladb 
# Nutzer anlegen 
mysql> CREATE USER roleuser@localhost identified by 'P@ssw0rd';

# Die Rolle dem Nutzer zugeordnet 
mysql> GRANT sakiladb TO roleuser@localhost 

# Die Standardrolle festlegen, wenn er sich einloggt 
SET DEFAULT ROLE ALL TO roleuser@localhost

```

## Weitere Rolle für den Nutzer 

```
CREATE ROLE mysqldb;
GRANT ALL ON mysql.* TO mysqldb;
GRANT mysqldb TO roleuser@localhost;

## Important. SET DEFAULT ROLE must be executed once 
## again to have mysqldb selected after login 
SET DEFAULT ROLE ALL TO roleuser@localhost;

```

## Abgekürzte From 

```
create user roleuser2@localhost identified by 'P@ssw0rd' DEFAULT ROLE sakiladb;

```



## Ref
  * https://www.mysqltutorial.org/mysql-roles/


