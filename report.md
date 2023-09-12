## 1 Задание
### Запрос с условием   
![Снимок экрана 2023-09-05 173834](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/6072d0b5-ef74-4700-a2fa-01ff7320465d)  
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/cf28988f-68d2-4c5c-b7dd-3292d884f2b2)  
## 2 Задание (06.09.23) 
### №1
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/3fe371de-f816-463d-9b04-a484dd19d00e)  
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/4e83ca08-7ce4-457a-ad6f-5c4ce8ee7f78)  
```
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
```
INSERT INTO "person"("id", "name", "age","gender", "address")
VALUES (15, 'Kirill', 24, 'male', 'Novosibirsk'),
(16, 'Anton', 54, 'male', 'Moskow'),
(17, 'Maksim', 23, 'male', 'Kazan'),
(18, 'Artem', 14, 'male', 'Samara'),
(19, 'Alise', 25, 'female', 'Novosibirsk');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/908f2593-71ce-4ca5-bf30-a4ce7e34f828)  
  
```
INSERT INTO "pizzeria"("id", "name", "rating")
VALUES (12, '888Pizza', '2.3'),
(13, 'Shredder Pizza', '3.8'),
(14, 'Park&Pizza', '4.8'),
(15, 'IL Patio', '2.7'),
(16, 'New York Pizza', '4.1');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/66e560ff-0811-4b4e-9d02-99fe98b84529)  
  
```
INSERT INTO "person_order"("id", "person_id", "menu_id","order_date")
VALUES (26, 12, 1, '2022-01-13'),
(27, 13, 4, '2022-01-13'),
(28, 13, 2, '2022-01-13'),
(29, 13, 12, '2022-01-13'),
(30, 14, 16, '2022-01-16');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/d12327bf-e49c-4edd-a70e-869b4a465ac1)  
  
```
INSERT INTO "menu"("id", "pizzeria_id", "pizza_name","price")
VALUES (25, 13, 'cheese pizza', 900),
(26, 14, 'pepperoni pizza', 1200),
(27, 15, 'sausage pizza', 950),
(28, 16, 'cheese pizza', 900);
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/9152264f-707e-4dc9-aeac-efd7e60d7b23)  
  
```
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
```
SELECT "name", "age" FROM "person"
WHERE "address" = 'Kazan';
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/6ef811cd-034d-40b0-b508-3e31bdbe298b)  
  
### №3
```
SELECT "name", "age" FROM "person"
WHERE "gender" = 'female'
ORDER BY "name" ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/b5ee5f5e-65da-4a6d-a74f-de80ea2802f6)  
  
### №4
```
SELECT "name", "rating" FROM "pizzeria"
WHERE "rating" > 3.5
ORDER BY "rating" ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/10519e79-c194-4766-bce5-45474ae03974)  
  
```
SELECT "name", "rating" FROM "pizzeria"
WHERE "rating" BETWEEN 3.5 AND 5
ORDER BY "rating" ASC;
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/3f874d6e-2d6a-42d8-b4af-f7d7c2d8ddfc)  
  
### №5
```
SELECT "person_id" FROM "person_visits"
WHERE "visit_date" BETWEEN '2022-01-05' AND '2022-01-18';
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/d4fd5a89-1ce8-4939-9077-69f29d098fa3)  
  
### №6
```
SELECT "name" FROM "person" WHERE person.id IN
(SELECT "person_id" FROM "person_order" WHERE "menu_id" = 1 OR "menu_id" = 3 OR "menu_id" = 7);
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/99c5f8b9-e881-4f2c-bb62-391a3aa389f5)  
  
### №7
```
SELECT EXISTS(SELECT * FROM "person" WHERE "name" = 'Peter');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/1863f1e5-b8c1-4c22-b37b-158f84d50f0c)  
  
```
SELECT EXISTS(SELECT * FROM "person" WHERE "name" = 'KEter');
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/39efd31d-4d48-44f0-9b54-fa9c99a11eb3)  
  






