## Conditional expressions and procedures

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/sql/sql.html';">**Back to SQL**</button></a>

### CASE

- Similar to if / else statements.

```sql
CASE
	WHEN condition_1 THEN result_1
	WHEN condition_2 THEN result_2
	ELSE some_other_result
END
```

- Example:

```sql
SELECT col_A,
CASE
	WHEN col_A = 1 THEN 'one'
	WHEN col_A = 2 THEN 'two'
	ELSE 'other'
	AS new_col_name
END
FROM table
```

- Case expression syntax:

```sql
CASE expression
	WHEN value_1 THEN result_1
	WHEN value_2 THEN result_2
	ELSE some_other_result
END
```

- Rewriting previous example:

```sql
SELECT col_A,
CASE col_A
	WHEN 1 THEN 'one'
	WHEN 2 THEN 'two'
	ELSE 'other'
END
FROM table
```

```sql
SELECT customer_id,
CASE
	WHEN (customer_id <= 100) THEN 'Premium'
	WHEN (customer_id BETWEEN 100 AND 200) THEN 'Plus'
	ELSE 'Normal'
END
FROM customer
```

```sql
SELECT customer_id,
CASE customer_id
	WHEN 2 THEN 'Winner'
	WHEN 5 THEN 'Second place'
	ELSE 'Loser'
END
FROM customer
```

```sql
SELECT
SUM(CASE rental_rate
	WHEN 0.99 THEN 1
	ELSE 0
END) AS bargains,
SUM(CASE rental_rate
	WHEN 2.99 THEN 1
	ELSE 0
END) AS regular,
SUM(CASE rental_rate
	WHEN 4.99 THEN 1
	ELSE 0
END) AS premium
FROM film
```

### COALESCE

- The ```COALESCE``` function accepts unlimited number of arguments and returns first argument that is not null. If all arguments are null, it returns null.

```sql
COALESCE(price,0)
```

### CAST

- Convert one datatype to another.

- Syntax for CAST function:

```sql
SELECT CAST('5' AS INTEGER)
```

- PostgreSQL CAST operator:

```sql
SELECT '5'::INTEGER
```

```sql
SELECT CAST(date AS TIMESTAMP) FROM table;
```

```sql
SELECT inventory_id,CHAR_LENGTH(CAST(inventory_id AS VARCHAR)) FROM rental
```

### NULLIF

- Takes in two inputs and returns NULL if both are equal, otherwise it returns the first argument passed.

```sql
NULLIF(arg1,arg2)
```

- Lecture example:

```sql
CREATE TABLE depts(first_name VARCHAR(50),department VARCHAR(50));
INSERT INTO depts(first_name,department) VALUES ('Vinton','A'),('Lauren','A'),('Claire','B')
```

- Calculate ratio between male and female members

```sql
SELECT 
SUM(CASE WHEN department = 'A' THEN 1 ELSE 0 END)/
SUM(CASE WHEN department = 'B' THEN 1 ELSE 0 END)
AS department_ratio
FROM depts
```

- The following code gives an error because division by 0:

```sql
SELECT 
SUM(CASE WHEN department = 'A' THEN 1 ELSE 0 END)/
SUM(CASE WHEN department = 'C' THEN 1 ELSE 0 END)
AS department_ratio
FROM depts
```

- Fix:

```sql
SELECT 
SUM(CASE WHEN department = 'A' THEN 1 ELSE 0 END)/
	NULLIF(SUM(CASE WHEN department = 'C' THEN 1 ELSE 0 END),0)
AS department_ratio
FROM depts
```

### VIEWS

