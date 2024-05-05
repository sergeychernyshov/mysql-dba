# Примеры команды DELETE

Удаление строк с условием LIMIT
````
delete from payment p order by p.customer_id LIMIT 10
````

Для удаления строк при массовых ограничениях можно установить параметр FOREIGN_KEY_CHECKS.
Отключает проверку вторичных ключей.

>set  FOREIGN_KEY_CHECKS = 0
````
begin

DELETE from film, film_actor, film_category
using film
join film_actor using (film_id)
join film_category  using (film_id)
left join inventory  using (film_id)
where inventory.film_id is null;

coomit;

set  FOREIGN_KEY_CHECKS = 1;

````