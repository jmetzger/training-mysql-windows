# PIT (Point-In-Timers) 

## Meta - Weg 

```
# Es ist wichtig, diese Reihenfolge 
1) Spielen ein dump aus:

# --delete-source-logs nur wenn keine master-slave-Replikation
mysqldump --events --routines --flush-logs --source-data=2 --delete-source-logs --all-databases > /usr/src/all-databases 

2) Machen wir Änderungen in der sakral 

use sakila 
insert into actor (last_name,first_name) values (‚Hans‘,’Metzger’);
insert into actor (last_name,first_name) values (‚Hansi‘,’Metzgerei’);
delete from actor where id > 200;

—— 

3) Recovery vor Delete 
1. Rausfinden wann der Fehler aufgetreten ist. 
cd /var/lib/mysql 
mysqlbinlog -vv bin-log.000005 

2. Einschränken des binlogs und in recovery.sql ausspielen
# bei mehreren binlogs im Zeitraum bitte alle angeben 
mysqlbinlog -vv --start-position=156 --stop-position=462 bin-log.000005 > /usr/src/recovery.sql  


3. Vollständigen Dump einspielen 
mysql < /usr/src/all-databases.sql 

4. recovery.sql einspielen 
mysql < /src/src/recovery.sql 

5. Überprüfen, ob die beiden Datensätze wieder da sind .
mysql> use sakila; select * from actor; 

```
