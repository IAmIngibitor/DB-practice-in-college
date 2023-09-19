## 1 Задание
### Запрос с условием   
![Снимок экрана 2023-09-05 173834](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/6072d0b5-ef74-4700-a2fa-01ff7320465d)  
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/cf28988f-68d2-4c5c-b7dd-3292d884f2b2)  
## 2 Задание (06.09.23) 
### №1
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/3fe371de-f816-463d-9b04-a484dd19d00e)  
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/4e83ca08-7ce4-457a-ad6f-5c4ce8ee7f78)  
```sql
INSERT INTO "Order_details"(order_detail_id,"Product_id", "Quantity", "Subtotal")
VALUES (1, 4, 2, 2 * (SELECT "Price" FROM "Products" WHERE "Product_id" = 4)),
(1, 1, 5, 5 * (SELECT "Price" FROM "Products" WHERE "Product_id" = 1)),
(2, 3, 4, 4 * (SELECT "Price" FROM "Products" WHERE "Product_id" = 3)),
(2, 5, 1, 1 * (SELECT "Price" FROM "Products" WHERE "Product_id" = 5)),
(2, 3, 2, 2 * (SELECT "Price" FROM "Products" WHERE "Product_id" = 3)),
(3, 7, 5, 5 * (SELECT "Price" FROM "Products" WHERE "Product_id" = 7)),
(4, 5, 3, 3 * (SELECT "Price" FROM "Products" WHERE "Product_id" = 5)),
(4, 12, 7, 7 * (SELECT "Price" FROM "Products" WHERE "Product_id" = 12)),
(4, 13, 2, 2 * (SELECT "Price" FROM "Products" WHERE "Product_id" = 13));
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/35fd552d-634d-475a-9488-718fa9fcbef5)  
### №2  
## Задание 3 (12.09.23)  
### №1  
```sql
INSERT INTO "person"("id", "name", "age","gender", "address")
VALUES (15, 'Kirill', 24, 'male', 'Novosibirsk'),
(16, 'Anton', 54, 'male', 'Moskow'),
(17, 'Maksim', 23, 'male', 'Kazan'),
(18, 'Artem', 14, 'male', 'Samara'),
(19, 'Alise', 25, 'female', 'Novosibirsk');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/908f2593-71ce-4ca5-bf30-a4ce7e34f828)  
  
```sql
INSERT INTO "pizzeria"("id", "name", "rating")
VALUES (12, '888Pizza', '2.3'),
(13, 'Shredder Pizza', '3.8'),
(14, 'Park&Pizza', '4.8'),
(15, 'IL Patio', '2.7'),
(16, 'New York Pizza', '4.1');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/66e560ff-0811-4b4e-9d02-99fe98b84529)  
  
```sql
INSERT INTO "person_order"("id", "person_id", "menu_id","order_date")
VALUES (26, 12, 1, '2022-01-13'),
(27, 13, 4, '2022-01-13'),
(28, 13, 2, '2022-01-13'),
(29, 13, 12, '2022-01-13'),
(30, 14, 16, '2022-01-16');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/d12327bf-e49c-4edd-a70e-869b4a465ac1)  
  
```sql
INSERT INTO "menu"("id", "pizzeria_id", "pizza_name","price")
VALUES (25, 13, 'cheese pizza', 900),
(26, 14, 'pepperoni pizza', 1200),
(27, 15, 'sausage pizza', 950),
(28, 16, 'cheese pizza', 900);
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/9152264f-707e-4dc9-aeac-efd7e60d7b23)  
  
```sql
insert into person_visits values (20, 7, 1, '2022-01-01');
insert into person_visits values (21, 7, 4, '2022-01-01');
insert into person_visits values (22, 8, 6, '2022-01-02');
insert into person_visits values (23, 8, 4, '2022-01-03');
insert into person_visits values (24, 8, 7, '2022-01-04');
insert into person_visits values (25, 9, 16, '2022-01-07');
insert into person_visits values (26, 10, 2, '2022-01-08');
insert into person_visits values (27, 11, 13, '2022-01-08');
insert into person_visits values (28, 11, 5, '2022-01-09');
insert into person_visits values (29, 11, 14, '2022-01-09');
insert into person_visits values (30, 12, 11, '2022-01-01');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/b9a03a41-5252-4003-8e5f-44cd53582477)    
  
### №2
```sql
SELECT "name", "age" FROM "person"
WHERE "address" = 'Kazan';
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/6ef811cd-034d-40b0-b508-3e31bdbe298b)  
  
### №3
```sql
SELECT "name", "age" FROM "person"
WHERE "gender" = 'female'
ORDER BY "name" ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/b5ee5f5e-65da-4a6d-a74f-de80ea2802f6)  
  
### №4
```sql
SELECT "name", "rating" FROM "pizzeria"
WHERE "rating" > 3.5
ORDER BY "rating" ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/10519e79-c194-4766-bce5-45474ae03974)  
  
```sql
SELECT "name", "rating" FROM "pizzeria"
WHERE "rating" BETWEEN 3.5 AND 5
ORDER BY "rating" ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/3f874d6e-2d6a-42d8-b4af-f7d7c2d8ddfc)  
  
