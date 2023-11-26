# SQL INSERT, UPDATE, and DELETE

## Learning Goals

- Use an  `INSERT` statement to add a new table row
- Use an  `UPDATE` statement to change a value in one or more table rows
- Use a `DELETE` statement to delete one or more table rows

## Introduction

SQL provides `INSERT`, `UPDATE`, and `DELETE`  statements to respectively
add, update, and delete a table row.  

We will continue working with the
`pet` table created in the previous lesson:

```sql
CREATE TABLE pet (
	id  INTEGER PRIMARY KEY,
	name TEXT,
	species TEXT,
	breed TEXT,
	age INTEGER
);
```

## INSERT  (Code Along)

The SQL `INSERT` statement adds a new row into a table.
The general syntax is:

```sql
INSERT INTO [table_name] (comma-separated list of column names)
VALUES (comma-separated list of values);
```

We can insert a row into the `pet` table with the statement:

```sql
INSERT INTO pet (id, name, species, breed, age) 
VALUES (1, 'Moe', 'cat', 'Tabby', 10);
```

1. Enter the `INSERT` statement into the query panel.
2. Press the Execute button.
3. Confirm the statement was successful.
4. 
![insert row](https://curriculum-content.s3.amazonaws.com/6036/sql-insert-statement/insert1.png)

The first value  is assigned to the primary key `id`, which must be unique.
If we attempt to execute the same `INSERT` statement again, we see the following
error as the table already contains a pet with id 1:

```text
ERROR:  duplicate key value violates unique constraint "pet_pkey"
DETAIL:  Key (id)=(1) already exists.
SQL state: 23505
```


We can confirm a new row was inserted by executing a `SELECT` statement:

```sql
SELECT *
FROM pet;
```

![Select statement](https://curriculum-content.s3.amazonaws.com/6036/sql-insert-statement/select1row.png)


Let's insert a few more rows into the `pet` table.

```sql
INSERT INTO pet (id, name, species, breed, age) 
VALUES (2, 'Hana', 'cat', 'Tabby', 1);

-- Use two single quotes '' to escape a single quote character in the name
INSERT INTO pet (id, name, species, breed, age) 
VALUES (3, 'Lil'' Bub', 'cat', 'American Shorthair', 5);

INSERT INTO pet (id, name, species, breed, age) 
VALUES (4, 'Snuggles', 'dog', 'Bichon', 5);

--unknown age
INSERT INTO pet (id, name, species, breed)
VALUES (5, 'Honey', 'dog', 'Cavachon');

-- unknown breed
INSERT INTO pet (id, name, species, age)
VALUES (6, 'Herbie', 'fish', 4);
```

- Lil' Bub the cat requires two single quotes between "Lil" and "Bub" to escape the single quote character.
- Honey the dog is not given a value for age.  The value `null` will be stored in that column.
- Herbie the fish is not given a value for breed.  The value `null` will be stored in that column.
- An SQL comment line starts with two dashes -- followed by a space.

The query tool can execute multiple SQL statements.

1. Enter all 5 INSERT statements into the query panel.
2. Press the Execute button to insert the 5 rows.
3. The message should confirm the statement was successful.

![insert 5 rows](https://curriculum-content.s3.amazonaws.com/6036/sql-insert-statement/insert5rows.png)
  
After executing the SQL statements listed above, clear the query panel
to remove the `INSERT` statements:

![clear query](https://curriculum-content.s3.amazonaws.com/6036/sql-select-statement/clearquery.png)

Select Yes to discard the changes.  This does not undo the changes to the table, it simply erases
the changes to the panel editor.

![discard statements](https://curriculum-content.s3.amazonaws.com/6036/sql-select-statement/confirmdiscard.png)


Now we can query the `pet` table to confirm it now contains 6 rows:

![select all rows](https://curriculum-content.s3.amazonaws.com/6036/sql-insert-statement/select6rows.png
)


The INSERT statement does not require the
comma-separated list of column names
if the number of values matches the number of columns.
For example, since the `pet` table contains 5 columns,
we could have written:

```sql
INSERT INTO pet 
VALUES (2, 'Hana', 'cat', 'Tabby', 1);
```

However, it is a good idea to explicitly list the column
names to ensure we provide the values in the correct order.
Also, we must provide the column names if a value
is not provided for one or more columns as was the case
for Honey the dog (unknown age) and Herbie the fish (unknown breed).


## UPDATE

The SQL `UPDATE` statement changes the column value(s) for one or more rows.

The general syntax is:

```sql
UPDATE [table_name] 
SET column_name = value
WHERE [row selection predicate]
```

For example:

```SQL
UPDATE pet
SET age = 7
WHERE id = 5;
```

NOTE: It is very important to ensure the `WHERE` clause is correct, otherwise we might
update the wrong row!    It is a good idea to first write a query using the `SELECT`
statement with the `WHERE` clause to see which rows will be affected.  Do this **before**
executing the `UPDATE` statement:

```SQL
SELECT *
FROM pet
WHERE id = 5;
```

If the `SELECT` shows the correct row to update, then type in the `UPDATE` statement
and execute the `UPDATE`.  

![update age](https://curriculum-content.s3.amazonaws.com/6036/sql-insert-statement/updateage.png)

After every update, select all rows `SELECT * FROM pet`
and confirm the correct row was updated.  It is ok if your row order
differs from what is shown below, as long as the values are the same.

![updated row](https://curriculum-content.s3.amazonaws.com/6036/sql-insert-statement/updatedrow.png)


**Caution** - If the `UPDATE` statement does not have a `WHERE` clause, all rows will be updated!


## DELETE

The SQL `DELETE` statement deletes one or more rows.

The general syntax is:

```sql
DELETE FROM [table_name] 
WHERE [row selection predicate]
```

For example:

```SQL
DELETE FROM pet
WHERE id = 6;
```

Once again, it is a good idea to first write a query using the `SELECT`
statement with the `WHERE` clause to see which rows will be selected.
If the `WHERE` clause picks the correct rows, convert the statement
into a `DELETE` statement.

**Caution** - If the `DELETE` statement does not have a `WHERE` clause, all rows will be deleted!

  
## Conclusion

We've seen how to use SQL's `INSERT`, `UPDATE`, and `DELETE`  statements to respectively
add, update, and delete rows in a table.

## Resources

- [PostgreSQL INSERT](https://www.postgresql.org/docs/current/sql-insert.html)    
- [PostgreSQL DELETE](https://www.postgresql.org/docs/current/sql-delete.html)       
- [PostgreSQL UPDATE](https://www.postgresql.org/docs/current/sql-update.html)  
