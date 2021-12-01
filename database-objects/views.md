# View

## Walkthrough 

```
CREATE VIEW `avorname` AS
    SELECT 
        first_name AS vorname
    FROM
        actor;
        
        
select * from avorname;

# Abfrage 
# das geht nicht -> weil view der Column nicht bekannt ist 
select * from avorname where first_name like 'A%';

# So muss es sein
select * from avorname where vorname like 'A%';
        
        


```
