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

<h1 align="center">🚧 [!UNDER CONSTRUCTION!] 🚧</h1>

## Типы данных

**Символьные типы**

- **CHAR**: представляет строку фиксированной длины.

    Длина хранимой строки указывается в скобках, например, CHAR(10) - строка из десяти символов. И если в таблицу в данный столбец сохраняется строка из 6 символов (то есть меньше установленной длины в 10 символов), то строка дополняется 4 пробелами и в итоге все равно будет занимать 10 символов

    Тип CHAR может хранить до 255 байт.

- **VARCHAR**: представляет строку переменной длины.

    Длина хранимой строки также указыватся в скобках, например, VARCHAR(10). Однако в отличие от CHAR хранимая строка будет занимать именно столько места, сколько необходимо. Например, если определенная длина в 10 символов, но в столбец сохраняется строка в 6 символов, то хранимая строка так и будет занимать 6 символов плюс дополнительный байт, который хранит длину строки.

    Всего тип VARCHAR может хранить до 65535 байт.

Начиная с MySQL 5.6 типы CHAR и VARCHAR по умолчанию используют кодировку UTF-8, которая позволяет использовать до 3 байт для хранения символа в зависимости от языка ( для многих европейских языков по 1 байту на символ, для ряда восточно-европейских и ближневосточных - 2 байта, а для китайского, японского, корейского - по 3 байта на символ).

Ряд дополнительных типов данных представляют текст неопределенной длины:

- **TINYTEXT**: представляет текст длиной до 255 байт.

- **TEXT**: представляет текст длиной до 65 КБ.

- **MEDIUMTEXT**: представляет текст длиной до 16 МБ

- **LONGTEXT**: представляет текст длиной до 4 ГБ

**Числовые типы**

- **TINYINT**: представляет целые числа от -128 до 127, занимает 1 байт

- **BOOL**: фактически не представляет отдельный тип, а является лишь псевдонимом для типа TINYINT(1) и может хранить два значения 0 и 1. Однако данный тип может также в качестве значения принимать встроенные константы TRUE (представляет число 1) и FALSE (предоставляет число 0).

    Также имеет псевдоним **BOOLEAN**.

- **TINYINT UNSIGNED**: представляет целые числа от 0 до 255, занимает 1 байт

- **SMALLINT**: представляет целые числа от -32768 до 32767, занимает 2 байтa

- **SMALLINT UNSIGNED**: представляет целые числа от 0 до 65535, занимает 2 байтa

- **MEDIUMINT**: представляет целые числа от -8388608 до 8388607, занимает 3 байта

- **MEDIUMINT UNSIGNED**: представляет целые числа от 0 до 16777215, занимает 3 байта

- **INT**: представляет целые числа от -2147483648 до 2147483647, занимает 4 байта

- **INT UNSIGNED**: представляет целые числа от 0 до 4294967295, занимает 4 байта

- **BIGINT**: представляет целые числа от -9 223 372 036 854 775 808 до 9 223 372 036 854 775 807, занимает 8 байт

- **BIGINT UNSIGNED**: представляет целые числа от 0 до 18 446 744 073 709 551 615, занимает 8 байт

- **DECIMAL**: хранит числа с фиксированной точностью. Данный тип может принимать два параметра precision и scale: DECIMAL(precision, scale).

    Параметр precision представляет максимальное количество цифр, которые может хранить число. Это значение должно находиться в диапазоне от 1 до 65.

    Параметр scale представляет максимальное количество цифр, которые может содержать число после запятой. Это значение должно находиться в диапазоне от 0 до значения параметра precision. По умолчанию оно равно 0.

    Например, в определении следующего столбца:

    ```
    salary DECIMAL(5,2)
    ```

    Число 5 - precision, а число 2 - scale, поэтому данный столбец может хранить значения из диапазона от -999.99 до 999.99.

    Размер данных в байтах для DECIMAL зависит от хранимого значения.
  
    Данный тип также имеет псевдонимы **NUMERIC**, **DEC**, **FIXED**.

- **FLOAT**: хранит дробные числа с плавающей точкой одинарной точности от -3.4028 * 10^38 до 3.4028 * 10^38, занимает 4 байта

    Может принимать форму FLOAT(M,D), где M - общее количество цифр, а D - количество цифр после запятой.

- **DOUBLE**: хранит дробные числа с плавающей точкой двойной точности от -1.7976 * 10^308 до 1.7976 * 10^308, занимает 8 байт. Также может принимать форму DOUBLE(M,D), где M - общее количество цифр, а D - количество цифр после запятой.

    Данный тип также имеет псевдонимы **REAL** и **DOUBLE PRECISION**, которые можно использовать вместо DOUBLE.

**Типы для работы с датой и временем**
- 
**Составные типы**
- 
**Бинарные типы**
- 
