# mysqldump mit asynchrones Verschlüsselung 

```
# Asynchrones Schlüsselpaar erstellen 
openssl req -x509 -nodes -newkey rsa:2048 -keyout mysqldump-key.priv.pem -out mysqldump-key.pub.pem

# Öffentlichen Schlüssel Verwenden zum Verschlüsseln 
mysqldump --routines --events --triggers --all-databases | openssl smime -encrypt -binary -text -aes256 -out database.sql.enc -outform DER mysqldump-key.pub.pem

# Entschlüsseln 
openssl smime -decrypt -in database.sql.enc -binary -inform DEM -inkey mysqldump-key.priv.pem -out mysql-backup.sql
mysql < mysql-backup.sql 

```
