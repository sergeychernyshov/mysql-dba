Создать роль. Для создания роли необходима привилегия CREATE ROLE или CREATE USER.
Роли хранят в таблице mysql.user
>create role 'application';

Удалить роль
>drop role  'application';

Предоставить привилегии
>grant all on salika.* to 'application_rw';
>grant select on salika.* to 'application_ro';

Просмотр привилегий с ролями
>show grants for 'bob'@'192.168.31.92' using 'application_ro'

Смена роли пользователя после аутентификации
>set role 'application_rw'
>set role 'application_ro'

Сбросить все роли
>set role none

Вернуться к роли по умолчанию
>set role default

Установить все роли
>set role all
>set role all EXCEPT 'application_rw'

Получить текущие роли пользователя
>select current_role()

Роли пользователей можно задать в параметре mandatory_roles.
Роли будут доступны всем пользователям.
>show variables like 'mandatory_roles%'