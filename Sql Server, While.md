```sql
create procedure whilst(@num int) as
begin
	while(@num > 10)
	begin
		set @num = @num-1
	end
end

exec whilst 2000
```
