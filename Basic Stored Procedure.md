```sql
create proc NameEmployeesProc as
begin
	select EmployeeNumber, EmployeeFirstName, EmployeeLastName
	from tblEmployee
end

exec [dbo].[NameEmployeesProc]

```
