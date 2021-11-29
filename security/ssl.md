# SSL - MySQL 

## Teil 1: 1-Weg-Sicherheit (nur auf Server validiert) 

```
Bei MySQL 8 werden Zertfikate in der Regel bereits erstellt. 
Ob ssl funktioniert können wir mit 

mysql>show variables like '%HAVE_SSL%';

# Es funktioniert bereits, allerdings mit den automatisch
# erstellten Zertifikaten

```

### Herausfinden, ob SSL verwendet wird 

```
# auf client auf dem mysql-server
mysql
mysql>status
SSL:			Not in use
Connection:		Localhost via UNIX socket
```

### Bitte das nicht verwenden, weil man damit nicht den Common Name setzen kann

```
sudo mysql_ssl_rsa_setup --uid=mysql
```

### CA (Certificate Authority) und Server-Key erstellen 

```
# On Server - create ca and certificates 
mkdir -p /etc/mysql/ssl
cd /etc/mysql/ssl

# create ca.  
openssl genrsa 4096 > ca-key.pem

# create ca-certificate 
# Common Name: MariaDB CA 
openssl req -new -x509 -nodes -days 365 -key ca-key.pem -out ca-cert.pem

# create server-cert 
# Common Name: MariaDB Server
# Password: --- leave empty ----
openssl req -newkey rsa:2048 -days 365 -nodes -keyout server-key.pem -out server-req.pem

# Next process the rsa - key 
openssl rsa -in server-key.pem -out server-key.pem

# Now sign the key 
openssl x509 -req -in server-req.pem -days 365 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 -out server-cert.pem

```

### Zertifikate validieren  

```
openssl verify -CAfile ca-cert.pem server-cert.pem
```

### Configure Server 
```
# create file 
# /etc/mysql/mysql.cnf.d/mysqld.cnf 
[mysqld]
ssl-ca=/etc/mysql/ssl/ca-cert.pem
ssl-cert=/etc/mysql/ssl/server-cert.pem
ssl-key=/etc/mysql/ssl/server-key.pem
## Set up TLS version here. For example TLS version 1.2 and 1.3 ##
tls_version = TLSv1.2,TLSv1.3

# Set ownership 
chown -vR mysql:mysql /etc/mysql/ssl/

```

### Restart and check for errors 
```
systemctl restart mysql
journalctl -u mysql

```

### Externen user auf server einrichten

```
# Einloggen in mysql-client als root

mysql> create user ext@'%' identified by 'P@ssw0rd';
Query OK, 0 rows affected (0.01 sec)

mysql> grant all on sakila.* to ext@'%';
Query OK, 0 rows affected (0.00 sec)

mysql> alter user ext@'%' REQUIRE SSL;
Query OK, 0 rows affected (0.00 sec)

mysql> select * from user where user = 'ext' \G

ssl_type: ANY
ssl_cipher: 0x
x509_issuer: 0x
x509_subject: 0x
```

### Test on Client (1. Versuch) 

```
# Er verbindet sich per SSL 
# Zertifikatsüberprüfung findet nur auf SERVER statt 
mysql -uext -p -h<ip-des-servers>
mysql> status 
mysql> exit 
# Wir probieren es ohne SSL 
mysql -uext -p -h<ip-des-servers> --ssl-mode=DISABLED 
# Trotz richtigem Passwort 
Enter password: 
ERROR 1045 (28000): Access denied for user 'ext'@'139.59.215.179' (using password: YES)

```

### Client verpflichten ein eigenes Zertifikat zu haben 

```
# auf server als root
mysql>ALTER USER ext@'%' REQUIRE X509

```

### On Client - fails because of missing client certificate  

```
mysql -uext -p -h159.223.23.99
Enter password: 
ERROR 1045 (28000): Access denied for user 'ext'@'139.59.215.179' (using password: YES)
```

## Teil 2: 2-Weg-Sicherheit (auf Server und Client validiert) 

### Client - Zertifikate auf Server erstellen 

  * Wir verwenden die gleiche CA wie beim Server

```
# auf dem Server 
cd /etc/mysql/ssl
# Bitte Common-Name: MariaDB Client 
openssl req -newkey rsa:2048 -days 365 -nodes -keyout client-key.pem -out client-req.pem

# process RSA - Key 
openssl rsa -in client-key.pem -out client-key.pem

# sign certficate with CA 
openssl x509 -req -in client-req.pem -days 365 -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 -out client-cert.pem

```

### Client - Zertifikate validieren 

```
openssl verify -CAfile ca-cert.pem client-cert.pem
```

### Zertifikate für Client zusammenpacken

```
mkdir cl-certs; cp -a client* cl-certs; cp -a ca-cert.pem cl-certs ; tar cvfz cl-certs.tar.gz cl-certs 
```


### Zertifikate auf Client transferieren 

```
scp cl-certs.tar.gz 11trainingdo@<ip-des-clients>:/tmp 
```



### Zertifikate einrichten 

```
# auf client 
mv /tmp/cl-certs.tar.gz /etc/mysql/
cd /etc/mysql; tar xzvf cl-certs.tar.gz 

cd /etc/mysql/cl-certs 
ls -la 


cd /etc/mysql/conf.d 
vi mysql.cnf 
[mysql]
ssl-ca=/etc/mysql/cl-certs/ca-cert.pem
ssl-cert=/etc/mysql/cl-certs/client-cert.pem
ssl-key=/etc/mysql/cl-certs/client-key.pem
```

### Zertifikate testen 

```
# Auf Server überprüfen dass X509 für user eingestellt ist
select user,ssl_type from mysql.user where user='ext'

# Auf Client zum server connecten
# Sollte die Verbindung nicht klappen stimmt auf dem 
# Client etwas mit der Einrichtung nicht
mysql -uext -p -h<ip-des-mysql-servers>
mysql> status 



```
## Ref 

  * https://dev.mysql.com/doc/refman/8.0/en/alter-user.html```
