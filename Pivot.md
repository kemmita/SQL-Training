```sql
select employee_id, in_person, online
from
(select employee_id, employee_name, sale_type
from employee_sales) As Source_Table
-- return all names of employees for sale types of in_person and online
PIVOT(
MAX(employee_name)
for sale_type in (in_person,online)
) as pi
```
```
the above would return the emplooyee_id in_person, online columns along with the associated employee names as column values 
[employee_id][in_person][online]
[1          ][Charles  ][NULL  ]
[3          ][NULL     ][Sarah ]
```
