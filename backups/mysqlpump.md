# mysqlpump 

## Nachteile

  * sichert keine Systemtabellen 
  * master-data / source-data geht nicht 

## Parallele Threads konfigurieren 

  * erhöht die Schnelligkeit 
  * Nutzerdaten als Grants ausspielen 

## Nur Nutzer exportieren 

  * mysqlpump --exclude-databases=% --exclude-triggers=% --users

## Parallele Verarbeitung

  * Empfehlung: maximal die Anzahl der Cores  

```
mysqlpump --default-parallelism=2 > /usr/src/all-databases
# with users 
# Including user grants 
mysqlpump --default-parallelism=2 --users > /usr/src/all-databases

```

## Reference 

  * https://www.percona.com/blog/2017/04/17/the-mysqlpump-utility/
