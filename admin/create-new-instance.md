# Create new Database instance 

## Walkthrough 

```
1. We stop MySQL 

net stop MySQL80 

2. Copy the Instance - Data 
C:\ProgramData\MySQL\MySQL Server 8.0
-> to e.g.
C:\ProgramData\MySQL\MySQL-Instance-2 

3. Change Permission 

Add user "NETWORK SERVICE" with all permissions (beside special per permission) 

4. Adjust my.ini in new folder MySQL-Instance-2 

Adjust:
# to new folder 
datadir=  
# port 
# to new port (not 3306) - must be unused 

5. Open cmd.exe as Administrator 

# then cd to bin-folder of mysql 
cd C:\Program Files\MySQL\MySQL Server 8.0\bin

# install service 
mysqld.exe --install mysql2 --defaults-file=C:\ProgramData\MySQL\MySQL-Instanz-2\my.ini 

6. Go to service and refresh 

7. Go to properties and change user to:

NETWORK SERVICE 
(clear password - lines and press o.k.)

8. Start new service and be happy 

```

## Debugging 

  * Is the path to binary correct in service 
  * Is the defaults-file path correct in service 
  * Is user NETWORK SERVICE added to new folder 
  * Is datadir correct in new my.ini 
  * Is port not same as in old my.ini 


