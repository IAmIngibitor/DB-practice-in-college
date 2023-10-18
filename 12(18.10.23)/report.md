## №1
```sql
SELECT cus.first_name, cus.last_name FROM customers cus
JOIN orders ord ON cus.customer_id = ord.customer_id
GROUP BY cus.first_name, cus.last_name, ord.order_date
HAVING COUNT(*) >= 2 AND ord.order_date BETWEEN '2023-07-17' AND '2023-10-17'
ORDER BY 1, 2
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/d410e183-854b-4357-bd63-3d1bb1a98c0d)  
  
## №2
```sql
SELECT AVG(ord.quantity) AS average, prd.category FROM orders ord
JOIN products prd ON prd.product_id = ord.product_id
WHERE price >= 50
GROUP BY prd.category
ORDER BY 2
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/64276bf2-a4a2-442a-9db3-6883a2fb95f9)  
  
## №3
```sql
WITH sum_customers AS (
	SELECT ord.customer_id, SUM(prd.price) AS summa FROM orders ord
	JOIN products prd ON prd.product_id = ord.product_id
	GROUP BY ord.customer_id
), avg_sum AS (
	SELECT ord.order_id, ord.customer_id, ord.quantity, SUM(prd.price) AS summa FROM orders ord
	JOIN products prd ON prd.product_id = ord.product_id
	GROUP BY ord.order_id
)

SELECT cus.first_name, cus.last_name, cus.email FROM customers cus
JOIN sum_customers scus ON scus.customer_id = cus.customer_id
JOIN avg_sum asum ON asum.customer_id = cus.customer_id
GROUP BY cus.first_name, cus.last_name, cus.email, scus.summa
HAVING scus.summa > AVG(asum.summa)
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/80c151b7-97bc-425b-a628-ae841e1787f0)  
  
## №4
```sql
WITH sum_price AS (
	SELECT ord.order_id, ord.customer_id, ord.product_id, ord.quantity, SUM(prd.price) AS summa FROM orders ord
	JOIN products prd ON prd.product_id = ord.product_id
	GROUP BY ord.order_id
	HAVING SUM(prd.price) >= 1000
)

SELECT cus.first_name, cus.last_name FROM customers cus
JOIN sum_price spr ON spr.customer_id = cus.customer_id
JOIN products prd ON prd.product_id = spr.product_id
WHERE category != 'Electronics'
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/4f9dbb11-867e-430e-a57b-00624a1bedaf)  
  
## №5
```sql
DROP VIEW IF EXISTS v_avg_order;

CREATE VIEW v_avg_order AS (
	WITH sum_order_id AS (
		SELECT ord.order_id, ord.customer_id, ord.quantity, SUM(prd.price) AS summa FROM orders ord
		JOIN products prd ON prd.product_id = ord.product_id
		GROUP BY ord.order_id
	), avg_sum_customer AS (
		SELECT soid.customer_id, ROUND(AVG(soid.summa), 2) AS avg_summa FROM sum_order_id soid
		GROUP BY soid.customer_id
	), avg_all_sum AS (
		SELECT ROUND(AVG(soid.summa), 2) AS avg_all FROM sum_order_id soid
	)
	
	SELECT cus.first_name, cus.last_name, ascus.avg_summa, (ascus.avg_summa - (SELECT avg_all FROM avg_all_sum)) AS difference FROM avg_sum_customer ascus
	JOIN customers cus ON cus.customer_id = ascus.customer_id
	JOIN sum_order_id soid ON soid.customer_id = ascus.customer_id
	GROUP BY cus.first_name, cus.last_name, ascus.avg_summa
);

SELECT * FROM v_avg_order
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/cba807c1-1fa8-4cbe-b33a-6d6c0b629d26)  
  
## №6
```sql
-- WORK IN PROGRESS

WITH customer_max_min AS (
	SELECT ord.customer_id, MAX(ord.order_date) AS max_date, MIN(ord.order_date) AS min_date FROM orders ord
	GROUP BY ord.customer_id
), range_max_min AS(
	SELECT cusxn.customer_id, (cusxn.max_date - cusxn.min_date) AS range FROM customer_max_min cusxn
)

SELECT cus.first_name, cus.last_name, MAX(ord.order_date), MAX(ord.order_date), MAX(rgxn.range) FROM orders ord
JOIN range_max_min rgxn ON rgxn.customer_id = ord.customer_id
JOIN customers cus ON cus.customer_id = ord.customer_id
GROUP BY cus.first_name, cus.last_name
HAVING (SELECT MAX(rgxn.range) FROM range_max_min rgxn)
```

## №7
```sql

```

## №8
```sql

```

## №9
```sql

```

## №10
```sql

```
