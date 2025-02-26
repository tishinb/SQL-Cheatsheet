## Выделение
```
SELECT * FROM products WHERE price < 3000;
```
```
SELECT * FROM orders WHERE status in ('cancelled', 'new');
```
## Операторы
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

## Добавление

## Обновление

## Удаление
