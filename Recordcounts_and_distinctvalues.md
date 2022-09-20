# Exercises

Q. How does the output differ when you remove the alias component from the above query?

```sql
SELECT
  COUNT(*)
FROM dvd_rentals.film_list;
-- output: count 997 instead of row_count 997
```

Q. Which actor_id has the most number of unique film_id records in the dvd_rentals.film_actor table?

```sql
SELECT actor_id, 
  COUNT(DISTINCT film_id) AS unique_film_count
FROM dvd_rentals.film_actor
GROUP BY actor_id
ORDER BY 2 DESC
LIMIT 1;

--output actor_id -> 107
```

Q. How many distinct fid values are there for the 3rd most common price value in the dvd_rentals.nicer_but_slower_film_list table?

```sql
SELECT
  COUNT(DISTINCT fid) AS unique_fid,
  price
FROM
  dvd_rentals.nicer_but_slower_film_list
GROUP BY
  price
ORDER BY
  1 DESC;
-- output 323
```

Q. How many unique country_id values exist in the dvd_rentals.city table?

```sql
SELECT
  COUNT(DISTINCT country_id) as unique_countries
FROM
  dvd_rentals.city
-- output 109
```

Q. What percentage of overall total_sales does the Sports category make up in the dvd_rentals.sales_by_film_category table?

```sql
SELECT
  category,
  ROUND(
    100 * total_sales::NUMERIC / SUM(total_sales) OVER (),
    2
  ) AS percentage
FROM dvd_rentals.sales_by_film_category;

```

Q. What percentage of unique fid values are in the Children category in the dvd_rentals.film_list table?

```sql
SELECT
  category,
  ROUND(
    100 * COUNT(DISTINCT fid) :: NUMERIC / SUM(COUNT(DISTINCT fid)) OVER (), 2)  AS percentage
    FROM
      dvd_rentals.film_list
    GROUP BY
      category
    ORDER BY
    category;
-- output 6.02
```
