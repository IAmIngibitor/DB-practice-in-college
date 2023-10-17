## №1
```sql
CREATE INDEX idx_menu_pizzeria_id ON menu(pizzeria_id);
CREATE INDEX idx_person_visits_person_id ON person_visits(person_id);
CREATE INDEX idx_person_visits_pizzeria_id ON person_visits(pizzeria_id);
CREATE INDEX idx_person_order_person_id ON person_order(person_id);
CREATE INDEX idx_person_order_menu_id ON person_order(menu_id);
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/22295f5e-bc7f-4a93-9be7-059b0efe6c2d)  
  
## №2
```sql
SET enable_seqscan = OFF;

EXPLAIN ANALYZE SELECT pizza_name, pizzeria.name AS pizzeria_name FROM menu, pizzeria
WHERE menu.pizzeria_id = pizzeria.id
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/5d55a0ad-6164-407d-9e16-50d0a68e0ec9)  
  
## №3
```sql
CREATE INDEX idx_person_name ON person(name);

EXPLAIN ANALYZE 
SELECT UPPER(name) FROM person;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/cef598aa-f4dd-4243-a0de-49b2f9d8a087)  
  
## №4
```sql
CREATE INDEX idx_person_order_multi ON person_order(person_id, menu_id);

EXPLAIN ANALYZE
SELECT person_id, menu_id,order_date
FROM person_order
WHERE person_id = 8 AND menu_id = 19;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/a9ec42fa-4b5d-4451-b640-048d493684e9)  
  
## №5
```sql
CREATE UNIQUE INDEX idx_menu_unique ON menu(pizzeria_id, pizza_name);

EXPLAIN ANALYZE
SELECT pizzeria_id, pizza_name FROM menu
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/2f2f9707-2ddd-4bf9-89f9-0f01e732b97f)  
  
## №6
```sql
CREATE UNIQUE INDEX idx_person_order_order_date ON person_order(person_id, menu_id) WHERE order_date = '2022-01-01';

EXPLAIN ANALYZE
SELECT person_id, menu_id FROM person_order
WHERE order_date = '2022-01-01'
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/1f0e15db-f5c7-4920-a7dd-4e4b318ccc4a)  
  
## №7
```sql
CREATE INDEX idx_1 ON pizzeria(id, rating);

EXPLAIN ANALYZE
SELECT
    m.pizza_name AS pizza_name,
    max(rating) OVER (PARTITION BY rating ORDER BY rating ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS k
FROM  menu m
INNER JOIN pizzeria pz ON m.pizzeria_id = pz.id
ORDER BY 1,2;
```
BEFORE
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/58cdf710-447e-48fd-a4b7-ece6def72494)  
AFTER
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/05e73017-2299-4f66-965d-649a22c7575d)

