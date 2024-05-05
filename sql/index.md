create table elem(
id int unsigned auto_increment,
a char(2) not null,
b char(2) not null,
c char(2) not null,
primary key (id),
key ind_a_b (a,b)
);

insert into elem
values
(1,'Ag','B','C'),
(2,'Au','Be','Co'),
(3,'Al','Br','Cr'),
(4,'Ar','Br','Cd'),
(5,'Ar','Br','C'),
(6,'Ag','B','Co'),
(7,'At','Bi','Ce'),
(8,'Al','B','C'),
(9,'Al','B','Cd'),
(10,'Ar','B','Cd')

commit;

Использование первичного ключа
explain select * from elem where id = 1

Использование индекса
explain select a,b from elem where a = 'Ar' and b = 'B'

Индекс не используется
explain select * from elem where b = 'B'

Принудительное использование индекса
explain select * from elem force index (ind_a_b) order by a,b

Использование индекса в GROUP BY
explain select a, COUNT(1) from elem group by a 

Использование индекса и временной таблицы
explain select  b,count(1) from elem  group by b 


create table elem_names(
sumbol char(2) not null,
name varchar(16) default null,
primary key (sumbol)
);

insert into elem_names
values
('Ag', 'Silver'),
('Al', 'Aluminum'),
('Ar', 'Argon'),
('At', 'Astatine'),
('Au', 'Gold'),
('B', 'Born'),
('Be', 'Beryllium'),
('Bi', 'Bismuth'),
('Br','Bromine'),
('C', 'Carbon'),
('Cd', 'Cadmium'),
('Ce', 'Cerium'),
('Co', 'Cobalt'),
('Cr', 'Chromium')

commit

Соединение таблиц при использовании индекса PK type=eq_ref
explain
select name from elem
join elem_names
on elem.a = elem_names.symbol
where a in ('Ag','Au','At')

Изменился порядок соединения таблиц
explain
select name from elem
join elem_names
on elem.a = elem_names.symbol
where a in ('Ag','Au')


Просмотр объема индексов по таблицам

select
t.table_name,
t.data_length,
t.index_length
from information_schema.tables t
where TABLE_type ='BASE TABLE'
and TABLE_SCHEMA = 'employees'
или
show table status like 'actor%'

data_length - размер индекса первичного ключа
index_length - размер всех вторичных индексов на таблицу


Подсчет размеров индекса
select index_name, sum(stat_value)*@@innodb_page_size 
from mysql.innodb_index_stats
where database_name = 'sakila'
/*and table_name = 'departments'*/
group by index_name 


Перестройка таблиц(первичного ключа)
alter table address ENGINE=INNODB