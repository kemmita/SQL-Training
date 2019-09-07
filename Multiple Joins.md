```sql
select SUM(e.SAL) as TotalSalary, d.LOC as Location, m.Name as ManagerName 
from EMPS e join DEPTs d on e.DEPTNO = d.DEPTNO join MGRs m on e.MGR = m.Id group by d.LOC, m.Name
```
