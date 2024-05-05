Запросы для определения блокировок
````
select * from performance_schema.data_locks

select * from performance_schema.data_lock_waits
````


Данные для тестов
````
CREATE TABLE `elem` (
  `id` int unsigned NOT NULL AUTO_INCREMENT,
  `a` char(2) NOT NULL,
  `b` char(2) NOT NULL,
  `c` char(2) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `ind_a` (`a`)
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci


insert into elem
values 
(2,'Au','Be','Co'), 
(5,'Ar','Br','C');

commit;
````
1.1)
>set SESSION TRANSACTION   isolation level  REPEATABLE READ

Для уровня изоляции REPEATABLE READ 
При обновлении данных по интервалу ````BETWEEN 2 and 5```` происходит блокировка индекса от 2 до бесконечности.
````
begin;

update elem set c='' where id BETWEEN 2 and 5;

select INDEX_NAME, LOCK_TYPE , LOCK_MODE ,LOCK_STATUS ,LOCK_DATA  from performance_schema.data_locks
where OBJECT_NAME  = 'elem';

end
````

В параллельной сессии невозможно выполнить
````
insert into elem values(3,'Al','Br','Cr');
````
````
insert into elem values(7,'Ag','B','Co');
````

1.2)
Если строки запрошены через IN то блокировка накладывается только на строки
````
begin;

update elem set c='' where id in (2 , 5);

select INDEX_NAME, LOCK_TYPE , LOCK_MODE ,LOCK_STATUS ,LOCK_DATA  from performance_schema.data_locks
where OBJECT_NAME  = 'elem';

commit;

end
````
В параллельной сессии возможны операции
````
insert into elem values(1,'Ag','B','C')

insert into elem values (3,'Al','Br','Cr')

insert into elem values (9,'Al','B','Cd')
````

1.3) Запрос IN может вызывать блокировку интервала
````
begin;

update elem set c='' where id in (2 ,3, 5);

select INDEX_NAME, LOCK_TYPE , LOCK_MODE ,LOCK_STATUS ,LOCK_DATA  from performance_schema.data_locks
where OBJECT_NAME  = 'elem';

commit;

end

````
В параллельной сессии невозможно выполнить
````
insert into elem values (3,'Al','Br','Cr')

insert into elem values (4,'Ar','Br','Cd')
````
В параллельной сессии возможно выполнить
````
insert into elem values(1,'Ag','B','C')

insert into elem values (9,'Al','B','Cd')
````
2)
>set SESSION TRANSACTION   isolation level read committed      

Для уровня READ COMMITTED
При обновлении строк по интервалу ````BETWEEN 2 and 5```` происходит блокировка строк только с
id = 2 и id = 5
````
begin;

update elem set c='' where id BETWEEN 2 and 5;

select INDEX_NAME, LOCK_TYPE , LOCK_MODE ,LOCK_STATUS ,LOCK_DATA  from performance_schema.data_locks
where OBJECT_NAME  = 'elem';
 
end
````
В параллельной сессии невозможно выполнить
update elem set c='L' where id =2;

В параллельной сессии возможно выполнить
````
insert into elem values(3,'Al','Br','Cr');
````
````
insert into elem values(7,'Ag','B','Co');
````


3) Не уникальный индекс в уровне REPEATABLE READ
````
begin;

update elem set c='' where a BETWEEN 'Ar' and 'Au';

select INDEX_NAME, LOCK_TYPE , LOCK_MODE ,LOCK_STATUS ,LOCK_DATA  from performance_schema.data_locks
where OBJECT_NAME  = 'elem';

commit;

end
````
Полностью заблокирован вторичный индекс. Вставка строк невозможна.