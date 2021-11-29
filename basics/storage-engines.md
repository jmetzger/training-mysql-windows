# Storage Engines 

## Why ?

```
Decide:
How to save your data internally 
```

## What do they do ?

  * In charge for: Responsible for storing and retrieving all data stored in MySQL
  * Each storage engine has its:
    * Drawbacks and benefits
  * Server communicates with them through the storage engine API
    * this interface hides differences
    * makes them largely transparent at query layer
    * api contains a couple of dozen low-level functions
      * e.g. “begin a transaction”,
      * “fetch the row that has this primary key”

## What do they not do ?

  * Storage Engines do not parse SQL
  * Storage Engines do not communicate with each other
  * They simply .....
    * They simply respond to requests from the server


## Which are the most important one ?

  * MyISAM
  * InnoDB
  * Memory
  * CSV
  * Blackhole (/dev/null)
  * Archive
  * Partition 
  * (Federated)

## In Detail: MyISAM - Storage Engine

   * table locks
     * Locks are done table-wide
   * no automatic data-recovery
     * you can loose more data on crashes than with e.g. InnoDB
     * you can loose up to 8 seconds of data 
   * no transactions
   * only indices are saved in memory through MySQL
   * compact saving (data is saved really dense)
   * table scans are quick

## In Detail: InnoDB - Storage Engine

### Features
    
  * support hot backups (because of transactions)
  * transactions are supported
  * foreign keys are supported
  * row-level locking
  * multi-versioning



indexes refer to the data through primary keys
indexes can quickly get huge in size
→ if size of primary index is not small
Caching/Indexes
optimized caching:
InnoDB puts Data in Buffer Pool
The Buffer Pool is in memory
Builds hash-indexes to speed up row retrieval
unpacked indexes
indexes are not compressed
because of that →
bigger than in MySQL
