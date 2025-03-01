# Прогресс

| Ключевые слова | Статус|
|------------------------------------| :---: |
| SELECT FROM                        | ✔️ |
| WHERE                              | ✔️ |
| OR и AND                           | ✔️ |
| ORDER BY                           | ✔️ |
| LIMIT                              | ✔️ |
| OFFSET                             | ✔️ |
| INSERT INTO                        | ✔️ |
| VALUE/VALUES                       | ✔️ |
| SET                                | ✔️ |
| UPDATE                             | ✔️ |
| DELETE                             | ✔️ |
|TRUNCATE                            | ✔️ |
|CREATE TABLE                        | ✔️ |
|DROP TABLE                          | ✔️ |

## Выделение

```
SELECT * FROM products WHERE price < 3000;
```

```
SELECT * FROM orders WHERE status in ('cancelled', 'new');
```

## Операторы OR и AND

```
SELECT * FROM orders WHERE sum > 3000 OR products_count >=3:
```

**Оператор OR, в отличие от AND, объединяет два условия**

**У AND приоритет выполнения выше**

```
SELECT * FROM orders WHERE sum BETWEEN 3000 AND 10000 OR status = 'cancelled';
```

```
SELECT * FROM orders WHERE products_count=2 OR products_count=5 AND status = 'cancelled';
```

```
SELECT * FROM orders WHERE (products_count=2 OR products_count=5) AND status = 'cancelled';
```

**Скобки используются для изменения приоритета операторов**

```
SELECT * FROM orders WHERE status = 'cancelled' AND (sum < 3000 or sum > 10000);
```

```
SELECT name, price FROM products ORDER BY price DESC;
```

```
SELECT * FROM products WHERE price >=5000 ORDER BY price DESC;
```

## Сортировка

```
SELECT name, count, price FROM products WHERE price <= 3000 ORDER BY name;
```

```
SELECT name, count, price FROM products WHERE price <= 3000 ORDER BY name ASC;
```

```
SELECT name, count, price FROM products WHERE price <= 3000 ORDER BY name DESC;
```

**ASC - сортировка по возрастанию (по умолчанию)**

**DESC - сортировка по убыванию**

```
SELECT name, price FROM products WHERE count>0
ORDER BY name LIMIT 6 OFFSET 12;
```

**LIMIT - ограничение количества строк(в данном случае первые 6)**

**OFFSET - смещение, указывает на то, сколько записей нужно пропустить(в данном случае первые 12)**

## Добавление

**Добавление с помощью VALUES:**

```
INSERT INTO orders (id, products, sum) VALUES (6, 3, 3000)
```

```
INSERT INTO products (id, name, count, price) VALUE (8, 'iMac 21', 0, 100100)
```

**Можно использовать как VALUE, так и VALUES**

**Добавление с помощью SET:**

```
INSERT INTO table (field1, field2) VALUES (value1, value2);
```

```
INSERT INTO table SET field1=value1, field2=value2;
```

**Разница между VALUES и SET**

```
INSERT INTO users SET id=10, first_name='Никита', last_name='Петров'
```

**Пакетный режим:**

```
INSERT INTO table (field1, field2)  
VALUES  
    (value1_1, value1_2), 
    (value2_1, value2_2), 
    (value3_1, value3_2);
```

## Обновление/Замена

```
UPDATE users SET salary=salary*1.1 WHERE salary<20000
```

**Умножение на 1.1, значит увеличение на 10%**

```
UPDATE products SET name='iMac' WHERE name = 'IMAC'
```

**NULL – это особое слово в MySQL и в отличии от "cancelled" или "new", его нужно писать без кавычек. 
А чтобы сравнить значение в поле с NULL, нужно использовать не символы равенства (=) и неравенства (<>), 
а специальное выражение IS NULL или IS NOT NULL.**

```
UPDATE orders SET status='new' WHERE status IS NULL
```

```
UPDATE orders SET amount=sum*products_count WHERE amount=0 OR amount IS NULL
```

```
UPDATE products SET price=price*1.05 ORDER BY price desc limit 5
```

**Умножение на 1.05, значит увеличение на 5%**

## Удаление

```
DELETE FROM products WHERE count<1;
```

**Удаление всех строк в таблице:**

```
DELETE FROM users;
```

```
TRUNCATE table users;
```

## Создание таблицы

```
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    column3 datatype,
   ....
);
```

**Например:**

```
CREATE TABLE orders (
    id INT UNSIGNED NOT NULL PRIMARY KEY,
    user_id INTEGER NULL,
    products_count INTEGER NULL,
    sum INTEGER NULL,
    status VARCHAR(20) NULL
);
```

## Удаление таблицы

```
DROP TABLE table_name;
```

<h1 align="center">🚧 [UNDER CONSTRUCTION!] 🚧</h1>

## Типы данных


