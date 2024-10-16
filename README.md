# Домашнее задание к занятию "`SQL. Часть 2`" - `Маркин Алексей`

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

---

### Решение 1

```
SELECT CONCAT(staff.first_name, ' ', staff.last_name) AS Manager, city.city AS City, COUNT(customer.customer_id) AS Customer_count 
FROM store 
JOIN staff ON store.manager_staff_id = staff.staff_id 
JOIN address ON store.address_id = address.address_id
JOIN city ON address.city_id = city.city_id 
JOIN customer ON store.store_id = customer.store_id 
GROUP BY store.store_id 
HAVING Customer_count > 300;
```

![Задание 1](https://github.com/Markin-AI/12-4/blob/main/img/1-1.png)

---

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

---

### Решение2

```
SELECT COUNT(film_id) AS Film_count 
FROM film 
WHERE length > (SELECT AVG(length) FROM film);
```

![Задание 2](https://github.com/Markin-AI/12-4/blob/main/img/2-1.png)

---

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

---

### Решение3

```
SELECT DATE_FORMAT(payment_date, '%Y-%M(%m)') AS Payment_month, COUNT(rental_id) AS Rental_count, SUM(amount) AS Total_amount 
FROM payment 
GROUP BY Payment_month 
ORDER BY Total_amount DESC LIMIT 1;
```

![Задание 3](https://github.com/Markin-AI/12-4/blob/main/img/3-1.png)

---