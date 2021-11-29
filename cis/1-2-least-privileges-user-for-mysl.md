# 1.2. Use Dedicated Least Privileged Account fr MySQL Daemon 

## Check 

```
# simple 
ps aux | grep mysql

# sophistiscated 
ps aux | head -n 1 && ps aux | grep mysql | grep -v grep
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
mysql      18341  0.5 42.4 1842172 426204 ?      Ssl  14:22   0:01 /usr/sbin/mysqld
```
