# InnoDB Table Encryption (MySQL 8) 

## Pre-Loading (before) InnoDB the component 

```
# Create file mysqld.my with the following content
# same location as mysqld 
# in /usr/bin/


# Restart server 
systemctl restart mysql
# If it is empty, it is not loaded 
mysql> select * from keyring_component_status

```
