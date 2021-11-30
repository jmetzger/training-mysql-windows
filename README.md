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

  1. Konfiguration 
     * [Konfiguration anpassen und neu starten]()

  1. Datenbank - Objekte 
     * [Databases](database-objects/databases.md)
     * [Tables](database-objects/tables.md)

  1. Administration 
     * [Globale und Session Variablen (Server System Variables)](/admin/global-session-variables.md)
     * [Global and Session Status](basics/status.md) 
     * [Error-log](/admin/log-error.md)
     * [Slow Query Log](/admin/slow-query-log.md)
     * [MySQL - Client - Tools (most important)](basics/mysql-client-tools.md) 

  1. Backup
     * [Backup mit mysqldump - best practices](backup-restore/mysqldump.md) 
     * [Backups PIT (Point-In-Time recovery)](backups/pit-recovery.md) 
     * [Backup mit xtrabackup](backups/xtrabackup.md)
     * [Backup mit xtrabackup mit Verschlüsselung](backups/xtrabackup-encrypted.md)
     * [Backup und Wiederherstellen in neuer Datenbank](backups/backup-restore-to-new-db.md)
     * [mysqldump mit asynchroner Verschlüsselung](backups/mysqldump-with-encryption.md)
     * [mydumper und myloader](https://github.com/maxbube/mydumper)
   
  1. Sicherheit
     * [Absichern von Server/Client mit ssl](security/ssl.md) 
     * [Verschlüsselte Backups mit xtrabackup](backups/xtrabackup-encrypted.md) 
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

  1. Authentifizierung / User-Management 
     * [Für User altes Password-Verfahren mysql_native_password verwenden in MySQL 8](user/mysql_native_password.md)
     * [Rollen](roles.md)
  
  1. Upgrade 
     * [Upgrade von MySQL 5.7 -> 8](upgrade/mysql-5-7-to-8.md)

  1. Windows 
     * [Welchen Benutzer für den Service verwenden?](windows/service-which-user.md)

  1. Tipps & Tricks 
     * [Version von MySQL rausfinden](tipps-tricks/mysql-version.md) 
     * [Show Information_schema within MySQL Workbench](tipps-tricks/mysql-workbench-information_schema)

  1. Documentation 
     * [Server System Variables - Reference](https://dev.mysql.com/doc/refman/8.0/en/server-system-variable-reference.html)
     * [MySQL Performance Dokument - en](https://schulung.t3isp.de/documents/pdfs/mysql/mysql-performance.pdf)
    
