# Примеры команд SELECT

````
имена таблиц в MySQL могут быть регистрозависимые и нерегистрозависимые.
это зависит от ОС на которой MySQL рпзвернут.
в Lunux имена таблиц регистрозависимые!!!
````

Поиск по тексту происходит независимо от регистра
````
select * from(
select 'ANNE' as c1, lower('ANNE') as c2 ) s
where s.c1 = s.c2

SELECT first_name FROM actor
where first_name = 'ANNE';

SELECT first_name FROM actor
where first_name = lower('ANNE');
````

Ограничить число строк вывода команды SELECT можно при помощи
нестандартной конструкции LIMIT.
Команда покажет первые 3 результата запроса
>SELECT first_name FROM actor limit 3

Конструкция ```limit 2,3``` выведет 3 строки, пропустив 2 строки.
Первый параметр указывает количество строк, которые нужно пропустить.
Второй параметр количество строк для вывода. 
>SELECT first_name FROM actor order by 1 limit 2,3

Аналогичный запрос
>SELECT first_name FROM actor order by 1 limit 3 offset 2

Конструкция соединения таблиц inner join в случае если столбцы названы одинаково
может выглядеть так
````
select c.city, c2.country 
from city c
inner join country c2 using (country_id)
where c2.country_id < 5
ORDER by country, city
````
Аналогичный запрос
````
select c.city, c2.country 
from city c
inner join country c2 
on c.country_id = c2.country_id 
where c2.country_id < 5
````

Сортировка с указанием порядка
````
select * from actor a
order by last_update COLLATE latin1_german1_ci
````

Объединение строк
````
(select a.first_name from actor a where a.actor_id = 5)
union
(select a.first_name from actor a where a.actor_id > 190)
order by FIRST_NAME limit 4
````

````
(select a.first_name from actor a where a.actor_id = 5)
union
(select a.first_name from actor a where a.actor_id > 190 or a.actor_id = 5)
````

````
(select a.first_name from actor a where a.actor_id = 5)
union all
(select a.first_name from actor a where a.actor_id > 190 or a.actor_id = 5)
````

Натуральное соединение производится по полям с одинаковыми названиями
````
select ai.first_name, ai.last_name, fa.film_id
from actor_info ai natural join film_actor fa 
````
Запрос с объединенными предикатами
````
select first_name ,last_name 
from employees e , titles t 
where (e.emp_no, first_name, last_name, title) =
(t.emp_no, 'Marjo', 'Giarratana', 'Senior Staff')
````
или
````
select first_name ,last_name 
from employees e , titles t 
where e.emp_no = t.emp_no
and first_name = 'Marjo'
and last_name = 'Giarratana'
and title = 'Senior Staff'
````
Коррелированный подзапрос
````
select count(1) 
from film f 
where 
	EXISTS (
		select inventory.film_id 
		from inventory 
		where inventory.film_id = f.film_id  
		GROUP by inventory.film_id
		HAVING COUNT(1) >= 2) 
````
