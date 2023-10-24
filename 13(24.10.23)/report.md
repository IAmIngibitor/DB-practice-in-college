## №1
```sql
SELECT p.id AS p_id, COUNT(pv.id) AS count_of_visits FROM person p
JOIN person_visits pv ON pv.person_id = p.id
GROUP BY 1
ORDER BY p_id ASC, count_of_visits DESC
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/5e166582-0c9d-4af5-b01b-501508383596)  
  
## №2
```sql
SELECT p.name, COUNT(pv.id) AS count_of_visits FROM person p
JOIN person_visits pv ON pv.person_id = p.id
GROUP BY 1
ORDER BY count_of_visits DESC
LIMIT 4
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/4eee41ae-3cdd-4786-bfe8-808b0b013766)  
  
## №3
```sql
WITH fav_rest_visit AS (
	SELECT pzz.name, COUNT(pv.id) AS count_of_visits FROM pizzeria pzz
	JOIN person_visits pv ON pv.pizzeria_id = pzz.id
	GROUP BY 1
	ORDER BY count_of_visits DESC
	LIMIT 3
), fav_rest_order AS (
	SELECT pzz.name, COUNT(pd.id) AS count_of_orders FROM pizzeria pzz
	JOIN menu ON menu.pizzeria_id = pzz.id
	JOIN person_order pd ON pd.menu_id = menu.id
	GROUP BY 1
	ORDER BY count_of_orders DESC
	LIMIT 3
)

SELECT fro.name, count_of_orders AS count, ('order') AS action_type FROM fav_rest_order fro
UNION
SELECT frv.name, count_of_visits AS count, ('visit') AS action_type FROM fav_rest_visit frv
ORDER BY 3 ASC, 2 DESC
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/e9a1297f-a4bd-45ca-8f7d-be683dcc5a71)  
  
## №4
```sql
WITH fav_rest_visit AS (
	SELECT pzz.name, COUNT(pv.id) AS count_of_visits FROM pizzeria pzz
	JOIN person_visits pv ON pv.pizzeria_id = pzz.id
	GROUP BY 1
	ORDER BY count_of_visits DESC
), fav_rest_order AS (
	SELECT pzz.name, COUNT(pd.id) AS count_of_orders FROM pizzeria pzz
	JOIN menu ON menu.pizzeria_id = pzz.id
	JOIN person_order pd ON pd.menu_id = menu.id
	GROUP BY 1
	ORDER BY count_of_orders DESC
)

SELECT frv.name, (frv.count_of_visits + fro.count_of_orders) AS total_count FROM fav_rest_visit frv
JOIN fav_rest_order fro ON fro.name = frv.name
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/f4aeca12-79f0-422c-bf78-ec6df706d56b)  
  
## №5
```sql
SELECT p.name, COUNT(pv.id) AS count_of_visits FROM person p
JOIN person_visits pv ON pv.person_id = p.id
GROUP BY 1
HAVING COUNT(pv.id) > 3
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/e9689644-ddf0-4ec6-9ecb-75ac52ab5c57)  
  
## №6
```sql
SELECT DISTINCT p.name FROM person p
LEFT JOIN person_order pd ON pd.person_id = p.id
ORDER BY 1
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/3079e06a-5295-48d8-beeb-bc1e29c8dd0e)  
  
## №7
```sql

```

## №8
```sql

```

## №9
```sql

```
