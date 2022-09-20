# Exercises

Q. Which id value has the most number of duplicate records in the health.user_logs table?

```sql
SELECT
  COUNT(*)
FROM dvd_rentals.film_list;
-- output: count 997 instead of row_count 997
```

Q. Which log_date value had the most duplicate records after removing the max duplicate id value from question 1?

```sql
SELECT actor_id, 
  COUNT(DISTINCT film_id) AS unique_film_count
FROM dvd_rentals.film_actor
GROUP BY actor_id
ORDER BY 2 DESC
LIMIT 1;

--output actor_id -> 107
```

Q. Which measure_value had the most occurences in the health.user_logs value when measure = 'weight'?

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

Q. How many single duplicated rows exist when measure = 'blood_pressure' in the health.user_logs? How about the total number of duplicate records in the same table?

```sql
SELECT
  COUNT(DISTINCT country_id) as unique_countries
FROM
  dvd_rentals.city
-- output 109
```

Q. What percentage of records measure_value = 0 when measure = 'blood_pressure' in the health.user_logs table? How many records are there also for this same condition?

```sql
SELECT
  category,
  ROUND(
    100 * total_sales::NUMERIC / SUM(total_sales) OVER (),
    2
  ) AS percentage
FROM dvd_rentals.sales_by_film_category;

```

Q. What percentage of records are duplicates in the health.user_logs table?

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
