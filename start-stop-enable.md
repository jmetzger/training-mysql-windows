# Starten,stopppen und aktivieren von MySQL

## start/stop/status 

```
# als root - Benutzer
systemctl status mysql
systemctl stop mysql 
systemctl start mysql 
```

## Aktivieren/Deaktivieren (enable/disable) 

```
# Automatischen Starten nach dem Booten (enable) 
systemctl enable mysql 

# is dienst aktiviert 
systemctl is-enabled mysql

# deaktivieren
systemctl disable mysql 
systemctl is-enabled mysql 

# systemctl status -> Zeile disabled/enabled 


```
