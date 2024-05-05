Список пользователя MySQL
>show privileges

Глобальные привилегии
1) Динамические: Привилегии которые появляются при установке плагинов
>select * from mysql.global_grants

    
2) Статические
>select * from mysql.user

Привилегии на уровне базы
>select * from mysql.db

Привилегии на таблицы
>select * from mysql.tables_priv

Привилегии уровня столбцов
>select * from mysql.columns_priv

Привилегии для хранимых процедур и функций
>select * from mysql.procs_priv

Привилегии прокси пользователя
>select * from mysql.proxies_priv

Роли по умолчанию
>select * from mysql.default_role

Ребра ролевых подграфов
>select * from mysql.role_edges

История смены паролей
>select * from mysql.password_history

Загрузить данные из этих таблиц в память 
>FLUSH PRIVILEGES

Просмотр привилегий для пользователя
>show grants for 'bob'@'192.168.31.%'

Просмотр привилегий под конкретным пользователем
>show grants
>show grants for current_user
>show grants for current_user()

Просмотр привилегий с ролями
>show grants for 'bob'@'192.168.31.92' using 'application_ro'

GROUP_REPLICATION_ADMIN - привилегии для настройки репликации