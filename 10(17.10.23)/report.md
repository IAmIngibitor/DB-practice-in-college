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
