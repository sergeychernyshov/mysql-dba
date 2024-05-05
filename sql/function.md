###now() текущая дата и время

select now() as d

###concat() соединяет строковые литералы в одну строку

select CONCAT(a.actor_id,"_", a.first_name) as str from actor a

select CONCAT(a.actor_id,'_', a.first_name) as str from actor a 

###year() извлекате текущий год из даты

select year(now())

###rand() случайное число от 0 до 1

select rand()
Последовательность будет одинаковой если указать параметр
select rand(14)

###str_to_date() преобразование в дату

select str_to_date('03/01/1996 12:00:00 AM', '%m/%d/%Y %h:%i:%s %p') converted

###current_user()  Текущий пользователь
select current_user()

###user() Пользователь предоставленный клиентом
select user()