### №5
```sql
SELECT "person_id" FROM "person_visits"
WHERE "visit_date" BETWEEN '2022-01-05' AND '2022-01-18';
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/d4fd5a89-1ce8-4939-9077-69f29d098fa3)  
  
### №6
```sql
SELECT "name" FROM "person" WHERE person.id IN
(SELECT "person_id" FROM "person_order" WHERE "menu_id" = 1 OR "menu_id" = 3 OR "menu_id" = 7);
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/99c5f8b9-e881-4f2c-bb62-391a3aa389f5)  
  
### №7
```sql
SELECT EXISTS(SELECT * FROM "person" WHERE "name" = 'Peter');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/1863f1e5-b8c1-4c22-b37b-158f84d50f0c)  
  
```sql
SELECT EXISTS(SELECT * FROM "person" WHERE "name" = 'KEter');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/39efd31d-4d48-44f0-9b54-fa9c99a11eb3)  
  
## 4 Задание (13.09.23)
### №1
```sql
SELECT "id", "pizza_name" FROM "menu" UNION
SELECT "id", "name" FROM "person"
ORDER BY "id", "pizza_name";
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/2540bbc2-9800-4505-8b86-37840ae6bdf0)  
  
### №2
```sql
SELECT "pizza_name" FROM "menu"
UNION
SELECT "name" FROM "person"
ORDER BY "pizza_name";
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/4044b81a-ff34-4429-9c50-e48bd113c93d)  
  
### №3
```sql
SELECT "person_id" FROM "person_order" 
WHERE "order_date" IN (SELECT "visit_date" FROM "person_visits")
ORDER BY "person_id" DESC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/41371702-9d30-4924-b6ef-e0863cd0ce71)  
  
### №4
```sql
SELECT ABS (
	(SELECT COUNT("person_id") FROM "person_order" WHERE "order_date" = '2022-01-07') -
	(SELECT COUNT("person_id") FROM "person_visits" WHERE "visit_date" = '2022-01-07')
);
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/a3297c2c-3d8a-4607-9988-57db48d0f549)  
  
## 5 Задание (19.09.23)
###  №1
```sql
SELECT person.id, person.name, "age", "gender", "address", pizzeria.id, pizzeria.name, "rating" FROM "person", "pizzeria"
ORDER BY person.id ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/cd7852d8-bb8b-4a73-bd1d-ea443e765312)  
  
```sql
SELECT person.id, person.name, "age", "gender", "address", pizzeria.id, pizzeria.name, "rating" FROM "person", "pizzeria"
ORDER BY pizzeria.id ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/fefa7b91-079e-493c-8f94-6b5ca89306e9)  
  
### №2
```sql
SELECT "order_date" AS action_date, "name" FROM "person_order", "person"
WHERE "order_date" IN (SELECT "visit_date" FROM "person_visits") AND person_order.person_id = person.id
ORDER BY "order_date" ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/4c0fbea1-c9ae-4eb2-98bb-0276835a4291)  
  
```sql
SELECT "order_date" AS action_date, "name" FROM "person_order", "person"
WHERE "order_date" IN (SELECT "visit_date" FROM "person_visits") AND person_order.person_id = person.id
ORDER BY "name" DESC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/1d870f57-6463-48bc-8420-67746fd87c88)  
  
### №3
```sql
SELECT "order_date", ("name" || ' (age:' || "age" || ')') AS person_information FROM "person_order"
JOIN "person" ON "person_id" = person.id
ORDER BY "order_date" ASC, "person_information" ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/2bbeb2c0-7cba-499c-b62d-fa2e125be9be)  
  
### №4
```sql
SELECT "order_date", ("name" || ' (age:' || "age" || ')') AS person_information FROM "person_order" NATURAL JOIN "person"
ORDER BY "order_date" ASC, "person_information" ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/cd8babdb-b348-4ff3-ba20-f8a47ca4cb00)  
  
### №5
#### IN
```sql
SELECT "name" FROM "pizzeria"
WHERE "id" NOT IN
(SELECT "pizzeria_id" FROM "person_visits");
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/a98d93c6-aefc-49e5-b91a-4052383de8d6)  
#### EXISTS
```sql
SELECT "name" FROM "pizzeria"
WHERE NOT EXISTS
(SELECT * FROM "person_visits" WHERE pizzeria.id = "pizzeria_id");
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/1f50bcd3-0eba-49fb-998c-c82265eda52f)  
  
### №6
```sql
SELECT person.name AS person_name, menu.pizza_name, pizzeria.name AS pizzeria_name FROM "person_order"
JOIN "person" ON person.id = person_order.person_id
LEFT JOIN "menu" ON menu.id = person_order.menu_id
LEFT JOIN "pizzeria" ON pizzeria.id = menu.pizzeria_id
ORDER BY "person_name", "pizza_name", "pizzeria_name";
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/dccc2a86-0537-4d4b-a9c7-41c9285a34fc)  
  
  

