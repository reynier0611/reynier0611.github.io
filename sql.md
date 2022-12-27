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

### Conditional selection

```sql
SELECT column_1, column_2 FROM table WHERE condition;
```

- comparison operators: ```=```, ```>```, ```<```, ```>=```, ```<=```, and ```<>``` or ```!=```.

- logical operators: ```AND```, ```OR```, ```NOT```.

```sql
SELECT name, choice FROM table WHERE name = 'David';
SELECT name, choice FROM table WHERE name = 'David' AND rate > 4;
```

### Ordering

```sql
SELECT col1, col2 FROM table ORDER BY col1 ASC
SELECT col1, col2 FROM table ORDER BY col1 ASC, col2 DESC
```

- Ascending is the default. Order by comes at the end of the query, including after WHERE statements.

### Limiting number of rows return in a query

- LIMIT is the last command to be executed

```sql
SELECT * FROM table ORDER BY payment_date DESC LIMIT 5;
```

- The command below is similar to ```.head()``` in a pandas dataframe:

```sql
SELECT * FROM table LIMIT 5;
```

### BETWEEN

- value BETWEEN low AND HIGH
- the same as value >= low AND value <= high

- can combine with NOT operator: value NOT BETWEEN low AND high
- the same as value < low OR value > high

- Can be used with dates (formatted as ```'2022-12-31'``` or ```'2022-12-31 23:39:11'```)

```sql
SELECT * FROM payment WHERE amount BETWEEN 8 AND 9;
SELECT * FROM payment WHERE amount NOT BETWEEN 8 AND 9;
```

### IN

Check if a value is included in a list of options.

```sql
SELECT color FROM table WHERE color IN ('red','blue')
SELECT color FROM table WHERE color NOT IN ('red','blue')
```

### LIKE and ILIKE

- The LIKE operator allows us to perform pattern matching against string data with the use of wildcard characters:
	- ```%```: matches any sequence of characters
	- ```_``` matches any single character

```sql
SELECT * FROM table WHERE first_name LIKE 'J%' AND last_name NOT LIKE 'S%'
```

- THE ILIKE operator is just like the LIKE operator, but LIKE is case sensitive and ILIKE is case insensitive.
