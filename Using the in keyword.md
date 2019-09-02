1. Below I wanted to select all of the emps that are in deptartment 10 or 20
```sql
select * from EMPs where DEPTNO in (10,20) and ENAME like '%i%' or JOB like '%er';
```
