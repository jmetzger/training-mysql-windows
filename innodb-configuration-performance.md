# InnoDB Performance Einstellungen 

## innodb_buffer_pool_size 

```
# 
select @@innodb_buffer_pool_size 

# Validieren ob es freien puffer gibt (Seite = Pages à 16 KB)
show status like '%pages_free';
+-------------------------------+-------+
| Variable_name                 | Value |
+-------------------------------+-------+
| Innodb_buffer_pool_pages_free | 39960 |
+-------------------------------+-------+
1 row in set (0.00 sec)

# /etc/mysql/mysql.conf.d/mysqld.cnf
innodb-buffer-pool-size = 8G 

# danach
systemctl restart mysql 

```

## InnoDB - Log file Size 

```
60-120 Minuten an Nutzdaten 
(die noch nicht in die Tablespaces geschrieben wurden) 

Berechnen, wiewiele in 60-120 minuten geschrieben werden 
(am besten in der Peak-Time) 

https://www.percona.com/blog/2008/11/21/how-to-calculate-a-good-innodb-log-file-size/

# Beispiel in /etc/mysql/mysql.conf.d/mysqld.cnf 
innodb_log_file_size = 128M 

# Restart 
systemctl restart mysql 

```

## Innodb - Log buffer size 

```
# ein commit muss reinpassen 
# i.d.R. .o.k. 

show variables like 'innodb_log_buffer_size';
+------------------------+----------+
| Variable_name          | Value    |
+------------------------+----------+
| innodb_log_buffer_size | 16777216 |
+------------------------+----------+
1 row in set (0.00 sec)

```

## innodb_flush_log_at_trx_commit

```
1 - Standard - Nach jedem commit die logs im buffer in das log_file schreiben (innodb_log_buffer -> innodb_log_file)
0 - Weniger schreiben, nur 1x pro Sekunde (es können bis zu 1 Sekunde an Daten verlorgen gehen) 

https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_flush_log_at_trx_commit
```

## Nur Linux: innodb_flush_method 

```
Beste und schnellste Methode hier in der Regel unter Linux:
O_DIRECT 
```
