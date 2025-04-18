## SQL query to calculate descriptive statistics for numeric variables in the film table

```SQL

SELECT COUNT(film_id) AS count_of_movies,
    AVG (rental_duration) AS average_rental_duration,
    MAX(rental_duration) AS maximum_rental_duration,
    MIN(rental_duration) AS minimum_rental_duration,
    AVG (rental_rate) AS average_rental_rate,
    MAX(rental_rate) AS maximum_rental_rate,
    MIN(rental_rate) AS minimum_rental_rate,
    AVG (length) AS average_length,
    MAX(length) AS maximum_length,
    MIN(length) AS minimum_length,
    AVG (replacement_cost) AS average_replacement_cost,
    MAX(replacement_cost) AS maximum_replacement_cost,
    MIN(replacement_cost) AS minimum_replacement_cost
FROM film;

```
## SQL query to find the mode for non-numeric variables in the film table

```SQL
SELECT  
    MODE () WITHIN GROUP (ORDER BY language_id) AS modal_language_id, 
    MODE () WITHIN GROUP (ORDER BY rating) AS modal_rating
FROM film;
```

