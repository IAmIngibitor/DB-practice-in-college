## 1 Задание
### Запрос с условием   
![Снимок экрана 2023-09-05 173834](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/6072d0b5-ef74-4700-a2fa-01ff7320465d)  
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/cf28988f-68d2-4c5c-b7dd-3292d884f2b2)  
## 2 Задание 
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
## Задание 3  
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

