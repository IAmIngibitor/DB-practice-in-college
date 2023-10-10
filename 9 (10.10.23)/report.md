### №1
```sql
CREATE VIEW v_persons_male AS
	SELECT * FROM person 
	WHERE gender = 'male';
CREATE VIEW v_persons_female AS
	SELECT * FROM person 
	WHERE gender = 'female';
SELECT * FROM v_persons_male, v_persons_female
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/37f50157-5e96-4de2-8fdb-35b08d31a2e4)  
  
### №2
```sql
DROP VIEW IF EXISTS v_persons_male, v_persons_female;

CREATE VIEW v_persons_male AS
	SELECT * FROM person 
	WHERE gender = 'male';
CREATE VIEW v_persons_female AS
	SELECT * FROM person 
	WHERE gender = 'female';

SELECT "name" FROM v_persons_male
UNION
SELECT "name" FROM v_persons_female
ORDER BY name;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/cf1d01b8-b619-4b29-a3d8-9e42ed00c37a)  
  
### №3
```sql
DROP VIEW IF EXISTS v_gen_dates;
CREATE VIEW v_gen_dates AS 
	SELECT generate_series('2022-01-01'::timestamp, '2022-01-31', '1 day')::date AS dates;
SELECT dates FROM v_gen_dates
ORDER BY dates;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/bd2363bb-d732-46ef-8d33-c986230a76c3)  
  
### №4
```sql
DROP VIEW IF EXISTS v_gen_dates;

CREATE VIEW v_gen_dates AS 
	SELECT generate_series('2022-01-01'::timestamp, '2022-01-31', '1 day')::date AS dates;
	
SELECT dates FROM v_gen_dates
LEFT JOIN person_visits ON dates = visit_date
WHERE visit_date IS NULL;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/8c9f1001-06fb-48bf-8275-9dc4e375b3d8)  
  
### bonus lvl
```sql
SELECT p1.name AS name1, p2.name AS name2, p1.address FROM person p1
JOIN person p2 ON p1.address = p2.address
WHERE p1.id < p2.id
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/0908752e-6796-4f7d-9ecd-6f924215f07b)  
  
### №5
```sql
DROP VIEW IF EXISTS v_02, v_06, v_symmetric_union;

CREATE VIEW v_02 AS
	SELECT id FROM person_visits
	WHERE visit_date = '2022-01-02';

CREATE VIEW v_06 AS
	SELECT id FROM person_visits
	WHERE visit_date = '2022-01-06';
	
CREATE VIEW v_symmetric_union AS
	(SELECT id FROM v_02 EXCEPT SELECT id FROM v_06)
	UNION
	(SELECT id FROM v_06 EXCEPT SELECT id FROM v_02);

SELECT * FROM v_symmetric_union
ORDER BY id;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/8d84a092-9566-464e-9ac7-3b12d7c075e4)  
  
  
### №6
```sql
DROP VIEW IF EXISTS v_price_with_discount;


CREATE VIEW v_price_with_discount AS
	SELECT person.name, menu.pizza_name, menu.price, round(SUM(menu.price - menu.price * 0.1)) AS discount_price FROM person_order p_r
	JOIN menu ON menu.id = p_r.menu_id
	JOIN person ON p_r.person_id = person.id
	GROUP BY name, pizza_name, price
	ORDER BY name, pizza_name;

SELECT * FROM v_price_with_discount
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/f264d968-d425-449a-8318-721c65524146)  
  
### №7
```sql
DROP MATERIALIZED VIEW IF EXISTS mv_dmitriy_visits_and_eats;

CREATE MATERIALIZED VIEW mv_dmitriy_visits_and_eats  AS
	SELECT pzz.name, menu.pizza_name, menu.price FROM pizzeria pzz
	JOIN menu ON menu.pizzeria_id = pzz.id
	JOIN person_visits p_v ON p_v.pizzeria_id = pzz.id
	JOIN person pr ON pr.id = p_v.person_id
	WHERE pr.name = 'Dmitriy' AND menu.price < 800 AND p_v.visit_date = '2022-01-08';

SELECT * FROM mv_dmitriy_visits_and_eats;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/c03463b5-f838-4474-a14f-fa0dbbd1837a)  
  
### №8
```sql
INSERT INTO person_visits(id, person_id, pizzeria_id, visit_date)
VALUES (20, 9, 3, '2022-01-08')
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/7fdee863-c73c-4e67-8e21-4a438fda21c9)  
  
