1) Активные транзакции длительностью более секунды
````
SELECT 
	ROUND(trx.TIMER_WAIT/1000000000000,3) as trx_runtime
	,trx.THREAD_ID 
	,trx.EVENT_ID as trx_event_id
	,trx.ISOLATION_LEVEL
	,trx.AUTOCOMMIT 
	,stm.CURRENT_SCHEMA as db 
	,stm.SQL_TEXT 
	,stm.ROWS_EXAMINED 
	,stm.ROWS_AFFECTED 
	,stm.ROWS_SENT 
	,if(stm.END_EVENT_ID is null,'runnig','done') as exec_state
	,ROUND(stm.TIMER_WAIT/1000000000000,3) as exec_time
from performance_schema.events_transactions_current trx
join performance_schema.events_statements_current stm using (thread_id)
where trx.STATE = 'ACTIVE'
and trx.TIMER_WAIT  > 1000000000000
````

<table>
    <thead>
        <tr>
            <th>Поле</th>
            <th>Значение</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>trx_runtime</td>
            <td>длительность транзакции</td>
        </tr>
        <tr>
            <td>THREAD_ID</td>
            <td>идентификатор клиентского подключения</td>
        </tr>
        <tr>
            <td>trx_event_id</td>
            <td>идентификатор события транзакции</td>
        </tr>
        <tr>
            <td>ISOLATION_LEVEL</td>
            <td>уровень изоляции</td>
        </tr>
        <tr>
            <td>AUTOCOMMIT</td>
            <td>YES - автокомит включен, NO - выключен</td>
        </tr>
        <tr>
            <td>db</td>
            <td>название базы данных</td>
        </tr>
        <tr>
            <td>SQL_TEXT</td>
            <td>последний запрос в транзакции</td>
        </tr>
        <tr>
            <td>ROWS_EXAMINED</td>
            <td>количество строк проверенных запросом из поля SQL_TEXT</td>
        </tr>
        <tr>
            <td>ROWS_AFFECTED</td>
            <td>количество строк измененных запросом из поля SQL_TEXT</td>
        </tr>
        <tr>
            <td>ROWS_SENT</td>
            <td>количество строк отправленных запросом из поля SQL_TEXT</td>
        </tr>
        <tr>
            <td>exec_state</td>
            <td>done - запрос выполнен, running - запрос выполнятся из поля SQL_TEXT</td>
        </tr>
        <tr>
            <td>exec_time</td>
            <td>время выполнения запроса из поля SQL_TEXT</td>
        </tr>
    </tbody>
</table>  

Аналогичный запрос в INNODB
````
select 
	trx.trx_mysql_thread_id as process_id
	,trx.trx_isolation_level
	,TIMEDIFF(now(), trx.trx_started) as trx_runtime
	,trx.trx_state
	,trx.trx_rows_locked
	,trx.trx_rows_modified
	,trx.trx_query
from information_schema.innodb_trx trx
where trx.trx_started< CURRENT_TIME - INTERVAL 1 SECOND 
```` 

2) Активные транзакции. Итоги.
````
select 
	trx.THREAD_ID 
	,max(trx.EVENT_ID) as trx_event_id
	,max(ROUND(trx.TIMER_WAIT/1000000000000,3)) as trx_runtime
	,sum(ROUND(stm.TIMER_WAIT/1000000000000,3)) as exec_time
	,sum(stm.ROWS_EXAMINED) as ROWS_EXAMINED
	,sum(stm.ROWS_AFFECTED) as ROWS_AFFECTED
	,sum(stm.ROWS_SENT) as ROWS_SENT
from performance_schema.events_transactions_current trx
join performance_schema.events_statements_history stm
on stm.THREAD_ID = trx.THREAD_ID 
and stm.NESTING_EVENT_ID = trx.EVENT_ID 
where stm.EVENT_NAME like 'statement/sql/%'
and trx.STATE ='ACTIVE'
and trx.TIMER_WAIT > 1000000000000
GROUP by trx.THREAD_ID 
````

3) Поиск истории выполнения SQL команд в транзакции
````
SELECT 
	stm.ROWS_EXAMINED as ROWS_EXAMINED 
	,stm.ROWS_AFFECTED as ROWS_AFFECTED
	,stm.ROWS_SENT  as ROWS_SENT
	,ROUND(stm.TIMER_WAIT/1000000000000,3) as exec_time 
	,stm.SQL_TEXT 
FROM performance_schema.events_statements_history stm
where stm.THREAD_ID = 54
/*and stm.NESTING_EVENT_ID*/
order by stm.EVENT_ID 
````

4) Зафиксированные транзакции
````
select 
	ROUND(max(trx.TIMER_WAIT)/1000000000000,3) as trx_time 
	,ROUND(sum(stm.TIMER_END-stm.TIMER_START)/1000000000000,3) as query_time
	,ROUND((max(trx.timer_wait)-sum(stm.TIMER_END-stm.TIMER_START))/1000000000000,3) as idle_time 
	,COUNT(stm.EVENT_ID) - 1 as query_count
	,sum(stm.ROWS_EXAMINED) as ROWS_EXAMINED
	,sum(stm.ROWS_AFFECTED) as ROWS_AFFECTED
	,sum(stm.ROWS_SENT) as ROWS_SENT
FROM performance_schema.events_transactions_history trx
join performance_schema.events_statements_history stm
on stm.NESTING_EVENT_ID = trx.EVENT_ID 
where trx.STATE ='COMMITTED'
and trx.NESTING_EVENT_ID is not null
GROUP by trx.THREAD_ID , trx.EVENT_ID 
````

<table>
    <thead>
        <tr>
            <th>Поле</th>
            <th>Значение</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>trx_time</td>
            <td>время транзакции, миллисекунды</td>
        </tr>
        <tr>
            <td>query_time</td>
            <td>общее время запроса, миллисекунды</td>
        </tr>
        <tr>
            <td>idle_time</td>
            <td>время транзакции без времени запросов(время простоя)</td>
        </tr>
        <tr>
            <td>query_count</td>
            <td>количество запросов в транзакции</td>
        </tr>
        <tr>
            <td>ROWS_EXAMINED</td>
            <td>количество строк проверенных</td>
        </tr>
        <tr>
            <td>ROWS_AFFECTED</td>
            <td>количество строк измененных</td>
        </tr>
        <tr>
            <td>ROWS_SENT</td>
            <td>количество строк отправленных</td>
        </tr>
    </tbody>
</table>  