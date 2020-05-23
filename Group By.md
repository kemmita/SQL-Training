1. A group by statement must be preceeeded by a an aggregate funciton such as sum, max, etc.
```sql
//below we returned the sum of hours worked per employee, they will be grouped by their last name.
select employee.lname, SUM(works_on.hours) as HoursWorked from employee 
join works_on on (employee.ssn = works_on.essn) group by employee.lname;
```
