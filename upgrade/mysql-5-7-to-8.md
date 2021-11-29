# Upgrade MySQL 5.7 -> MySQL 8 

## Walkthrough (Teil 1)

```
# Download repo - apt install package on server
cd /usr/src 
wget https://dev.mysql.com/downloads/repo/apt/
-> mysql-apt..... 

dpkg -i  mysql-apt-config_0.8.20-1_all.deb
# all settings can be like, then select OK 

# Repostände lokal updaten 
apt update 

apt install mysql-shell 

mysqlsh>
JS \c root@localhost

## Probleme mit socket evtl durch unterschiedliche Paketherkünfte (MySQL 5.7 -> MySQL 8) 
MySQL 5.7. kam von Ubuntu und verwendete einen anderen Socket 
MySQL 8 verwendet den socket /var/lib/mysql/mysql.sock 

```

## Anpassen des Socket in Server und Client - Teil 2

```
cd /etc/mysql/mysql.conf.d/mysqld.cnf 
# socket geändert in 
[mysqld]
socket = /var/lib/mysql/mysql.sock 

# Server neu starten und prüfen ob sockt da ist im Verzeichnis 
systemctl restart mysql 
/var/lib/mysql/

# socket geändert für client - config 
cd /etc/mysql/conf.d/mysql.cnf 

# mysql.conf 
[mysql]
socket = /var/lib/mysql/mysql.sock 

# Achtung auch für mysqldump setzten z.B. in Datei 
# client.cnf - neu erstellen 
[client]
socket = /var/lib/mysql/mysql.sock 

```

## Test Script für MySQL Migration aufgerufen 

```
mysqlsh
# Vorne connection, hinten Options 
JS> util.checkForServerUpgrade('root@localhost',{"configPath":"/etc/mysql/my.cnf"})

# Dann Ausgabe sieht ungefähr so aus.
The MySQL server at localhost:33060, version 5.7.31-log - MySQL Community
 
Server (GPL), will now be checked for compatibility issues for upgrade to MySQL
 
8.0.21...
 
1) Usage of old temporal type
 
  No issues found
 
...... 

```

## Ausgabe überprüft, was muss evtl geändert, berücksichtigt werden.

```
z.B. AUTO_CREATE_NO_USER - unkritisch, da in MySQL 8 per default der Fall ist. 
(Es wird bei grants keine user angelegt, wenn diese nicht existieren) 


```

## Sicherung der Datenbank VOR !! Update 

```
mysqldump --all-databases --routines --events > /usr/src/all-database.sql 
# Wenn 0 ausgabe, dann ist das Script erfolgreich durchgelaufen
echo $?
# Zur Sicherheit noch letzte in Dump anschauen
# Hier muss Dump completed stehen
```

## Server stoppen und deinstallieren 

```
systemctl stop mysql 
apt remove mysql-server-5.7 
# alte Abhängigkeiten, die nicht mehr benötigt werden, werden gelöscht
apt autoremove 
```

## Neuen Server installieren und Fehler bereinigen 

```
# mysql-server ist in der Regel die neueste, zur Sicherheit nochmal checken
# mit apt search mysql-server 
apt install mysql-server 

# mysqld.conf behalten !! 

# Wenn server nicht starten Fehler bereinigen
# Analysieren
/var/log/mysql/error.log 

# mysqld.conf entsprechend anpassen 

# danach start probieren, so lange bis es geht !! (fehlerbereinigung -> starten -> fehlerber....)
systemctl start mysqld 

#### Upgrade erfolgt beim Starten in Place sowohl in Installationspackage als auch tar.gz 
```

## Refs:

  * https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-utilities-upgrade.html
