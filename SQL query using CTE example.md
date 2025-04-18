# SQL query using CTE to find the average amount paid by the top 5 customers from the top 10 cities in the top 10 counties

```sql

WITH top_countries_cte (country) AS
        (SELECT D.country 
        FROM customer A 
        INNER JOIN address B ON A.address_id = B.address_id 
        INNER JOIN city C ON B.city_id = C.city_id 
        INNER JOIN country D ON C.country_id = D.country_id 
        GROUP BY D.country 
        ORDER BY COUNT(A.customer_id) DESC
        LIMIT 10),
    top_cities_cte (city) AS
        (SELECT C.city 
        FROM customer A 
        INNER JOIN address B ON A.address_id = B.address_id 
        INNER JOIN city C ON B.city_id = C.city_id 
        INNER JOIN country D ON C.country_id = D.country_id 
        WHERE D.country IN 
            (SELECT * 
            FROM top_countries_cte)
            GROUP BY C.city 
            ORDER BY COUNT(A.customer_id) DESC 
            LIMIT 10),
    top_5_customers_cte (customer_id, customer_first_name, customer_last_name, city, country, total_amount_paid) AS
        (SELECT B.customer_id,
        B.first_name AS customer_first_name, 
        B.last_name AS customer_last_name, 
        D.city, 
        E.country, 
        SUM(A.amount) AS total_amount_paid
        FROM payment A 
        INNER JOIN customer B ON A.customer_id = B.customer_id 
        INNER JOIN address C ON B.address_id = C.address_id 
        INNER JOIN city D ON C.city_id = D.city_id 
        INNER JOIN country E ON D.country_id = E.country_id 
        WHERE D.city IN
            (SELECT * 
            FROM top_cities_cte)
            GROUP BY B.customer_id, B.first_name, B.last_name, D.city, E.country 
            ORDER BY SUM(A.amount) DESC 
            LIMIT 5)
SELECT AVG(total_amount_paid) AS top_customers_average_paid 
FROM top_5_customers_cte;
```
