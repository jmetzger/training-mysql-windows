# Plugin vs. Components 

## Components 
 
  * Abgeschlossene Einheiten
  * MySQL-Server ist ein Komponente
  * Eine weitere Komponenten kann geschrieben werden.
  * Diese kommunziert über einen Service mit der anderen Komponenten 

## Plugins 

  * Server, stellt eine API / bzw. verschiedene bereit 
  * Auf dieses greift das Plugin dann zu 
  * Alles innerhalb der Komponenten MySQL-Server 
  * Oftmals schlecht implementiert 
    * Eigentlich respektiv auf bestimmte apis 
    * In der Realität, scope ist oft auf alle api 
  * Plugin kann alles auslesen 

## Vorteile von Komponentens 

  * Keine Endung mehr beim Laden notwendig 
