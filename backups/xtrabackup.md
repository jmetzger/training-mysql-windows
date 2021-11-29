# xtrabackup 

## Installation 

```
wget https://repo.percona.com/apt/percona-release_latest.$(lsb_release -sc)_all.deb
# installationsquelle werden in /etc/apt/sources.list.d geschrieben 
dpkg -i percona-release_latest.focal_all.deb 
# neue installationsquellen einlesen
apt update
apt search xtrabackup
apt install percona-xtrabackup-80 
```

## Walkthrough 

```
# server version differs to xtrabackup
# xtrabackup 8.0.26 
# mysql-server 8.0.27 

xtrabackup --backup --target-dir /usr/src/backups/ --no-server-version-check
xtrabackup --prepare --target-dir /usr/src/backups/ --no-server-version-check

# altes datenverzeichnis aus dem Weg räumen 
cd /var/lib 
systemctl stop mysql
mv mysql mysql.bkup 

#
xtrabackup --copy-back --target-dir /usr/src/backups/ --datadir=/var/lib/mysql --no-server-version-check
# adjust permission
chown -R mysql:mysql mysql 
chmod -R g=,o= mysql 
systemctl start mysql 
```

## Walkthrough 

```
# server version differs to xtrabackup
# xtrabackup 8.0.26 
# mysql-server 8.0.27 

# important to check if installed 
# and eventually install 
apt search qpress
apt install qpress 

xtrabackup --backup --compress --target-dir /usr/src/backups/ --no-server-version-check
xtrabackup --decompress --target-dir /usr/src/backups/ 
xtrabackup --prepare --target-dir /usr/src/backups/ --no-server-version-check

# altes datenverzeichnis aus dem Weg räumen 
cd /var/lib 
systemctl stop mysql
mv mysql mysql.bkup 

#
xtrabackup --copy-back --target-dir /usr/src/backups/ --datadir=/var/lib/mysql --no-server-version-check
# adjust permission
chown -R mysql:mysql mysql 
chmod -R g=,o= mysql 
systemctl start mysql 
```

## Ref:

  * https://www.percona.com/blog/2020/10/23/mysql-new-releases-and-percona-xtrabackup-incompatibilities/
