# Richtigen Dump für Point-In-Recovery (PIT) erstellen

```
# Version 1: mysql ab 8.0.26 
# -> source-data / delete-source-logs 
# -- events - scheduled tasks mit dumpen 
# -- routines - procedures und functions 
# -- flush-logs - neues binary log wird direkt erstellt 
mysqldump --all-databases --events --routines  --source-data=2 --delete-source-logs --flush-logs > /usr/src/all-databases.sql

# Version 2: mysql vor 8.0.26  
# -- events - scheduled tasks mit dumpen 
# -- routines - procedures und functions 
# -- flush-logs - neues binary log wird direkt erstellt 
mysqldump --all-databases --events --routines  --master-data=2 --delete-master-logs --flush-logs > /usr/src/all-databases.sql
```
