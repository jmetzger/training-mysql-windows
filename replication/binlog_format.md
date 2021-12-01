# Binlog format 

## What ? 

```
The binlog format determines how the data is written into the binary log 
```

## Which options ? 

  * STATEMENT (first one in MySQL over development time)  
  * ROW 
  * MIXED

## STATEMEMT

  * The exact statement executed on replicant (master) will be written to binlog 

## ROW 

  * If you execute an update, it will not write the update itself but the results 
  * Example: update last_name = 'Testuser' from sakila.actor where actor > 100 (200 dataset)  
  * In binlog systems writes 100 dataset, each dataset with the exact data for that row 
 
## MIXED 

  * Systems decided if the sql was determenistic 
  * If not -> uses row 
  * if yes -> uses Statement 

## DEFAULT 

   * ROW (safest option) 
