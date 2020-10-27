```sql
CREATE TRIGGER TR_tblTransaction
ON tblTransaction
AFTER DELETE, INSERT, UPDATE
AS
BEGIN
    select * from inserted
	  select * from deleted
END
GO

BEGIN TRANSACTION
INSERT INTO tblTransaction(Amount, DateOfTransaction, EmployeeNumber)
VALUES(123, '2020-02-12', 123)
ROLLBACK TRANSACTION
```
