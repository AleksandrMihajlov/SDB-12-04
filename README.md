# SDB-12-04
SQL. Часть 2 - Aleksandr Mihajlov SYS34  
  
### Задание 1  
  
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.  
  
```sql
select concat(staff.first_name , ' ', staff.last_name), city.city, count(customer.customer_id)
from sakila.store s
join sakila.staff staff on staff.store_id = s.store_id 
join sakila.customer customer on customer.store_id = s.store_id
join sakila.address a on a.address_id = s.address_id 
join sakila.city city on city.city_id = a.city_id
group by staff.staff_id, city.city_id 
having COUNT(customer.customer_id) > 300
```
![alt text](https://github.com/AleksandrMihajlov/SDB-12-04/blob/main/1.png)  
  
### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.
  
```sql
select COUNT(film.title)
from sakila.film film  
where film.`length` > (select AVG(`length`) from sakila.film)
```  
![alt text](https://github.com/AleksandrMihajlov/SDB-12-04/blob/main/2.png)  
  
### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.
  
```sql
select month(payment_date), sum(amount), count(payment_id)
from sakila.payment
group by month(payment_date)
ORDER by sum(amount) desc
limit 1
```  
![alt text](https://github.com/AleksandrMihajlov/SDB-12-04/blob/main/3.png)