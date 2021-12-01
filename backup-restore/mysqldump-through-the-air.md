# mysqldump through the air

```
mysqldump --all-databases --single-transaction --source-data=2 --routines --events --flush-logs --delete-source-logs -uroot -p | mysql -uroot -p --port=3308
```
