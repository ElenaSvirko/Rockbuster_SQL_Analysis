## SQL query searching for duplicates in the film table, which contains information about the films stored in the Rockbuster relational database

```SQL
SELECT title, description, release_year, language_id, length, replacement_cost, rating, COUNT(*)
FROM film
GROUP BY title, description, release_year, language_id, length, replacement_cost, rating 
HAVING COUNT(*) > 1;
```


## SQL query checking for missing values in the customer table, which contains personal information about Rockbuster customers. The first query checks for the values left blank. The second query checks for missing values marked as ‘NA’ within sting (non-numeric) variables. 

```SQL
SELECT * FROM customer
WHERE customer_id IS NULL 
OR store_id IS NULL 
OR first_name IS NULL 
OR last_name IS NULL 
OR email IS NULL 
OR address_id IS NULL 
OR activebool IS NULL 
OR create_date IS NULL 
OR last_update IS NULL 
OR active is NULL;
```

```SQL
SELECT * FROM customer 
WHERE first_name = 'NA' 
OR last_name = 'NA' 
OR email = 'NA';
```
