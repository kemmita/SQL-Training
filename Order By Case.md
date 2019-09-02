1. We cannot use an if statement in a select statement, so we will need to use a case stataement.
```sql
select JOB, ENAME, SAL 
	from EMPs
order by case when JOB like '%sales%' then COMM else SAL end
```
