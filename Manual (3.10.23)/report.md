## Задание 1 
### №1
```sql
SELECT * FROM table
```
Возвращает всю указанную таблицу
### №2
```sql
SELECT age FROM students
```
Возвращает указанный столбец ```age``` из таблицы ```students```

## 2 Задание (06.09.23) 
### №1
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
Добавляет записи в таблицу ```Order_details```  
Вложенный запрос ```(SELECT "Price" FROM "Products" WHERE "Product_id" = 1)``` возвращает требуемое значение из другой таблицы
## Задание 3 (12.09.23)  
### №2
```sql
SELECT "name", "age" FROM "person"
WHERE "address" = 'Kazan';
```
Возвращает указанные столбцы с условием, что столбец ```"address"``` в этой записи равен```'Kazan'```
```sql
SELECT "name", "rating" FROM "pizzeria"
WHERE "rating" BETWEEN 3.5 AND 5
ORDER BY "rating" ASC;
```
Оператор ```BEETWEEN value AND value``` указывает промежуток для условия  
```ORDER BY column``` сортирует по указанному столбцу(по умолчанию ```ASC``` - по возрастанию)
### №6
```sql
SELECT "name" FROM "person" WHERE person.id IN
(SELECT "person_id" FROM "person_order" WHERE "menu_id" = 1 OR "menu_id" = 3 OR "menu_id" = 7);
```
Вложенный запрос ```(SELECT "person_id" FROM "person_order" WHERE "menu_id" = 1 OR "menu_id" = 3 OR "menu_id" = 7)``` возвращает записи соответствующие указанным условиям  
Оператор ```IN``` позволяет сравнить одну запись с таблицей записей, которую возвращает вложенный запрос
  
### №7
```sql
SELECT EXISTS(SELECT * FROM "person" WHERE "name" = 'Peter');
```
Функция ```EXISTS()``` возвращает логическое значение true/false
## 4 Задание (13.09.23)
### №1
```sql
SELECT "id", "pizza_name" FROM "menu"
UNION
SELECT "id", "name" FROM "person"
ORDER BY "id", "pizza_name";
```
Оператор ```UNION``` объединяет два запроса в один
### №4
```sql
SELECT ABS (
	(SELECT COUNT("person_id") FROM "person_order" WHERE "order_date" = '2022-01-07')
	-
	(SELECT COUNT("person_id") FROM "person_visits" WHERE "visit_date" = '2022-01-07')
);
```
Функция ```ABS()``` возвращает значение по модулю  
Функция ```COUNT()``` возвращает подсчитанное кол-во записей столбца
## 5 Задание (19.09.23) 
### №3
```sql
SELECT "order_date", ("name" || ' (age:' || "age" || ')') AS person_information FROM "person_order"
JOIN "person" ON "person_id" = person.id
ORDER BY "order_date" ASC, "person_information" ASC;
```
```("name" || ' (age:' || "age" || ')') AS person_information``` возвращает объединение столбцов в одном с указанным форматом
Оператор ```JOIN``` объединяет две таблицы и помещает в одну строку записи с совпадающими полями
### №4
```sql
SELECT "order_date", ("name" || ' (age:' || "age" || ')') AS person_information FROM "person_order" NATURAL JOIN "person"
ORDER BY "order_date" ASC, "person_information" ASC;
``` 
```NATURAL JOIN``` создает соединение на основе общих столбцов в таблицах
### №5
```sql
SELECT "name" FROM "pizzeria"
WHERE "id" NOT IN
(SELECT "pizzeria_id" FROM "person_visits");
```
Условие ```NOT``` инвертирует входные значения   
### №6
```sql
SELECT person.name AS person_name, menu.pizza_name, pizzeria.name AS pizzeria_name FROM "person_order"
JOIN "person" ON person.id = person_order.person_id
LEFT JOIN "menu" ON menu.id = person_order.menu_id
LEFT JOIN "pizzeria" ON pizzeria.id = menu.pizzeria_id
ORDER BY "person_name", "pizza_name", "pizzeria_name";
```
Оператор ```LEFT JOIN``` возвращает все записи с первой таблицы и записи совпадающие со второй  
  
## 6 Задание (20.09.23)
### №1
```sql
SELECT "name", "rating" FROM "pizzeria"
LEFT JOIN "person_visits" ON "pizzeria_id" = pizzeria.id
WHERE "pizzeria_id" IS NULL;
```
```LEFT JOIN``` с условием ```WHERE column IS NULL``` возвращает записи из первой таблицы не совпадающие со второй
### №2
```sql
SELECT missing_date::date FROM generate_series ('2022-01-01'::timestamp, '2022-01-10', '1 day') AS "missing_date"
LEFT JOIN "person_visits" ON "visit_date" = "missing_date"
WHERE "visit_date" IS NULL;
```
Функция ```generate_series('2022-01-01'::timestamp, '2022-01-10', '1 day')``` возвращает таблицу последовательных записей с указанным интервалом от ```'2022-01-01'``` до ```'2022-01-10'``` и шагом ```'1 day'```,
```::timestamp``` указание типа значений
  
### №3
```sql
SELECT COALESCE (person.name, '-') AS person_name, COALESCE (person_visits.visit_date, NULL) AS visit_date, COALESCE (pizzeria.name, '-') AS pizzeria_name 
FROM "person_visits"
RIGHT JOIN "person" ON person.id = person_visits.person_id
FULL JOIN "pizzeria" ON pizzeria.id = person_visits.pizzeria_id
ORDER BY "person_name", "visit_date", "pizzeria_name";
```
Функция ```COALESCE()``` возвращает значения не равные NULL, иначе (если указано) они заменяются на указанный формат
  
### №4
```sql
WITH "m" AS (
	SELECT "missing_date"::date FROM generate_series ('2022-01-01'::timestamp, '2022-01-10', '1 day') AS "missing_date"
)
SELECT "missing_date" FROM "m"
LEFT JOIN "person_visits" ON "visit_date" = "missing_date"
WHERE "visit_date" IS NULL;
```
Выражение ```WITH name AS ()``` позволяет создать временную таблицу используемую только для данного запроса
