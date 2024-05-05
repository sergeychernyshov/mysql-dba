#Настройка севера
1) установить использование файла подкачки на минимум.
Подкачка будет использоваться на севере только в случае крайней необходимости
Установка на сервере.
>echo 1 > /proc/sys/vm//swappiness

Установка значение для сохранения после перезагрузки
>vi /etc/sysctl.conf

Установить значение 
````vm.swappiness=1````
Значение 0 не очень хороший вариант, т.к. ОС будет убивать процессы,
которым не хватило памяти.

2)Поверить планировщик ввода-вывода
>cat /sys/block/sda/queue/scheduler

Приоритет noop для VM, deadline для сервера.

3)Отключить использование больших страниц памяти в Linux
````
>cat /sys/kernel/mm/transparent_hugepage/enabled
[always] madvise never
````

4)Пакет для уменьшения фрагментации RAM
установка из репозитория MySQL
>yum install jemalloc

Проверка путей
````
[root@MiWiFi-R3-srv ~]# rpm -ql jemalloc
/usr/bin/jemalloc.sh
/usr/lib64/libjemalloc.so.1
/usr/share/doc/jemalloc-3.6.0
/usr/share/doc/jemalloc-3.6.0/COPYING
/usr/share/doc/jemalloc-3.6.0/README
/usr/share/doc/jemalloc-3.6.0/VERSION
/usr/share/doc/jemalloc-3.6.0/jemalloc.html
````

Добавить в файл systemcl mysqld
>systemctl edit mysqld

строки
````
[Service]
Environment="LD_PRELOAD=/usr/lib64/libjemalloc.so.1"
````
Перезапустить сервер MySQL
> systemctl restart  mysqld

Проверить работу jemalloc
````
[root@MiWiFi-R3-srv ~]# lsof -Pn -p $(pidof mysqld) | grep "jemalloc"
mysqld  3848 mysql  mem       REG              253,0   212096    13772 /usr/lib64/libjemalloc.so.1
````

5)Параметр innodb_buffer_pool_size
отвечает за размер кеша таблиц и индексов INNODB
>show global variables like '%innodb_buffer_pool_size%'

6)размер  redo log файлов
>show global variables like '%innodb_log_file_size%'

7)Параметр innodb_numa_interleave.
Отвечает за балансировку распределения памяти в узлах.
После изменения параметра MySql нужно перезапустить
show global variables like '%innodb_numa_interleave%'