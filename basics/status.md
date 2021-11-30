# Status 

## What for ? 

```
# Counts a number of values, like Com_select (how many selects)
# - since the server runs:
show global variables like 'Com_select';
# - in session && since last flush in session 
show variables like 'Com_select'


```

## flush status 

```
# flushes session status 
# only values that are specific in session, like Com_select 
show variables like 'Com_select';
flush status;
show variables like 'Com_select';

```
