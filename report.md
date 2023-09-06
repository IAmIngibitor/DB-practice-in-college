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
