Просмотр всех переменных для текущего сеанса
>show status

Параметры могут быть доступны на разных уровнях.
GLOBAL - уровень БД, SESSION (по умолчанию) - уровень сессии.
>show status like 'Com_show_status%'
2
>show global status like 'Com_show_status%'
3

Сброс всех параметров для всех сеансов
>FLUSH status

Количество попыток подключения к MySQL (удачных и неудачных)
>show global status like 'connections';

Максимальное количество подключений к MySQL
>show global variables like 'max_connections%'

Количество подключений к MySQL
>show global status like 'Threads_connected%'

Количество запросов, которые выполняются
>show global status like 'Threads_running%'

Максимальное число коннектов, которые было с момента запуска 
>show global status like 'Max_used_connections%'

дата, когда было зафиксированном максимальное количество подключений
>show global status like 'Max_used_connections_time%'

Ошибки подключений
>show global status like 'Aborted_clients%'
>show global status like 'Aborted_connects%'

Количество выполенных запросов
>show global status like 'queries%'
>show status like 'queries%' 

Количесво выполненых запросов исключая запросы в процедурах и функциях
>show global status like 'Questions%'
>show status like 'Questions%' 

Количество выполненых различный запросов
>show global status like 'Com_%'

Количество команд (_multi значит удаление или обновление сразу нескольких таблиц)
````
show global status like 'Com_select';
show global status like 'Com_insert';
show global status like 'Com_update';
show global status like 'Com_update_multi%';
show global status like 'Com_delete';
show global status like 'Com_delete_multi%';
````

Количество команд, которые выполнили full scan таблицы
>show global status like 'select_scan%'

Количество команд, которые в запросе JOIN вызвали полное сканирование
>show global status like 'Select_full_join%'

Количество запросов, которые использовали range scan
>show global status like 'Select_range%'

Подсчет запрошенных данных из системы хранения можно найти в параметрах
>show global status like 'handler_%'

Показатель наличия не интексированных таблиц
>show global status like 'Handler_read_rnd_next%'

Подсчет числа строк без сортировки
>show global status like 'Handler_read_rnd'

Подсчет полного сканирования индекса
>show global status like 'Handler_read_rnd%'

Подсчет числа строк которые получены из индекса
>show global status like 'Handler_read_key%'

Количество медленных запросов
>show global variables like 'long_query%'

Количество медленных запросов, определяется как число запросов, 
которые выполняются больше чем значение
>show global variables like 'long_query_time%'

Количество измененных строк
````
show global status like 'Handler_delete%'
show global status like 'Handler_update%'
show global status like 'Handler_insert%'
````

Количество явно созданных временных таблиц
>show global status like 'com_create_table%'

Количество временных таблиц неявно созданных, в момент выполнения SQL
>show global status like 'Created_tmp_tables%'

Количество временных таблиц, которые были выгружены на диск
>show global status like 'Created_tmp_disk_tables%'

Количество созданных временных файлов
> show global status like 'Created_tmp_files';


Количество подготовленных запросов
>show global status like 'Com_stmt_prepare%';

Количество выполненных запросов
>show global status like 'Com_stmt_execute%';

Максимальное количество подготовленных запросов
>show global variables like 'max_prepared%';
max_prepared_stmt_count	16382

Количество разобранных запросов сейчас
>show global status like 'Prepared_stmt%';