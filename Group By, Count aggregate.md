1. Below we query two tables to return the numvber of books written per each author.
```sql
select COUNT(books.title) as NumberOfBooks, author.name from books join author on(author.id = books.authorid) group by author.name;
```
