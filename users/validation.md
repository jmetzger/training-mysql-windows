# Spezialfälle für die Validierung 

## Passwort-Ablauf pro User setzten 

```
# Passwort läuft nach 60 Tagen ab und muss neu gesetzt werden
ALTER USER training@localhost PASSWORD EXPIRE INTERVAL 60 day;
```

  * https://dev.mysql.com/doc/refman/8.0/en/password-management.html

## Läßt sich eine Passwort - Länge pro User festlegen ? 

```
Nein. 
Nur auf Server-Ebene für alle Benutzer möglich (über Validation Komponente) 
```

  * https://dev.mysql.com/doc/refman/8.0/en/validate-password.html
