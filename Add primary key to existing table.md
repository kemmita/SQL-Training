1. if the column is currently null, we will need to change that.
```sql
alter table DEPTs 
alter column DEPTNO integer not null
```
```sql
alter table DEPTs add primary key (DEPTNO)
```
