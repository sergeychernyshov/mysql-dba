Утилита mysqldump подключается при помощи логина и пароля в файле конфигурации в разделе [client].
Если не настроен файл конфигурации нужно будет вводить логин и пароль.

Получить дамп базы MySql в консоле можно командой
>mysqldump sakila

Получить DDL команды для создания структуры
>mysqldump --no-data sakila 

Дамп одной таблицы
> mysqldump sakila actor

Ограничить дамп можно условием WHERE
>mysqldump sakila actor --where="actor_id < 10";

Полный дамп всех баз
>mysqldump --all-databases --triggers --routines --events > dump.sql

Полный согласованный дамп можно получить при помощи опции --single-transaction
>mysqldump --all-databases --triggers --routines --events --single-transaction> dump.sql

Архив с дампом
>mysqldump --all-databases --triggers --routines --events --single-transaction | gzip > dump.sql.gzmusql
