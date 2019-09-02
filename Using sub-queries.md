1. We need to use a sub query to figureout which employee will recieve a raise. 
```sql
update EMPs
	set SAL = SAL*1.15
where EMPNO in (select EMPNO from emp_bonus)
```
