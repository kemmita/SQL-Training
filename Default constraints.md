1. A defualt constraint can be set to a column in the chance the data is not submitted for the column in question.
2. If data is not submitted for an employees salary, 1000 will be applied as default
```sql
alter table EMPs add constraint baseSAL default 1000 for SAL
```

