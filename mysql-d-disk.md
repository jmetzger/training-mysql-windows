# MySQL - Install on other disk 

## Walkthrough 

```

# 1. Download installer 

# 2. Run Default installation to C: (with service) without installing service 

# 3. Move installation directory to new destination (e.g. D:\

# 4. Create new service with new destination (config-file) 
# Erstellt den Service
# Rechte muss stimmen / Rechte müssen gleich bleiben 
mysqld.exe --install --defaults-file=D:\mymysqldir\my-defaults.cnf 

# 5. service starten
# oder unter Verwaltung 
net start mysql 

```



```
