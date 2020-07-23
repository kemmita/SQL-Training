1. A view is like a custom/virtual table, consisting of multiple tables. We will define its architecture below. 
```sql
create view vUserComment
as
select u.Id as userId, u.UserName, u.Email, c.body
from AspNetUsers u
join Comments c on u.Id = c.AuthorId
```
2. Once you have created the view, you can query it as a normal table.
```sql
select count(Body) as BodyCount, userId from vUserComment group by userId
```
