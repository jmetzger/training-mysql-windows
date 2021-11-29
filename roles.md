# Rollen (Roles)

## Konzept 

  * Rolen 

## Walkthrough  

```
# Rolle anlegen 
mysql> CREATE ROLE sakiladb 
# Berechtigungen der Rolle zuordnen / alle Berechtigungen für sakila 
mysql> GRANT ALL ON sakila.db TO sakiladb 
# Nutzer anlegen 
mysql> CREATE USER roleuser@localhost identified by 'P@ssw0rd';

# Die Rolle dem Nutzer zugeordnet 
mysql> GRANT sakiladb TO rolesuser@localhost 

# Die Standardrolle festlegen, wenn er sich einloggt 
SET DEFAULT ROLE ALL TO roleuser@localhost

```

## Abgekürzte From 

```
create user roleuser2@localhost identified by 'P@ssw0rd' DEFAULT ROLE sakiladb;

```



## Ref
  * https://www.mysqltutorial.org/mysql-roles/


