1. You can stack tables on top of eachother as long as the columns selected are of the same datatype.
```sql
select ENAME, DEPTNO
	from EMPs
where DEPTNO = 10
union all
select DNAME, DEPTNO from DEPTs
```
