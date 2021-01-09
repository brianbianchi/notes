
# SQL

## Transactions

One way to safely make changes to your SQL database is by using `transactions`. By wrapping statements in a transaction, you are able to revert your changes, if needed.

### Example
In this example, I wrap a couple of delete statements in a transaction.

```sql
BEGIN tran
SAVE tran point1

DELETE FROM table
WHERE var = 2
SAVE tran point2

DELETE FROM table
WHERE var = 3
SAVE tran point3
```

If you need to revert your changes, `rollback` to a save point.

```sql
rollback tran point1
```
