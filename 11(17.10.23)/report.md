## №1
```sql
create table person_discounts
(id bigint primary key ,
 person_id bigint not null ,
 pizzeria_id bigint not null ,
 discount numeric not null ,
 constraint uk_person_discounts unique (person_id, pizzeria_id, discount),
 constraint fk_person_discounts_person_id foreign key  (person_id) references person(id),
 constraint fk_person_discounts_pizzeria_id foreign key  (pizzeria_id) references pizzeria(id));
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/e19b9576-2344-4ec6-90db-48899068d051)  
  
## №2
```sql
DROP VIEW aoo;
CREATE VIEW aoo AS (
	WITH disc AS (
	SELECT pr.person_id, menu.pizzeria_id FROM person_order pr
	JOIN menu ON menu.id = pr.menu_id)
	 SELECT person_id, pizzeria_id, COUNT(*) AS amount_of_orders FROM disc
	 GROUP BY person_id, pizzeria_id
	 ORDER BY 1
);

INSERT INTO person_discounts(id, person_id, pizzeria_id, discount)
SELECT ROW_NUMBER() OVER (ORDER BY 1), person_id, pizzeria_id,
CASE
	WHEN (SELECT amount_of_orders) = 1 THEN 10.5
	WHEN (SELECT amount_of_orders) = 2 THEN 22
	ELSE 30
END AS discount FROM aoo;

SELECT * FROM person_discounts
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/680f85fd-51e4-4163-baf6-548f5bb4c1a4)  
  
## №3
```sql
SELECT p.name, menu.pizza_name, menu.price, ROUND(SUM(menu.price - ((menu.price / 100) * pd.discount))) AS discount_price, pz.name FROM person_discounts pd
JOIN person p ON p.id = pd.person_id
JOIN menu ON menu.pizzeria_id = pd.pizzeria_id
JOIN pizzeria pz ON pz.id = pd.pizzeria_id
GROUP BY p.name, menu.pizza_name, menu.price, pz.name
ORDER BY 1
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/5cb0b133-62b6-463d-ab81-0dbe144491b3)  
  
## №4
```sql
DROP INDEX IF EXISTS idx_person_discounts_unique;
CREATE UNIQUE INDEX idx_person_discounts_unique ON person_discounts(person_id, pizzeria_id);

EXPLAIN ANALYZE
SELECT p.name, menu.pizza_name, menu.price, ROUND(SUM(menu.price - ((menu.price / 100) * pd.discount))) AS discount_price, pz.name FROM person_discounts pd
JOIN person p ON p.id = pd.person_id
JOIN menu ON menu.pizzeria_id = pd.pizzeria_id
JOIN pizzeria pz ON pz.id = pd.pizzeria_id
GROUP BY p.name, menu.pizza_name, menu.price, pz.name
ORDER BY 1
```
#### BEFORE
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/4c381f45-0d1f-40fd-8e6a-cc7336c1ca2c)  
#### AFTER
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/505ca03f-5888-4b80-a104-291c784b9bc7)
  
## №5
```sql
DROP TABLE person_discounts;
create table person_discounts
(id bigint primary key ,
 person_id bigint not null ,
 pizzeria_id bigint not null ,
 discount numeric not null default 0 CHECK(discount >= 0 AND discount <= 100),
 constraint uk_person_discounts unique (person_id, pizzeria_id, discount),
 constraint fk_person_discounts_person_id foreign key  (person_id) references person(id),
 constraint fk_person_discounts_pizzeria_id foreign key  (pizzeria_id) references pizzeria(id));
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/dbec7ba0-e004-4ee1-b27d-a01cb9debe73)  
## №6
```sql
COMMENT ON TABLE person_discounts IS 'Table is useless for me'
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/6ae987b3-4356-4929-b5a4-7de4b5479fc8)
  
## №7
```sql
DROP SEQUENCE IF EXISTS seq_person_discounts;
CREATE SEQUENCE seq_person_discounts
MINVALUE 1 START WITH 1 INCREMENT BY 1;

SELECT setval('seq_person_discounts', (SELECT COUNT(*) FROM person_discounts))

ALTER TABLE person_discounts ALTER COLUMN id SET DEFAULT NEXTVAL('seq_person_discounts');

INSERT INTO person_discounts(person_id, pizzeria_id, discount)
VALUES (3, 1, 0),
		(2, 4, 0);
	
SELECT * FROM person_discounts
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/59fc6170-8a5b-43a8-82a0-15ae5c646100)
