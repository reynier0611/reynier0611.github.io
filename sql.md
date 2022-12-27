## Structured Query Language (SQL) <img src="img/sql_logo.jpg" width="40" height="40" style="float: right;" />

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> 

```sql
SELECT column_1, column_2 FROM table;
```

- To select all columns from the table (not recommended):

```sql
SELECT * FROM table;
```

### Select distinct (unique) values in a column:

```sql
SELECT DISTINCT column FROM table;
SELECT DISTINCT(column) FROM table;
```

### Count function

```sql
SELECT COUNT(column_1) FROM table;
SELECT COUNT(column_2) FROM table;
SELECT COUNT(*) FROM table;
```

returns number of rows in the table. All the calls above return the same value.

### Combining distinct and count:

```sql
SELECT COUNT(DISTINCT column_1) FROM table;
```

### SELECT WHERE

```sql
SELECT column_1, column_2 FROM table WHERE condition;
```

- comparison operators: ```=```, ```>```, ```<```, ```>=```, ```<=```, and ```<>``` or ```!=```.

- logical operators: ```AND```, ```OR```, ```NOT```.

```sql
SELECT name, choice FROM table WHERE name = 'David';
SELECT name, choice FROM table WHERE name = 'David' AND rate > 4;
```

### ORDER BY

```sql
SELECT col1, col2 FROM table ORDERBY col1 ASC/DESC
```

- Ascending is the default. Order by comes at the end of the query, including after WHERE statements.






