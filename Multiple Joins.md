```sql
select e.ENAME, d.LOC, d.DNAME, eb.Recieved 
from EMPs e join DEPTs d on e.DEPTNO = d.DEPTNO 
left join emp_bonus eb on e.EMPNO = eb.EMPNO
```
