explain select * from film f where
exists (select 1 from inventory i where i.film_id = f.film_id)

explain select * from actor a
where actor_id in (SELECT actor_id from film_actor fa where fa.film_id = 11)

explain select * from actor a
where actor_id in (
SELECT actor_id from film_actor fa join
film using(film_id)
where title = 'ZHIVAGO CORE')

explain select first_name, last_name
from actor a
join film_actor fa using(actor_id)
join film f using (film_id)
join film_category fc  using (film_id)
join category c  using (category_id)
where c.name = 'Horror'

explain analyze select first_name, last_name
from actor a
join film_actor fa using(actor_id)
join film f using (film_id)
join film_category fc  using (film_id)
join category c  using (category_id)
where c.name = 'Horror'
