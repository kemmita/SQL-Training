```sql
create proc NameEmployeesProc(@EmployeeNumber int) as
begin
	select EmployeeNumber, EmployeeFirstName, EmployeeLastName
	from tblEmployee where EmployeeNumber = @EmployeeNumber
end

exec NameEmployeesProc 141
```
