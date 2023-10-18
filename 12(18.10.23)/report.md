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

```

## №6
```sql

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
