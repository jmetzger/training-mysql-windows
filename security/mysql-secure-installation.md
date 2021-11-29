# mysql_secure_installation 

## Sicherstellen, dass die Komponente Validate als Passwort-Mechanismus aktiviert wird

```
mysql_secure_installation

und keine root-benutzer von extern erlauben

mysql>
select * from mysql.user where user='root' and host != 'localhost'
    -> ;
Empty set (0.00 sec)

```
