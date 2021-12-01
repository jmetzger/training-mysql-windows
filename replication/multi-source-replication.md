# Multi-Source-Replication 

## Background 

  * Aggregate multiple source into one slave 
  * Uses channels (FOR CHANNEL 'replicant-1' 

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

