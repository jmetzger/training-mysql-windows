# Training - Grundlagen MySQL Admininstration (Windows)

## Agenda 

  1. Architecture of MySQL 
     * [MySQL Architectur](mysql-architecture.md)
     * [Verarbeitungsschritte Server (Schritte)](/performance/mysql-server-architecture.md)
     * [InnoDB Struktur](innodb/innodb-structure.md)
     * [Storage Engines](/basics/storage-engines.md)
     * [Unterschiede MySQL 5.7 -> 8](differences-mysql-5-7-to-8.md) 
     * [Ort Datenverzeichnis Windows](datadir-windows.md)

  1. Installation 
     * [MySQL auf andere Platte installieren](mysql-d-disk.md)
     * [Start/Status/Stop/Enable von MySQL](start-stop-enable.md)
     * [Lauscht mysql nach draussen ?](/installation/listening-where.md)
     * [2. Instanz von MySQL erstellen](/admin/create-new-instance.md)

  1. Konfiguration 
     * [Konfiguration anpassen und neu starten]()

  1. Datenbank - Objekte 
     * [Databases](database-objects/databases.md)
     * [Tables](database-objects/tables.md)
     * [Events](https://www.mysqltutorial.org/mysql-triggers/working-mysql-scheduled-event/)
     * [Views](database-objects/views.md) 

  1. Administration 
     * [Globale und Session Variablen (Server System Variables)](/admin/global-session-variables.md)
     * [Global and Session Status](basics/status.md) 
     * [Error-log](/admin/log-error.md)
     * [Slow Query Log](/admin/slow-query-log.md)
     * [MySQL - Client - Tools (most important)](basics/mysql-client-tools.md) 
     * [Manage max_connections](max-connections.md)

  1. Backup
     * [Backup mit mysqldump - best practices](backup-restore/mysqldump.md) 
     * [mysqldump through the air ](backup-restore/mysqldump-through-the-air.md)
     * [Backups PIT (Point-In-Time recovery)](backups/pit-recovery.md) 
     * [Backup und Wiederherstellen in neuer Datenbank](backups/backup-restore-to-new-db.md)
     * [mysqldump mit asynchroner Verschlüsselung](backups/mysqldump-with-encryption.md)
     * [mydumper und myloader](https://github.com/maxbube/mydumper)
   
  1. Sicherheit
     * [Absichern von Server/Client mit ssl](security/ssl.md)  
     * [Prüfen ob socket verwendet, bei lokalem System](security/check-socket.md)
     * [mysql_secure_installation - validate plugin aktivieren](security/mysql-secure-installation.md)
     * [general log deaktivieren](/security/disable-general-log.md)
     * [plugin vs. components](/security/plugins-vs-components.md)
     * [User Passwort-Länge und Passwort-Ablauf](users/validation.md)
     * [Trigger ohne Super-Rechte anlegen](trigger-no-super.md)

  1. Sicherheit (CIS) 
     * [1.1 Place Databases on Non-System Partitions](cis/db-non-system-partition.md)
     * [1.2 Use dedicated Least Privileged Account](cis/1-2-least-privileges-user-for-mysl.md)
  
  1. Tools 
     * [Testdatenbank Sakila installieren](tools/sakila.md)  

  1. Performance - Analyse 
     * [Tool pt-query-digest](tools/windows-pt-query-digest.md) 

  1. Authentifizierung / User-Management 
     * [Für User altes Password-Verfahren mysql_native_password verwenden in MySQL 8](user/mysql_native_password.md)
     * [Wildcard-Rechte für Datenbank](user/wildcard-perms-db.md)
     * [Rollen](roles.md)

  1. Replication 
     * [Overview](replication/overview-multi-source.md)
     * [Multi-Source-Replication](replication/multi-source-replication.md)
     * [Binlog format](replication/binlog_format.md)
     * [Change-Replication-Filter](replication/change-replication-filter.md)
     * [What to do on error (sql-thread not running)](replication/what-do-to-on-error.md)
  
  1. Upgrade 
     * [Upgrade von MySQL 5.7 -> 8](upgrade/mysql-5-7-to-8.md)

  1. Windows 
     * [Welchen Benutzer für den Service verwenden?](windows/service-which-user.md)

  1. Tipps & Tricks 
     * [Version von MySQL rausfinden](tipps-tricks/mysql-version.md) 
     * [Show Information_schema within MySQL Workbench](tipps-tricks/mysql-workbench-information_schema)
     * [Set path in Windows for User to easily use mysql](tipps-tricks/mysql-path-windows.md)
     * [Security with outfile mysql](tipps-tricks/security-write-into-outfile.md)

  1. Documentation 
     * [Server System Variables - Reference](https://dev.mysql.com/doc/refman/8.0/en/server-system-variable-reference.html)
     * [MySQL Performance Dokument - en](https://schulung.t3isp.de/documents/pdfs/mysql/mysql-performance.pdf)
    
