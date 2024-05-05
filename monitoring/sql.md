Время отклика на запрос
````
select
ROUND(BUCKET_QUANTILE * 100, 1) as p,
ROUND(BUCKET_TIMER_HIGH/1000000000, 3) as ms
from performance_schema.events_statements_histogram_global
where bucket_quantile >= 0.95
````

Количество ошибок в sql (ERROR_NUMBER = 1287 предупреждение об использовании устаревших конструкций)
````
select sum(SUM_ERROR_RAISED) as global_errors
from performance_schema.events_errors_summary_global_by_error
where ERROR_NUMBER != 1287
````

````
select sum(SUM_ERRORS) as query_errors
from performance_schema.events_statements_summary_global_by_event_name
where EVENT_NAME like 'statement/sql/%'
````

Ошибки подключения
show status like 'Aborted_clients%'
show status like 'Aborted_connects%'

show status like 'Connection_errors_accept'
show status like 'Connection_errors_internal'
show status like 'Connection_errors_max_connections'
show status like 'Connection_errors_peer_address'
show status like 'Connection_errors_select'
show status like 'Connection_errors_tcpwrap'


Количество запросов (все запросы БД, в том числе и внутри триггеры)
show status like 'queries%'

Количество запросов отправленных пользователем
show status like 'questions%'

Количество транзакций можно узнать из метрик
show status like 'com_begin%'
show status like 'com_commit%'
show status like 'Com_rollback'
show status like 'Com_rollback_to_savepoint%'

В INNODB количество транзакций можно узнать
````
select count from information_schema.innodb_metrics
where name like 'trx_active_transactions%'
````

Полное сканирование при соединении
>show global status like 'Select_full_join';

Соединение по диапазону
>show global status like 'Select_full_range_join';

Соединение по диапазону
>show global status like 'Select_range';

Соединение по диапазону
>show global status like 'Select_range_check';

Соединение без ключей
>show global status like 'Select_scan';