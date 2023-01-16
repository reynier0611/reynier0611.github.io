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
SELECT payment_date,TO_CHAR(payment_date,'mm-dd-yyyy')
FROM payment;
```

- [Data type formatting functions](https://www.postgresql.org/docs/current/functions-formatting.html)