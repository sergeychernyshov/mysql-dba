
show variables like '%default_aut%' - плагин для аутентификации

bob'@'%' - подключение возможно с любого адреса.

create user 'bob'@'192.168.31.%' identified by 'Serka_1312';

create user 'bob2'@'192.168.31.%'
identified with mysql_native_password
by 'Serka_1312'
default role 'user_role' --установки роли по умолчанию
require SSL and cipher 'EDH-RSA-DES-CBC3-SHA'
with max_user_connections 10
password expire never;


create user 'bob2'@'192.168.31.%'
identified with mysql_native_password
by 'Serka_1312'
default role 'user_role'
require SSL
with max_user_connections 10
password expire never;


Пользователь может выполнять 10 запросов в час
подключаться не чаще 1 раза в час
выполнять подключение 2 раза в час

create user 'bob3'@'192.168.31.%'
with max_queries_per_hour 10
max_connections_per_hour 2
max_user_connections 1;

Получить текущего пользователя возможно
select current_user(), user()

Получить текущие роли пользователя
select current_role()

Посмотреть плагин Аутентификации
select host, user, plugin  from mysql.user

Смена плагина аутентификации
alter user 'bob'@'192.168.31.%' identified with mysql_native_password 

Смена пароля
alter user 'bob'@'192.168.31.%' identified by 'Pass!sdf123'

Блокировка пользователя
alter user 'bob'@'192.168.31.%' account lock

Разблокировка пользователя
alter user 'bob'@'192.168.31.%' account unlock

Установка срока действия пароля
alter user 'bob'@'192.168.31.%' password expire

Переименование пользователя(можно менять адрес)
rename user 'bob'@'192.168.31.%' to  'bob2'@'192.168.31.%'
rename user 'bob2'@'192.168.31.%' to  'bob3'@'192.168.32.%'

Удаление пользователя
DROP  user 'bob3'@'192.168.32.%'
DROP  user if exists 'bob3'@'192.168.32.%'

Запрос для проверки объектов пользователя
````
select 
	event_schema as obj_schema,
	event_name as obj_name,
	'EVENT' as obj_type
from Information_schema.events
where DEFINER = 'bob@localhost'
union
select 
	routine_schema as obj_schema,
	routine_name as obj_name,
	routine_type as obj_type
from Information_schema.routines
where DEFINER = 'bob@localhost'
union
select 
	trigger_schema as obj_schema,
	trigger_name as obj_name,
	'trigger' as obj_type
from Information_schema.triggers
where DEFINER = 'bob@localhost'
union
select 
	table_schema as obj_schema,
	table_name as obj_name,
	'view' as obj_type
from Information_schema.views
where DEFINER = 'bob@localhost'
union
select 
	user as obj_schema,
	host as obj_name,
	'proxy_user' as obj_type
from mysql.proxies_priv
where Proxied_host  = 'localhost'
and proxied_user = 'bob'
````
