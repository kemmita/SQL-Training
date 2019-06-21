```sql
create proc NameEmployeesProc(@EmployeeNumber int) as
begin
	if exists (select * from tblEmployee where EmployeeNumber = @EmployeeNumber)(
		select EmployeeNumber, EmployeeFirstName, EmployeeLastName
		from tblEmployee where EmployeeNumber = @EmployeeNumber
	) else (
		select 'Employee does not exist.' as DeveloperGeneratedError
	)
end
exec NameEmployeesProc 8
```
