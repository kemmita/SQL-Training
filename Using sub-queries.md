1. We can use a sub query to query the user table with an added predefined condition. 
```sql
select u.Id as userId, u.UserName, u.Email, c.body
from (select * from AspNetUsers where UserName != 'bob') u
join Comments c on u.Id = c.AuthorId
```

2. We need to use a sub query to figureout which employee will recieve a raise. 
```sql
update EMPs
	set SAL = SAL*1.15
where EMPNO in (select EMPNO from emp_bonus)
```
