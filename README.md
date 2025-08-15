# Домашнее задание к занятию "Расширенные возможности SQL" - Голиков Алексей

---

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Решение 1

```
SELECT CONCAT(s.first_name, ' ', s.last_name) AS Seller, c2.city AS City, COUNT(c.customer_id) AS Customer
FROM staff s
JOIN store s2 ON s2.store_id = s.store_id
JOIN customer c ON c.store_id = s2.store_id
JOIN address a ON a.address_id = s2.address_id
JOIN city c2 ON c2.city_id = a.city_id
GROUP BY s.staff_id, c2.city_id
HAVING COUNT(c.customer_id) > 300;
```

![Скриншот 1](https://github.com/donz-tt/hw-11-4_sql_2/blob/main/img/hw-11.4-1.jpg)

---

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Решение 2

```
SELECT COUNT(film_id) AS films FROM film
WHERE length > (select AVG(length) from film);
```

![Скриншот 2](https://github.com/donz-tt/hw-11-4_sql_2/blob/main/img/hw-11.4-2.jpg)

---

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Решение 3

```
SELECT MONTH(payment_date) AS Month, SUM(p.amount) AS Sum, COUNT(p.rental_id) AS Rents
FROM payment p
GROUP BY MONTH(payment_date)
ORDER BY SUM(p.amount)
DESC LIMIT 1;
```

![Скриншот 3](https://github.com/donz-tt/hw-11-4_sql_2/blob/main/img/hw-11.4-3.jpg)

---

