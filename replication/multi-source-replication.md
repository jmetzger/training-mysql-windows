# Multi-Source-Replication 

## Background 

  * Aggregate multiple sources into one slave 
  * Uses channels (FOR CHANNEL 'replicant-1')

## Walkthrough 

```
-> ON master/replicant:

# 1. create replication user 
# event better IP-Range instead of % -> 192.168.56.% 
CREATE USER repl_multi@'%' identified by 'your_secret_pass'
GRANT REPLICATION SLAVE ON *.* TO 'repl_multi'@'%'

# 2. test connection with that user 
# in our case on same server 
# explicitly host, because that's how we use it in CHANGE MASTER 
mysql -urepl_multi -p -h127.0.0.1 

# 3. Daten auf master ausspielen und master-data notieren 
# CHANGE MASTER steht relativ am Anfang der Datei 
mysqldump --all-databases --single-transaction --source-data=2 --routines --events --flush-logs --delete-source-logs -uroot -p > all-databases.sql

-> ON slave/replica:

# 1. be sure, that server does not have same server_id // server uuid 

# --> Delete auto.cnf in datadir 

# -> change server_id in my.cnf in [mysqld] section to > 1 
# must be unique across all servers in master/slave replications network 
# e.g. 
server_id = 2 

# 2. Restart server (in our case mysql2 is the replica) 
net stop mysql2
net start mysql2

# 3. Import data into slave/replica from master 
# port of our replica is 3308 
mysql -uroot -p --port=3308 -h 127.0.0.1 < all-databases.sql 

# 4. Construct change master -> sql command 
# with master_pos, master_log_file from dump 
# CHANGE MASTER is the same as CHANGE REPLICATION SOURCE 
CHANGE REPLICATION SOURCE TO
SOURCE_HOST='127.0.0.1',
SOURCE_USER='repl_multi',
SOURCE_PASSWORD='password',
SOURCE_LOG_FILE='binlog.000026',
SOURCE_LOG_POS=156
FOR CHANNEL 'replicant-1';

# 5. start replica 
START REPLICA FOR CHANNEL 'replicant-1'

# 6. Check on slave if you succeeded
show replica status; 
# or 
show slave status; 

# look for slave_io_running -> YES  

# look for slave_sql_running -> YES 

# If not look for errors within the output 

```


## Show the state of replication in performance schema 

```
# all slaves 
show slave status;

# specific slave
show slave status for channel 'replicant1';

# more information in performance_schema 
use performance_schema;
select * from performance_schema.replication_connection_status \G
```

