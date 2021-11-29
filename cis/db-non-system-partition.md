# 1.1 Place Databases on Non-System Partitions 

## Überprüfen, wo das datadir liegt 

```
mysql> select @@datadir;
+----------------------+
| @@datadir            |
+----------------------+
| /var/lib/mysql-data/ |
+----------------------+
1 row in set (0.00 sec)

mysql> show variables like 'datadir';
+---------------+----------------------+
| Variable_name | Value                |
+---------------+----------------------+
| datadir       | /var/lib/mysql-data/ |
+---------------+----------------------+
1 row in set (0.01 sec)
```

## Walkthrough 

```
# /etc/apparmod.d/
vi usr.sbin.mysqld 
# ---> change these lines 
# Allow data dir access
#  /var/lib/mysql/ r,
#  /var/lib/mysql/** rwk,
  /var/lib/mysql-data/ r,
  /var/lib/mysql-data/** rwk,
## <-----

systemctl stop mysql
systemctl restart apparmor 
systemctl status apparmor 
aa-status

# Change config of mysql 
# datadir 
cd /etc/mysql/mysql.conf.d/
vi mysqld.cnf 
# change datadir to /var/lib/mysql-data # on seperate partition 
datadir=/var/lib/mysql-data 

cd /var/lib
cp -a mysql mysql-data  
systemctl restart mysql

# Bei Erfolg ist das Datadir jetzt geändert 
mysql>
show variables like 'datadir';
```

## Debuggen bei Problemen 

```
journalctl -u mysql -e 
/var/log/mysql/error_log 


```
systemctl stop mysql
