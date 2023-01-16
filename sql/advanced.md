## Advanced topics

<a><button name="button" style = "color:red;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io';">**Back to Table of Content**</button></a> <a><button name="button" style = "color:blue;width:200px;height:30px;cursor:pointer" onclick="window.location.href='https://reynier0611.github.io/sql/sql.html';">**Back to SQL**</button></a>


### Timestamps

- ```TIME``` - contains only time
- ```DATE``` - contains only date
- ```TIMESTAMP``` - contains date and time
- ```TIMESTAMPZ``` - contains date, time, and timezone

##### Functions and operations

- ```TIMEZONE```
- ```NOW```
- ```TIMEOFDAY```
- ```CURRENT_TIME```
- ```CURRENT_DATE```

```sql
SHOW ALL
```

```sql
SHOW TIMEZONE
```

- To get your current timestamp

```sql
SELECT NOW()
```

- The same, but as a string

```sql
SELECT TIMEOFDAY()
```

- Similarly use ```CURRENT_TIME``` and ```CURRENT_DATE```

### EXTRACT

- allows you to extract a sub-component of a date value:
	- ```YEAR```
	- ```MONTH```
	- ```DAY```
	- ```WEEK```
	- ```QUARTER```

```sql
EXTRACT(YEAR FROM date_col)
```

here's an actual example:

```sql
SELECT EXTRACT(YEAR FROM payment_date)
AS new_col_name_if_wanted
FROM payment
```

### AGE

- calculates and returns the current age given a timestamp

```sql
AGE(date_col)
```

here's an actual example

```sql
SELECT AGE(payment_date)
FROM payment;
```

### TO_CHAR

- general function to convert data types to text
- useful for timestamp formatting

```sql
TO_CHAR(date_col,'mm-dd-yyyy')
```

here's an actual example:

```sql
SELECT payment_date,TO_CHAR(payment_date,'mm-dd-yyyy') FROM payment;
```

- [Data type formatting functions](https://www.postgresql.org/docs/current/functions-formatting.html)

### Mathematical functions and operators

- [Documentation](https://www.postgresql.org/docs/9.5/functions-math.html)

```sql
SELECT ROUND(rental_rate/replacement_cost,2)*100 FROM film;
```

### String functions and operators

- [Documentation](https://www.postgresql.org/docs/10/functions-string.html)

```sql
SELECT first_name || ' ' || last_name FROM customer;
```

```sql
SELECT LOWER(LEFT(first_name,1) || last_name) || '@gmail.com' FROM customer;
```

### Sub-query

```sql
SELECT AVG(grade) FROM test_scores;
```

```sql
SELECT student, grade FROM test_scores
WHERE grade > (SELECT AVG(grade) FROM test_scores)
```

```sql
SELECT student, grade FROM test_scores
WHERE student IN (SELECT student FROM honor_roll_table)
```

- Here's a complex example with joins, order bys, and subqueries.

```sql
SELECT film_id, title
FROM film
WHERE film_id IN
(SELECT film_id FROM rental INNER JOIN inventory
ON rental.inventory_id = inventory.inventory_id
WHERE return_date BETWEEN '2005-05-29'
AND '2005-05-30')
ORDER BY title
```

#### EXISTS

- This operator is used to test for the existence of rows in a subquery. Typiccally a subquery is passed to the ```EXISTS()``` function to check if any rows are returned with the subquery.

```sql
SELECT col_name FROM table_name
WHERE EXISTS(SELECT column_name FROM table_name WHERE condition)
```

- People who have at least one payment of more than $11:

```sql
SELECT first_name, last_name FROM customer
AS c
WHERE EXISTS
(SELECT * FROM payment AS p
WHERE p.customer_id = c.customer_id
AND amount > 11)
```

- the opposite can be achieved adding the ```NOT``` operator:

```sql
SELECT first_name, last_name FROM customer
AS c
WHERE NOT EXISTS
(SELECT * FROM payment AS p
WHERE p.customer_id = c.customer_id
AND amount > 11)
```

### Self-Join:

- Join of two copies od the same table

```sql
SELECT tableA.col, TableB.col
FROM table AS tableA JOIN table AS tableB
ON tableA.some_col = tableB.other_col
```

```sql
SELECT f1.title, f2.title, f1.length
FROM film AS f1 INNER JOIN film AS f2
ON f1.film_id != f2.film_id
AND f1.length = f2.length
AND f1.length = 117
```