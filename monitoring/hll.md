Контролировать HLL (History list length) возможно командой

>show engine innodb status

History list length 0

или SQL командой

````
select name,count
from information_schema.innodb_metrics
where name ='trx_rseg_history_len'
````