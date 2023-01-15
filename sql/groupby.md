## GROUP BY

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/sql/sql.html';">**Back to SQL**</button></a>

```sql
SELECT category_col, AGG(data_col) FROM table WHERE category_col != 'A' GROUP BY category_col;
```

```sql
SELECT company, SUM(sales) FROM table WHERE GROUP BY company ORDER BY SUM(sales);
```

```sql
SELECT DATE(payment_date),SUM(payment) GROUP BY DATE(payment_date);
```

### HAVING

- Filtering after ```GROUP BY```.

```sql
SELECT company, SUM(sales) FROM table WHERE company != 'Google' GROUP BY company HAVING SUM(sales) > 1000;
```

### AS

Create an alias for a column or result

```sql
SELECT column AS new_name FROM table;
```

The ```AS``` operator gets executed at the very end of a query. We cannot use the alias inside a ```WHERE``` operator.