# Storage Engines 

## Warum ?

```
Du triffst die Auswahl:
Wie sollen Deine Daten gespeichert werden
```

## Wie unterscheiden sich die Storage Engines ?

  * In der Performance, Features und anderen Charakteristiken, die Du brauchst 

## Was machen Sie ?

  * Sie sind zuständig für: Speichern und Lesen aller in MySQL Daten 
  * Jede Storage Engine hat:
    * Vor- und Nachteile  
  * Der Server kommuniziert mit den Storage Engines über die storage engine API 
    * Unterschiede kann ich durch das Interface nicht sehen.
    * Die api enthält mehrere Dutzend low-level Funktionen z.B. “Beginne eine Transkation”, “Hole die Zeilen, die diesen Primärschlüssel hat”

## Storage Engine machen folgendes NICHT ....

  * Storage Engines parsen kein SQL
  * Storage Engines kommunizieren nicht miteinander.

## Welches sind die Wichtigsten ?

  * MyISAM
  * InnoDB (Default) 
  * Memory
  * CSV
  * Blackhole (/dev/null)
  * Archive
  * Federated

## In Detail: MyISAM - Storage Engine

```
Feautures/Vorteile/Nachteile 

Tabellen-Locks auf Tabellenebene.
Kein automatisches Data-Recovery
Daten z.B. bei Stromausfall können verloren (bis zu 8 Sekunden)
Kein Transaktionen 
Indizes werden im Arbeitsspeicher vorgehalten

Vorteil: 
Kompakte Datenspeicherung 
Table Scans sind sehr schnell
```

## In Detail: InnoDB - Storage Engine

```
Features

Unterstützt hot backups (wg. Transaktionen)
Transaktionen werden unterstüzt
Foreign Keys werden unterstützt
row-level locking
multi-versioning

indexes referenzieren die Daten über Primärschlüssel 
indexes can quickly get huge in size
→ if size of primary index is not small

Sehr effektives Handling von Daten im Arbeitsspeicher 

```
