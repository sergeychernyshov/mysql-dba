Включение лога медленных запросов для сохранения всех запросов
````
set long_query_time = 0;
set global slow_query_log = ON;
````

Поиск файла для медленных запросов
````
>show global variables like 'slow_query_log_file%'

slow_query_log_file	/var/lib/mysql/MiWiFi-R3-srv-slow.log
````