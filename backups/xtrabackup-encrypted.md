# Encrypted backups with xtrabackup 

## Walkthrough 

```
# use output -> this key as encrypt-key 
openssl rand -base64 24
xtrabackup --backup --target-dir=/usr/src/backups-encrypted --encrypt=AES256 --encrypt-key="yIzl4skb1/Nn/t8g3cuEzpjGoYQQzo9l" --no-server-version-check 
xtrabackup --decrypt=AES256 --encrypt-key="yIzl4skb1/Nn/t8g3cuEzpjGoYQQzo9l" --target-dir=/usr/src/backups-encrypted 
xtrabackup --prepare --target-dir=/usr/src/backups-encrypted 

#
systemctl stop mysql
cd /var/lib
mv mysql mysql.bkup4
# datadir needs to in config of /etc/mysql/ - folders (in one config with category [mysqld]
xtrabackup --copy-back --target-dir=/usr/src/backups-encrypted  --no-server-version-check 
cd /var/lib/
chown -R mysql:mysql mysql
chmod -R g=,o= mysql
systemctl start mysql

```


## Refs:

  * https://www.percona.com/doc/percona-xtrabackup/2.4/backup_scenarios/encrypted_backup.html
  * https://www.percona.com/doc/percona-xtrabackup/LATEST/security/pxb-apparmor.html
