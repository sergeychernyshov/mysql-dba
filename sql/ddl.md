alter table actor rename  column last_update to last_updated

alter table actor change last_updated last_updated_time timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP

alter table actor add index idx_first_name(first_name)

alter table actor drop index idx_first_name

alter table actor add primary key (actor_id)

alter table actor drop primary key

alter table actor rename to actor2

rename table actor2 to actor

create table t1(a smallint)

create table t2(a smallint)

drop table t1,t2

create table t1(a smallint)

create table t2(a smallint)

drop table if exists t1,t2

Создать копию таблицы без данных
>create table employees2 like employees

Создать кипию таблицы с данными
>create table employees3 as select * from employees

Создать таблицу с другими полями
````
create table report2( title varchar(128), category varchar(128))
select first_name as title, last_name as category from employees
````

Создать таблицу и заполнить данные запросом
````
CREATE TABLE `employees4` (
`emp_no` int NOT NULL,
`birth_date` date NOT NULL,
`first_name` varchar(14) NOT NULL,
`last_name` varchar(16) NOT NULL,
`gender` enum('M','F') NOT NULL,
`hire_date` date NOT NULL,
PRIMARY KEY (`emp_no`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
select * from employees
````