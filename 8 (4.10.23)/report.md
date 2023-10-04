## №1
```sql
SELECT id FROM menu
EXCEPT ALL
SELECT menu_id FROM person_order
ORDER BY id;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/07908314-b3cc-4f00-b41d-988766f7744f)  
  
## №2
```sql
WITH ids AS (
	SELECT id FROM menu
	EXCEPT ALL
	SELECT menu_id FROM person_order
	ORDER BY id
)
SELECT pizza_name, price, pizzeria.name AS pizzeria_name FROM menu
JOIN pizzeria ON pizzeria_id = pizzeria.id
WHERE menu.id IN (SELECT * FROM ids)
ORDER BY pizza_name, price;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/1ece63ba-3201-4b48-be22-d1050005d220)  
  
## №3
```sql
WITH man AS (
	SELECT pizzeria.name FROM pizzeria
	JOIN person_visits ON pizzeria.id = pizzeria_id
	JOIN person ON person_id = person.id
	WHERE gender = 'male'
), woman AS (
	SELECT pizzeria.name FROM pizzeria
	JOIN person_visits ON pizzeria.id = pizzeria_id
	JOIN person ON person_id = person.id
	WHERE gender = 'female'
)
(SELECT name FROM man EXCEPT ALL SELECT name FROM woman)
UNION
(SELECT name FROM woman EXCEPT ALL SELECT name FROM man)
ORDER BY name;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/dac9a1e8-56fa-421c-a582-190633c0b232)  
  
## №4
```sql
WITH man AS (
	SELECT pizzeria.name FROM pizzeria
	JOIN menu ON pizzeria.id = pizzeria_id
	JOIN person_order ON menu.id = menu_id
	JOIN person ON person_id = person.id
	WHERE gender = 'male'
), woman AS (
	SELECT pizzeria.name FROM pizzeria
	JOIN menu ON pizzeria.id = pizzeria_id
	JOIN person_order ON menu.id = menu_id
	JOIN person ON person_id = person.id
	WHERE gender = 'female'
)
(SELECT name FROM man EXCEPT SELECT name FROM woman)
UNION
(SELECT name FROM woman EXCEPT SELECT name FROM man)
ORDER BY name; 
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/71d76fe4-5772-48a5-bf72-7beba5e97410)  
  
## №5
