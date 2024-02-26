# Файлы базы данных MySQL

Каталог данных MySQL
Путь хранится в параметре datadir.

```
mysql> select @@datadir;
+-----------------+
| @@datadir       |
+-----------------+
| /var/lib/mysql/ |
+-----------------+
1 row in set (0.00 sec)
```

В каталоге /var/lib/mysql/ расположены:

1) Журнальные файлы REDO.
Размер журнальных файлов указывается в параметре innodb_log_file_size.

2) Файл с цифровой подписью сервера auto.cnf. 

3) Сертификаты для создания безопасных подключений к БД. Файлы *.pem.

4) Каталог performance_schema хранит информацию о производительности БД MySQL.

напирмер, число подключенных пользователей

```
mysql> select * from performance_schema.users;
+-----------------+---------------------+-------------------+-------------------------------+--------------------------+
| USER            | CURRENT_CONNECTIONS | TOTAL_CONNECTIONS | MAX_SESSION_CONTROLLED_MEMORY | MAX_SESSION_TOTAL_MEMORY |
+-----------------+---------------------+-------------------+-------------------------------+--------------------------+
| NULL            |                  36 |                48 |                        272128 |                 66731832 |
| event_scheduler |                   1 |                 1 |                             0 |                    16665 |
| root            |                   1 |                 1 |                         30816 |                   216697 |
+-----------------+---------------------+-------------------+-------------------------------+--------------------------+
3 rows in set (0.00 sec)
```

5) Файл ```ibtmp1``` необходим для создания временных таблиц или внутренних таблиц.
Размер файла регулируется параметром innidb_temp_data_file_path.
   
6) Файл ```ibdata1``` содерхит данные словаря InnoDB, буфара двойной записи, буфара изменений ижурналов отмены.
Файл может содержать данные данные таблиц и индексов если выключить опцию innodb_file_per_table.
Может быть несколько файлов ibdata.
   
7) Файл ```mysql.sock``` используется для обмена данными с локальными клиентами.
Межпроцессное взаимодествие на сервере.
Параметр bind-address указывает IP адреса с которых разрешено подключение.
Параметр skip-networking отключает использование сети. То есть никакие TCP/IP соединения не будут обработаны. СУБД будет использовать только сокет.
   
8) Подкаталог ```mysql``` содержит файлы с информацией о сервере MySQL во время работы.

### MySQL 8.0

1) Журнальные файлы были перемещены из ```ibdata1``` в каталог данных.
Расположение задается параметром innodb_undo_directory.
   
2) файлы *.dblwr - это буферы двойной записи.
Формат имени #id_<размер страницы>_<номер файла>.dblwr.
Расположение задается параметром innodb_doublewrite_dir
   
3) Файл ```mysql.ibd``` хранит данные словарей и системные таблицы.