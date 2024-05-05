# Работа с базами данных MySQL

Посмтреть список всех баз данных сервера MySQL можно запросом
>show databases

Также можно ограничить список баз при помощи конструкции LIKE.
Условие LIKE регистрозависимое!
>show databases like 's%'

Создать базу можно командой
````
mysql>CREATE DATABASE sakila;
````

Удалить базу можно командой
````
mysql>DROP DATABASE sakila;
````


Команда ля создания базы с проверкой существования базы
````
mysql>CREATE DATABASE if not exists sakila;
````

Получить команду для создания базы ````sakila````
>show create database sakila

Просмотр индексов для таблицы
>show index from actor

Выбор базы данных в консоли MySQL
````
mysql> use sakila;
````
Просмотр текущей базы данных. Работает в среде разработки.
>select DATABASE()

Просмотр таблиц базы
>show tables from sakila;

Просмотр списка таблиц текущей базы. Если уже база выбрана.
>show tables;

Просмотр колонок таблицы category. Методы идентичны.
>show columns from category;
>desc city;

Получить скрипт создания таблицы.
>show create table country;

Список доступных кодировок можно посмотреть командой.
обозначение _ci значит case insensitive - не чувствительный регистр.
>show character set

Список порядков расстановки и наборов символов
>show collation


Посмотреть список глобальных параметров базы
>show GLOBAL variables

Посмотреть список параметров базы
>show variables

Ограничить список параметров возможно при помощи конструкции LIKE
>show variables like 'collation%'
 
|Variable_name|Value|
|-------------|-----|
|collation_connection|utf8mb4_0900_ai_ci|
|collation_database|utf8mb4_0900_ai_ci|
|collation_server|utf8mb4_0900_ai_ci|
 
>show variables like 'character%'

|Variable_name|Value|
|-------------|-----|
|character_set_client|utf8mb4|
|character_set_connection|utf8mb4|
|character_set_database|utf8mb4|
|character_set_filesystem|binary|
|character_set_results||
|character_set_server|utf8mb4|
|character_set_system|utf8mb3|
|character_sets_dir|/usr/share/mysql-8.0/charsets/|

Создание базы с указанием кодировки и порядкa расстановки.
_cs - регистрозависимая кодировка.
>create database rose default character set utf8mb4 collate utf8mb4_ru_0900_as_cs;


Показать предупреждения после выполнения команд
>show warnings;
  
Посмотреть уровень изоляции транзакций
>SELECT @@transaction_ISOLATION;

Смена уровня изоляции на уровне сессии
Можно применять на уровне GLOBAL, SESSION, NEXT_TRANSACTION 
>set session transaction isolation LEVEL  serializable
>set session transaction isolation LEVEL read COMMITTED 



Просмотр параметра autocommit
>select @@autocommit
>show variables like 'autocommit%'

Смена параметра autocommit
>set session autocommit=0

Включить возможность просмотра замков
````
select * from performance_schema.setup_instruments
where name = 'wait/lock/metadata/sql/mdl';

update performance_schema.setup_instruments set enabled = 'YES'
where name = 'wait/lock/metadata/sql/mdl';
````

Просмотр замков
>select * from sys.schema_table_lock_waits  
````
select 
	object_name, 
	waiting_thread_id, 
	waiting_lock_type, 
	waiting_query, 
	sql_kill_blocking_query, 
	blocking_thread_id
from sys.schema_table_lock_waits  
````

Просмотр замков
>select * from performance_schema.metadata_locks

Просмотр всех замков из других сеансов
````
SELECT 
	OBJECT_TYPE,
	OBJECT_SCHEMA ,
	OBJECT_NAME ,
	LOCK_TYPE ,
	LOCK_STATUS ,
	THREAD_ID,
	processlist_id,
	processlist_info
from performance_schema.metadata_locks
inner join performance_schema.threads
on thread_id = owner_thread_id
where processlist_id <> connection_id()
````

Проверить ошибки движка
>show engine innodb status