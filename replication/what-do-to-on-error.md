# What do to on error ? 

## Situation 

```
# Auf dem slave/replica 
show slave status;

# Wir sehen 
slave_sql_running -> no

# And we will see an
# and it show us at which place the error occured 
# binlog -> and binlog_pos 
Last_SQL_Error 
```

## Troubleshoot 

```
# We look into the binlog in the master for this channel 
# and have a look what it did there 

# cmd.exe
# cd <data-directory>
mysqlbinlog -vv bin-log.0000026 | more 

# So now we look at the command which should have executed 
# and also look, if the next would be o.k. 
# Example 
# Command 1: CREATE DATABASE dauertest 
# .. but this database already exists on slave 
# Command 2: SET GIT... would be o.k. 

# Go back to slave 
STOP SLAVE FOR CHANNEL 'your-channel' 
# so we skip one binlog / relaylog -entry 
SET GLOBAL sql_slave_skip_counter = 1 
START SLAVE FOR CHANNEL 'your-channel' 

# Doublecheck if it is running 
SHOW REPLICA STATUS 

# now -> should be
# io_thread_running = YES  
# sql_thread_running = YES 
```

## IMPORTANT 

```
If it struggles with the next error,
DO NOT PROCEED LIKE so.
But re-setup the slave 

-> Because slave it completely messed up <--

```
