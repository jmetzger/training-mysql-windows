# Auf welchem Interface lauscht der Server ?

## Wie finde ich das raus ?

```
lsof -i | grep mysql
# localhost means it does NOT listen to the outside now 
# mysqld  5208           mysql   19u  IPv4  56942      0t0  TCP localhost:mysql (LISTEN)
```
