# Change Replication Filter 

## Why ? 

  * Allows to ignore db or only replicate specific db's 
  * also possible: different for channel 

## Example 

```
CHANGE REPLICATION FILTER REPLICATE_DO_DB = (d1) FOR CHANNEL channel_1;
CHANGE REPLICATION FILTER REPLICATE_DO_DB = (d1);

```


## Reference 

  * https://dev.mysql.com/doc/refman/8.0/en/change-replication-filter.html
