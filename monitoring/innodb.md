Количество измененных строк
````
show global status like 'Innodb_rows_inserted%'
show global status like 'Innodb_rows_updated%'
show global status like 'Innodb_rows_deleted%'
````

Количество прочитанных строк
>show global status like 'Innodb_rows_read%'

Количество прочитанных байт
>show global status like 'Innodb_data_read%'

Количество записанный на диск байт
>show global status like 'Innodb_data_written%'

Количество записанный в журнал переделок байт
> show global status like 'Innodb_os_log_written%'

Байты прочтенные с диска суммарно
>show global status like 'innodb_data_reads'

Байты записанные на диск суммарно
>show global status like 'innodb_data_writes'

Количество записанных страниц данных
> show global status like 'Innodb_pages_written%'

Количество записанных страниц данных из буферного пула
> show global status like 'Innodb_buffer_pool_pages_flushed%'

Объем данных ожидающих операций 
>show global status like 'Innodb_%pending%'

Число запросов на чтение
>show global status like 'Innodb_buffer_pool_read_requests%'

Число страниц для чтения с диска 
>show global status like 'Innodb_buffer_pool_reads%'

Подсчет числа открытых транзакций, операций commit и rollback
````
show global status like 'Com_begin%'
show global status like 'Com_commit%'
show global status like 'Com_rollback%'
````

Количество транзакций, которые ожидают снятия замка
>show global status like 'Innodb_row_lock_current_waits%'

Количеств ожиданий снятия замка
>show global status like 'Innodb_row_lock_waits%'

Время ожидания снятия замка, суммарно, максимальное, среднее в миллисекундах
````
show global status like 'Innodb_row_lock_time%'
show global status like 'Innodb_row_lock_time_max%'
show global status like 'Innodb_row_lock_time_avg%'
````

Отчет о состоянии движка INNODB
>show engine innodb status;


Количество транзакций горизонта событий (норма до 1000, критически 100000)
````
select * from information_schema.innodb_metrics
where name like 'trx_rseg_history_len%'
````

Количество deadlock сессий убитых базой MySQL
````
select * from information_schema.innodb_metrics
where name like 'lock_deadlocks%'
````

Количество миллисекунд потраченных на получение блокировки строк
````
select * from information_schema.innodb_metrics
where name like 'lock_row_lock_time%'
````

Текущее количество запросов, которые ожидают блокировок строк
````
select * from information_schema.innodb_metrics
where name like 'lock_row_lock_current_waits%'
````

Текущее количество запросов, которые ожидают получения строки
````
select * from information_schema.innodb_metrics
where name like 'lock_row_lock_waits%'
````

Общее время ожидания блокировок
````
select * from information_schema.innodb_metrics
where name like 'lock_timeouts%'
````

Количество страниц в буфере
>show global status like 'Innodb_buffer_pool_pages_total%'

% грязных страниц в буфере
>show global status like 'Innodb_buffer_pool_pages_dirty%'

% свободных страниц в буфере
>show global status like 'Innodb_buffer_pool_pages_free%'