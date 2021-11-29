# Welcher Benutzer unter Windows ? 

## LocalSystem is nicht gut !! 

```
Zu viele Rechte 
```

## Optimal wäre: LocalService 

```
# geht nur auf, wenn applikation und DB-Server auf gleichem Host 
mysqld --install --local-service 

# 
mysqld --remove "ServiceNamen" 

```

## 2. Alternative: NetworkService 

```
Frage: Nimmt der installer diesen beider Installatio

```

## Refs: 

  * https://www.netikus.net/documents/MySQLServerInstallation/index.html?moresecurity.htm


