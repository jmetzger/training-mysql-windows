# General Log deaktivieren

## Warum ?

  * Wird sehr schnell, sehr groß 
  * Schlecht für die Performance 

## Überprüfung ? 

```
select @@general_log 
# sollte auf 0 stehen 
show variables like 'general_log' 
OFF 

```
