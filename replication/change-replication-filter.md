# Change Replication Filter 

## Why ? 

  * Allows to ignore db or only replicate specific db's 
  * also possible: different for channel 

## Example 

```
CHANGE REPLICATION FILTER REPLICATE_DO_DB = (dauertest) FOR CHANNEL replicant-1;
CHANGE REPLICATION FILTER REPLICATE_DO_DB = (d1);

```

## Start and Stop the slave (important) 

```
STOP REPLICA SQL_THREAD FOR CHANNEL 'replicant-1';
CHANGE REPLICATION FILTER REPLICATE_DO_DB = (dauerversuche) FOR CHANNEL 'replicant-1';
START REPLICA SQL_THREAD FOR CHANNEL 'replicant-1';
```

## Rausnehmen 

```
STOP REPLICA SQL_THREAD FOR CHANNEL 'replicant-1';
CHANGE REPLICATION FILTER REPLICATE_DO_DB = () FOR CHANNEL 'replicant-1';
START REPLICA SQL_THREAD FOR CHANNEL 'replicant-1';
```

## Reference 

  * https://dev.mysql.com/doc/refman/8.0/en/change-replication-filter.html
