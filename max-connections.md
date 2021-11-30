# Max connections 

## Max Connections default 

```
select @@max_connections;
```
## Error like 

```
Too many connections 

## increase or debug first by using status 
show status like '%max%conn%';
# Variable_name	Value
Connection_errors_max_connections	16
Max_used_connections	3
Max_used_connections_time	2021-11-30 11:01:37



```

## Change in config 

```
# my.ini 
[mysqld]
# or even more 
max_connections = 151 

# restart server 
net stop MySQL80 
net start MySQL80 
```
